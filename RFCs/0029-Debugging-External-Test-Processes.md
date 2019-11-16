# 0029 Debugging External Test Processes

# Summary
Introduce APIs to improve debugging support in Visual Studio for tests that run in an external process distinct from `testhost*.exe`.

# Motivation
Some test frameworks (examples include [TAEF](https://docs.microsoft.com/en-us/windows-hardware/drivers/taef/) and [Python](https://docs.microsoft.com/en-us/visualstudio/python/unit-testing-python-in-visual-studio)) need to execute tests in a external process distinct from `testhost*.exe`. When it comes to debugging such tests in Visual Studio today, there are a couple of problems. 

1. A test adapter can request to launch a child process with debugger attached by calling  [`IFrameworkHandle.LaunchProcessWithDebuggerAttached()`](https://github.com/microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Adapter/Interfaces/IFrameworkHandle.cs#L29) within adapter's implementation of [`ITestExecutor.RunTests()`](https://github.com/microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Adapter/Interfaces/ITestExecutor.cs#L23) (after checking that [`IRunContext.IsBeingDebugged`](https://github.com/microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Adapter/Interfaces/IRunContext.cs#L32) is `true`). However, there is no supported way for a test adapter to request that debugger should be attached to an **already running process**.

2. Even though a test adapter can launch a child process with debugger attached as described above, today the debugger is always attached to the `testhost*.exe` process as well meaning that **Visual Studio ends up debugging two processes** instead of just the single process where tests are running.

Debugging of Python tests is supported in VS today. However, the Python adapter works around the above limiations by talking to the Python extension inside VS whenever `ITestExecutor.RunTests()` is invoked and `IRunContext.IsBeingDebugged` is true. The Python extension in VS then attaches VS debugger to the Python test process independently and also detaches the `testhost*.exe` process to achieve the desired behavior. While this works for Python, not all test frameworks that need to support debugging of tests running in external processes would want their users to also install a VS extension. For this reason, debugging of TAEF tests is currently not supported in VS.

# Proposed Changes
1. Introduce a new interface `IFrameworkHandle2` that inherits [`IFrameworkHandle`](https://github.com/microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Adapter/Interfaces/IFrameworkHandle.cs#L12) and adds the following `AttachDebuggerToProcess()` API that an adapter can invoke from within [`ITestExecutor.RunTests()`](https://github.com/microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Adapter/Interfaces/ITestExecutor.cs#L23). 

```
namespace Microsoft.VisualStudio.TestPlatform.ObjectModel.Adapter
{
    /// <summary>
    /// Handle to the framework which is passed to the test executors.
    /// </summary>
    public interface IFrameworkHandle2 : IFrameworkHandle
    {
        /// <summary>
        /// Attach debugger to an already running process.
        /// </summary>
        /// <param name="pid">Process ID of the process to which the debugger should be attached.</param>
        /// <returns><see cref="true"/> if the debugger was successfully attached to the requested process, <see cref="false"/> otherwise.</returns>
        bool AttachDebuggerToProcess(int pid);
    }
}
```

```
// Adapter's implementation of ITestExecutor.RunTests()
void ITestExecutor.RunTests(IEnumerable<TestCase> tests, IRunContext runContext, IFrameworkHandle frameworkHandle)
{
    ...

    if (runContext.IsBeingDebugged && frameworkHandle is IFrameworkHandle2 frameworkHandle2)
    {
        frameworkHandle2.AttachDebuggerToProcess(testProcessId);
    }

    ...
}
```

2. (Optional) Introduce a new `ITestExecutor2` interface that inherits [`ITestExecutor`](https://github.com/microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Adapter/Interfaces/ITestExecutor.cs#L15) and adds the following `RunTests()` API. Newer adapters can choose to implement `ITestExecutor2` instead of `ITestExecutor`. This would allow them to access `IFrameworkHandle2` without needing to cast from `IFrameworkHandle` to `IFrameworkHandle2`.

3. Introduce a new `ITestHostLauncher2` interface that inherits [`ITestHostLauncher`](https://github.com/microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Client/Interfaces/ITestHostLauncher.cs#L11) and adds the following `AttachDebuggerToProcess()` API. Visual Studio's Test Explorer will supply an implementation of this interface via [`IVsTestConsoleWrapper.RunTestsWithCustomTestHost()`](https://github.com/microsoft/vstest/blob/master/src/Microsoft.TestPlatform.VsTestConsole.TranslationLayer/Interfaces/IVsTestConsoleWrapper.cs#L120) and `ITestHostLauncher2.AttachDebuggerToProcess()` will be called when  `IFrameworkHandler2.AttachDebuggerToProcess()` is called within an adapter.

```
namespace Microsoft.VisualStudio.TestPlatform.ObjectModel.Client.Interfaces
{
    /// <summary>
    /// Interface defining contract for custom test host implementations
    /// </summary>
    public interface ITestHostLauncher2 : ITestHostLauncher
    {
        /// <summary>
        /// Attach debugger to already running custom test host process.
        /// </summary>
        /// <param name="pid">Process ID of the process to which the debugger should be attached.</param>
        /// <returns><see cref="true"/> if the debugger was successfully attached to the requested process, <see cref="false"/> otherwise.</returns>
        bool AttachDebuggerToProcess(int pid);
    }
}

```

4. (Optional) Introduce a new `IVsTestConsoleWrapper2` interface that inherits [`IVsTestConsoleWrapper`](https://github.com/microsoft/vstest/blob/master/src/Microsoft.TestPlatform.VsTestConsole.TranslationLayer/Interfaces/IVsTestConsoleWrapper.cs#L15) and adds the following `RunTestsWithCustomTestHost()` APIs. Visual Studio's Test Explorer can call this API and directly supply instance of `ITestHostLauncher2` without the needing to cast from `ITestHostLauncher2` to [`ITestHostLauncher`](https://github.com/microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Client/Interfaces/ITestHostLauncher.cs#L11).

5. Introduce a new well-known `TestProperty` - `TestCaseProperties.UsesCustomTestHostProcess` - that an adapter can tack on to `TestCase`s that will execute in a separate external process distinct from `testhost*.exe`. If all selected tests in a debugging session have this property attached, then the Test Platform and Visual Studio can avoid attaching debugger to the `testhost*.exe` process. Note: This may have some perf implication when debugging large selections (as the check will be performed even in cases where the property is not present). However, the scenario where someone wants to debug a large enough number of `TestCase`s where this would become a problem should be rare. I assume that the overhead of checking presence of one `TestProperty` on the selected `TestCases`s should not be huge for most regular debugging operations.

```
namespace Microsoft.VisualStudio.TestPlatform.ObjectModel
{
    ...

    public static class TestCaseProperties
    {
        ...

        public static readonly TestProperty UsesCustomTestHostProcess =
            TestProperty.Register(
                id: "TestCase.UsesCustomTestHostProcess",
                label: "UsesCustomTestHostProcess",
                category: string.Empty,
                description: string.Empty,
                valueType: typeof(bool),
                validateValueCallback: (object value) => value is bool,
                attributes: TestPropertyAttributes.Hidden,
                owner: typeof(TestCase));

        ...
   }

   ...
}
```
