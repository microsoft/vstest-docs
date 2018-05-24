# 0015 Telemetry Design

## Summary
This note details the Telemetry design for the Test Platform.

## Motivation
Telemetry will help us make the test experience better.

## Data Points collected by TestPlatform
* Total number of tests discovered/ran by each adapter.
* Total number of adapters discovered.
* Number of sources sent for discovery/execution.
* Total time taken by each adapter to run/discover Tests.
* Total adapters used to run/discover tests.
* Total time taken for discovery/execution.
* Paralled enabled or not.
* List of Data Collectors Enabled.
* List of loggers Used.
* Discovery/Execution State.
* TargetOS.
* Target Framework.
* Target Platform.
* Target Device.
* MaxCPU count.
* TestPlatform Version.
* CommandLine switches Used {/Settings, /Parallel, /EnableCodeCoverage, /InIsolation, /Platform, /Framework, /UseVsixExtensions}.

### Sending Consent for collecting Telemetry Metrics in Test Platform in Design Mode
**Collection in Test Platform will only happen if TestPlatform receives consent from the consumers.**

The "CollectMetrics" field has been added in [TestPlatformOptions](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Client/TestPlatformOptions.cs) to send consent from Design Mode Scenarios(VS, VSCode etc) to TestPlatform. The users have to set "CollectMetrics" so that TestPlatform can collect Metrics and send it back to the users.

The [IVsTestConsoleWrapper](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.VsTestConsole.TranslationLayer/Interfaces/IVsTestConsoleWrapper.cs) and [IVsTestConsoleWrapperAsync](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.VsTestConsole.TranslationLayer/Interfaces/IVsTestConsoleWrapperAsync.cs) contains API's that support TestPlatformOptions. Users must use these API's to send consent to the TestPlatform for collecting Metrics.

**For Instance**
For Discovery : Users have to use this API to pass TestPlatform Options.

        /// <summary>
        /// Start Discover Tests for the given sources and discovery settings.
        /// </summary>
        /// <param name="sources">List of source assemblies, files to discover tests</param>
        /// <param name="discoverySettings">Settings XML for test discovery</param>
        /// <param name="options">Options to be passed into the platform.</param>
        /// <param name="discoveryEventsHandler">EventHandler to receive discovery events</param>
        void DiscoverTests(IEnumerable<string> sources, string discoverySettings, TestPlatformOptions options, ITestDiscoveryEventsHandler2 discoveryEventsHandler);
        
For Execution using sources: Users have to use this API to pass TestPlatform Options.

        /// <summary>
        /// Starts a test run given a list of sources.
        /// </summary>
        /// <param name="sources">Sources to Run tests on</param>
        /// <param name="runSettings">RunSettings XML to run the tests</param>
        /// <param name="options">Options to be passed into the platform.</param>
        /// <param name="testRunEventsHandler">EventHandler to receive test run events</param>
        void RunTests(IEnumerable<string> sources, string runSettings, TestPlatformOptions options, ITestRunEventsHandler testRunEventsHandler);

Similarly, while running tests using TestCases, there are API's available to send TestPlatformOptions along with them.

## Telemetry Design
### Collecting Data
* Collect Telemetry Data Points in various process(testhost,datacollector etc) and send it to vstest.console process where it will be uploaded or send back to users in design mode. 

**For eg:**
* In Test Host Process:
We have to collect how much time does each executor took to run test, Time taken to load adapters etc.

* In Vstest.console:
We have to collect Total Discovery Time taken, Total Tests Run in case of parallel scenarios.

#### Aggregating data points in Test Host process

* It may happen that TestHost is on a newer version whereas vstest.console is on older version. So, TestHost process should not collect Metrics by default. So, is should only collect Metrics when users give consent to collect Metrics.
So, for sending consent from Vstest.console process to Test Host, Command line argument i.e. boolean **TelemetryOptedIn** is sent to TestHost Process from Vstest.console process.

The interface [IRequestData](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Client/Interfaces/IRequestData.cs) has been has been exposed to TestHost process which contains [IMetricCollection](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Client/Interfaces/IMetricsCollection.cs) which will collect the Metrics in a dictionary.

#### Sending Metrics from TestHost process to vstest.console process
Currently, At the end of Discovery Complete, we are sending **TestDiscovery.Complete** message event along with DiscoveryCompletePayload, so we will add our collected Metrics along with [DiscoveryCompletePayload](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.CommunicationUtilities/Messages/DiscoveryCompletePayload.cs). Similar will be done at end of **TestExecution.Complete** event where we will add the Metrics in [TestRunCompleteEventArgs](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Client/Events/TestRunCompleteEventArgs.cs). This helps us in sending whole metrics in one go and helps us to decrease performance overhead of sending messages from test host process to vstest.console process.

In VsTestConsole process, the metrics which will be received from TestHost process will be aggregated with the VsTestConsole own metrics.

### Publishing Data

For Publishing data, there are two scenarios:
* Design Mode: We will be aggregating all the data in vstest.console and send to various IDE's(VS, VSCode etc) giving the IDE's options to add this telemetry data along with thier own Telemetry.

* Non-Design Mode:
We will be using VSTelemetry for first phase as of now to cover all windows scenarios. In phase 2, we will be extending support for crossplat.

### Consuming Metrics in Design Mode Scenarios from Test Platform
The whole aggregated metrics will be appended in vstest.console process in the final Execution/Disocvery Complete message and it will be send back to the consumers. When users use API's that are available in [IVSTestConsoleWrapper](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.VsTestConsole.TranslationLayer/Interfaces/IVsTestConsoleWrapper.cs), they have to pass the event handler which will contain API's to get back the Metrics from TestPlatform.

In Case of Execution, users will pass [ITestRunEventsHandler](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Client/Interfaces/ITestRunEventsHandler.cs), which contains [TestRunCompleteEventArgs](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Client/Events/TestRunCompleteEventArgs.cs) which will have Metrics in it which users can consume.

In Case of Discovery, users have to pass new interface [ITestDiscoveryEventsHandler2](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Client/Interfaces/ITestDiscoveryEventsHandler2.cs) which contains [DiscoveryCompleteEventArgs](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Client/Events/DiscoveryCompleteEventArgs.cs) which will have metrics in it which users can consume.
