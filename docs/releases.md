# Release Notes

## 15.0.0-preview-20161227.02

* Add enhancement: trx logger can take logfile parameter [#282](https://github.com/Microsoft/vstest/pull/282).
* Allow TranslationLayer to specify Diag parameters [#296](https://github.com/Microsoft/vstest/pull/296).
* Passing runsettings as command line arguments [#297](https://github.com/Microsoft/vstest/pull/297).
* Localization work [#302](https://github.com/Microsoft/vstest/pull/302).
* Testhost Diag log file name format change [#303](https://github.com/Microsoft/vstest/pull/303).
* Fix for issue where xlftool.exe is not able to update neutral xlf file if we update any existing resource string [#305](https://github.com/Microsoft/vstest/pull/305).

A list of all changes since last release are available [here](https://github.com/Microsoft/vstest/compare/v15.0.0-preview-20161216-01...v15.0.0-preview-20161227-02).

### Drops

* TestPlatform vsix: [TestPlatform.CI.Real-20161227-02](https://devdiv.visualstudio.com/DevDiv/VS.in%20Agile%20Testing%20IDE/_build/index?buildId=490545&_a=summary&tab=artifacts)
* Microsoft.TestPlatform.ObjectModel: [15.0.0-preview-20161227-02](https://dotnet.myget.org/feed/vstest/package/nuget/Microsoft.TestPlatform.ObjectModel/15.0.0-preview-20161227-02)
* Microsoft.TestPlatform.TranslationLayer: [15.0.0-preview-20161227-02](https://dotnet.myget.org/feed/vstest/package/nuget/Microsoft.TestPlatform.TranslationLayer/15.0.0-preview-20161227-02)

## 15.0.0-preview-20161216.01

* Migrate to csproj from xproj [#217](https://github.com/Microsoft/vstest/pull/217).
* Translationlayer timeout for CustomHost Launch changed to indefinate [#265](https://github.com/Microsoft/vstest/pull/265)
* Added net46 folder in lib of Microsoft.TestPlatform Nuget Package [#247](https://github.com/Microsoft/vstest/pull/247).
* Added license link.
* Added third party notice to nuget packages [#249](https://github.com/Microsoft/vstest/pull/249).
* Change assembly signing to public [#256](https://github.com/Microsoft/vstest/pull/256).
* Make testhost a project dependency instead of content [#264](https://github.com/Microsoft/vstest/pull/264).
* Several changes to build infrastructure for csproj migration [#262](https://github.com/Microsoft/vstest/pull/262) [#268](https://github.com/Microsoft/vstest/pull/268/files).
* Include microbuild.core as a dependency for signing [#267](https://github.com/Microsoft/vstest/pull/267).
* Make External packages are restored with a separate csproj [#273](https://github.com/Microsoft/vstest/pull/273).
* Add Acceptance tests for netcore1.0 target [#259](https://github.com/Microsoft/vstest/pull/259).
* Add Acceptance tests for netcore1.1 target [#270](https://github.com/Microsoft/vstest/pull/270).
* Added E2E test for RunTestsWithCustomTestHostLauncher.
* Change testcase gereration id algorithm to SHA1 to be in compat with Associate-WorkItem scenarios [#279](https://github.com/Microsoft/vstest/pull/279).
* Bug fix: Default logger output path should be cmd-line friendly [#244](https://github.com/Microsoft/vstest/issues/244).
* Bug fix: TRX logger Started Time incorrect [#253](https://github.com/Microsoft/vstest/pull/253).
* Update README.md [#263](https://github.com/Microsoft/vstest/pull/263).

A list of all changes since last release are available [here](https://github.com/Microsoft/vstest/compare/v15.0.0-preview-20161123-03...v15.0.0-preview-20161216-01).

### Drops

* TestPlatform vsix: [TestPlatform.CI.Real-20161216-01](https://devdiv.visualstudio.com/DevDiv/VS.in%20Agile%20Testing%20IDE/_build/index?buildId=474910&_a=summary&tab=summary)
* Microsoft.TestPlatform.ObjectModel: [15.0.0-preview-20161216-01](https://dotnet.myget.org/feed/vstest/package/nuget/Microsoft.TestPlatform.ObjectModel/15.0.0-preview-20161216-01)
* Microsoft.TestPlatform.TranslationLayer: [15.0.0-preview-20161216-01](https://dotnet.myget.org/feed/vstest/package/nuget/Microsoft.TestPlatform.TranslationLayer/15.0.0-preview-20161216-01)

## 15.0.0-preview-20161123.03

* Support for debugging .net core project.
* Support for parallel discovery and execution.
* Support to discover and run test from a solution having .net core and desktop project.
* Support of arguments(output, configuration, framework and noBuild) in dotnet test.
* Support to run test from project targeting multiple TargetFrameworkMoniker using dotnet test.
* Support for trx logger in non-windows machine.
* Added diag argument to enable logging in vstest.console.
* Acceptance test for test platform.
* Bug fix: display a message on console when dotnet is not installed on the machine.
* Bug fix: dotnet test should return a non-0 exit code when any test fails [here](https://github.com/Microsoft/vstest/issues/241).
* Bug fix: dotnet test fails due to missing quotes in the path of vstest.console [here](https://github.com/Microsoft/vstest/issues/231).
* Bug fix: terminate vstest.console if no testhost found [here](https://github.com/Microsoft/vstest/issues/144).
* Bug fix: testCaseFilter argument doesn't filter tests in .net core [here](https://github.com/Microsoft/vstest/issues/201).
* Bug fix: cannot add Microsoft.Net.Test.Sdk as a dependency of net451 projects [here](https://github.com/Microsoft/vstest/issues/190).

A list of all changes since last release are available [here](https://github.com/Microsoft/vstest/compare/v15.0.0-preview-20160923-03...v15.0.0-preview-20161123-03).

### Drops

* TestPlatform vsix: [TestPlatform.CI.Real-20161123-03](https://devdiv.visualstudio.com/DevDiv/VS.in%20Agile%20Testing%20IDE/_build/index?buildId=442970&_a=summary)
* Microsoft.TestPlatform.ObjectModel: [15.0.0-preview-20161123-03](https://dotnet.myget.org/feed/vstest/package/nuget/Microsoft.TestPlatform.ObjectModel/15.0.0-preview-20161123-03)
* Microsoft.TestPlatform.TranslationLayer: [15.0.0-preview-20161123-03](https://dotnet.myget.org/feed/vstest/package/nuget/Microsoft.TestPlatform.TranslationLayer/15.0.0-preview-20161123-03)

## 15.0.0-preview-20160923-03

* New configuration `DisableParallelization` in runsettings. This setting may be used by adapters to disable parallel run in certain scenarios, e.g. test profiling or instrumented runs.
* Support for non-shared test hosts. A non shared test host is exclusive per test source. E.g. .net core tests use a non-shared host.
* New nuget package: Microsoft.TestPlaform.TestHost. All .net core test apps will refer to this package.
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
