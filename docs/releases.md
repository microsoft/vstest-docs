# Release Notes

## 15.0.0-preview-20160923-03

* New configuration `DisableParallelization` in runsettings. This setting may be used by adapters to disable parallel run in certain scenarios, e.g. test profiling or instrumented runs.
* Support for non-shared test hosts. A non shared test host is exclusive per test source. E.g. .net core tests use a non-shared host.
* Sample performance tests for test platform
* Bug fix: support for reg free COM in Dia
* Bug fix: display a message in VS on test host crash
* Bug fix: in .net core, user may provide relative path to run tests

A list of all changes since last release are available [here](https://github.com/Microsoft/vstest/compare/v15.0.0-preview-20160914-02...v15.0.0-preview-20160923-03).

### Drops

* TestPlatform vsix: [TestPlatform.CI.Real-20160923-03](https://devdiv.visualstudio.com/DevDiv/VS.in%20Agile%20Testing%20IDE/_build/index?buildId=343725&_a=summary)
* Microsoft.TestPlatform.ObjectModel: [15.0.0-preview-20160923-03](https://dotnet.myget.org/feed/vstest/package/nuget/Microsoft.TestPlatform.ObjectModel/15.0.0-preview-20160923-03)
* Microsoft.TestPlatform.TranslationLayer: [15.0.0-preview-20160923-03](https://dotnet.myget.org/feed/vstest/package/nuget/Microsoft.TestPlatform.TranslationLayer/15.0.0-preview-20160923-03)

## 15.0.0-preview-20160914-02

* Support for .net core framework
* New nuget package `Microsoft.Testplatform.CLI` for dotnet-cli
* Performance instrumentation of runner, discovery and execution
* Bug fix: Handle crash of test host
* Bug fix: Handle paths and arguments on Unix
* Bug fix: Sign core binaries

### Drops

* TestPlatform vsix: [TestPlatform.CI.Real-20160914-02](https://devdiv.visualstudio.com/DevDiv/VS.in%20Agile%20Testing%20IDE/_build/index?buildId=329464&_a=summary)
* Microsoft.TestPlatform.ObjectModel: [15.0.0-preview-20160914-02](https://dotnet.myget.org/feed/vstest/package/nuget/Microsoft.TestPlatform.ObjectModel/15.0.0-preview-20160914-02)
* Microsoft.TestPlatform.TranslationLayer: [15.0.0-preview-20160914-02](https://dotnet.myget.org/feed/vstest/package/nuget/Microsoft.TestPlatform.TranslationLayer/15.0.0-preview-20160914-02)
