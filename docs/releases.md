# Release Notes

## 15.3.0-preview-20170601-03

* Monitor data Collector Launch and Exit events, log error in case data collector crashes.
* Fixed for issue where using environment variables in test results directory path in run settings throws error.
* Added support to handle `CollectSourceInformation` flag in runsettings
* Fixed scenario where testhost crash info is not coming to Testwindow
* In case of parallel if test host is aborted, add a new one in place of that

### Issue Fixed
* https://github.com/Microsoft/vstest/issues/823


A list of all changes since last release are available [here](https://github.com/Microsoft/vstest/compare/v15.3.0-preview-20170517-02...v15.3.0-preview-20170601-03).

### Drops

* TestPlatform vsix: [15.3.0-preview-20170601-03](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20170601-03;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [15.3.0-preview-20170601-03](http://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.3.0-preview-20170601-03)

## 15.3.0-preview-20170517-02

* Fakes support.
* Wait for testhost stderr to be available if connection is broken between vstest.console and testhost.
* Data collector log message improvements.
* Extracedt socket implementation to allow experimentation with multiple data interchange formats and ipc. Added concept of framing for messages passed between various processes. TestRequestSender2 uses these concepts and is a replacement for the earlier TestRequestSender.
* Localized new added string.
* Code cleanup


### Issue Fixed
* https://github.com/Microsoft/vstest/issues/646
* https://github.com/Microsoft/vstest/issues/706
* https://github.com/Microsoft/vstest/issues/618
* https://github.com/Microsoft/vstest/issues/801
* https://github.com/Microsoft/vstest/issues/799


A list of all changes since last release are available [here](https://github.com/Microsoft/vstest/compare/v15.3.0-preview-20170427-09...v15.3.0-preview-20170517-02).

### Drops

* TestPlatform vsix: [15.3.0-preview-20170517-02](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20170517-02;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [15.3.0-preview-20170517-02](http://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.3.0-preview-20170517-02)


## 15.3.0-preview-20170425-07

* Data collector support enabled
* Test Host Extensibility enabled
* ResultsDirectory argument and Runsettings priority order [#322](https://github.com/Microsoft/vstest/pull/322)
* Supporting Multiple TestProperty with the same key value [#328](https://github.com/Microsoft/vstest/pull/328)
* Allow VSTestConsole path to be specified [#325](https://github.com/Microsoft/vstest/pull/325)
* Adding /InIsolation flag for backward compatibility [#414](https://github.com/Microsoft/vstest/pull/414) 
* Fixed reading test adapter paths from runsettings [#455](https://github.com/Microsoft/vstest/pull/455)
* Honor cache timeout for discovery. [#470](https://github.com/Microsoft/vstest/pull/470)
* Read asynchronously from test host process [#529](https://github.com/Microsoft/vstest/pull/529)
* Fixing nunit inconclusive tests reported as failure [#533](https://github.com/Microsoft/vstest/pull/533)
* BatchSize Runsettings [#550](https://github.com/Microsoft/vstest/pull/550)
* Make default testcase filter property name FullyQualifiedName [#555](https://github.com/Microsoft/vstest/pull/555)
* Logger extensibility [#557](https://github.com/Microsoft/vstest/pull/557)
* Update Microsoft.VisualStudio.TestTools.TestPlatform.V2.CLI.vsmanproj [#581](https://github.com/Microsoft/vstest/pull/581)
* Add Microsoft.NET.Test.Sdk.props to buildMultiTargeting [#580](https://github.com/Microsoft/vstest/pull/580)
* Moving to Netcoreapp 2.0 [#603](https://github.com/Microsoft/vstest/pull/603)
* Create config file for test project targeting .NET Framework [#642](https://github.com/Microsoft/vstest/pull/642)
* Create new RuntimeProvider to be associated with each ProxyOperationManager [#653](https://github.com/Microsoft/vstest/pull/653)
* Inject entry point only for project targeting netcoreapp [#665](https://github.com/Microsoft/vstest/pull/665)
* Dotnet test output coloring [#641](https://github.com/Microsoft/vstest/pull/641)
* Remove binding redirect of Newtonsoft.Json from testhost config file [#663](https://github.com/Microsoft/vstest/pull/663)
* Resolve testhost from source directory if we couldnt resolve it via nuget cache [#690](https://github.com/Microsoft/vstest/pull/690)
* Improve testplatform message [#691](https://github.com/Microsoft/vstest/pull/691)
* Protocol v2 improvements [#672](https://github.com/Microsoft/vstest/pull/672), [#698](https://github.com/Microsoft/vstest/pull/698)
* Use "dotnet test --verbosity" arg for console verbosity [#735](https://github.com/Microsoft/vstest/pull/735)

A list of all changes since last release are available [here](https://github.com/Microsoft/vstest/compare/v15.0.0...v15.3.0-preview-20170425-07).

### Drops

* TestPlatform vsix: [15.3.0-preview-20170425-07](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20170425-07;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [15.3.0-preview-20170425-07](http://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.3.0-preview-20170425-07)

## 15.0.0-preview-20170125-04

* Localization for following nuget packages:
 1) Microsoft.TestPlatform.CLI
 2) Microsoft.TestPlatform
 3) Microsoft.TestPlatform.ObjectModel
 4) Microsoft.TestPlatform.TestHost

A list of all changes since last release are available [here](https://github.com/Microsoft/vstest/compare/v15.0.0-preview-20170123-02...15.0.0-preview-20170125-04).

### Drops

* Microsoft.TestPlatform.ObjectModel: [15.0.0-preview-20170125-04](https://dotnet.myget.org/feed/vstest/package/nuget/Microsoft.TestPlatform.ObjectModel/15.0.0-preview-20170125-04)
* Microsoft.TestPlatform.TranslationLayer: [15.0.0-preview-20170125-04](https://dotnet.myget.org/feed/vstest/package/nuget/Microsoft.TestPlatform.TranslationLayer/15.0.0-preview-20170125-04)

## 15.0.0-preview-20170123.02

* Allow multiple test properties with same key [#239](https://github.com/Microsoft/vstest/issues/239), [#358](https://github.com/Microsoft/vstest/issues/358)
* Localization for testplatform vsix package [#146](https://github.com/Microsoft/vstest/issues/146)
* Working directory should be set to test source parent directory [#311](https://github.com/Microsoft/vstest/issues/311)
* Allow relative source paths to vstest.console [#331](https://github.com/Microsoft/vstest/issues/331)
* Stacktrace and error message should be in context of failed test [#285](https://github.com/Microsoft/vstest/issues/285)

A list of all changes since last release are available [here](https://github.com/Microsoft/vstest/compare/RC.3...15.0-rtm).

### Drops

* TestPlatform vsix: [TestPlatform.CI.Real-20170123-02](https://devdiv.visualstudio.com/DevDiv/_build/index?buildId=533598&_a=summary)
* Microsoft.TestPlatform.ObjectModel: [15.0.0-preview-20170123-02](https://dotnet.myget.org/feed/vstest/package/nuget/Microsoft.TestPlatform.ObjectModel/15.0.0-preview-20170123-02)
* Microsoft.TestPlatform.TranslationLayer: [15.0.0-preview-20170123-02](https://dotnet.myget.org/feed/vstest/package/nuget/Microsoft.TestPlatform.TranslationLayer/15.0.0-preview-20170123-02)

## 15.0.0-preview-20170106.08

* First Draft for the Protocol tool. [#306](https://github.com/Microsoft/vstest/pull/306)
* Fixed DiaSession issue which showed async methods to be `external` [#307](https://github.com/Microsoft/vstest/pull/307)
* Localized vstest [#308](https://github.com/Microsoft/vstest/pull/308)
* Added OutputType to Microsoft.NET.Test.Sdk.target [#310](https://github.com/Microsoft/vstest/pull/310)
* Enclosed run settings arguments to handle whitespace [#312](https://github.com/Microsoft/vstest/pull/312)
* Converted TestPlatform.vsix from V2 to V3 format [#316](https://github.com/Microsoft/vstest/pull/316)

A list of all changes since last release are available [here](https://github.com/Microsoft/vstest/compare/v15.0.0-preview-20161227-02...v15.0.0-preview-20170106-08).

### Drops

* TestPlatform vsix: [TestPlatform.CI.Real-20170106-08](https://devdiv.visualstudio.com/DevDiv/VS.in%20Agile%20Testing%20IDE/_build/index?buildId=505945&_a=summary&tab=artifacts)
* Microsoft.TestPlatform.ObjectModel: [15.0.0-preview-20170106-08](https://dotnet.myget.org/feed/vstest/package/nuget/Microsoft.TestPlatform.ObjectModel/15.0.0-preview-20170106-08)
* Microsoft.TestPlatform.TranslationLayer: [15.0.0-preview-20170106-08](https://dotnet.myget.org/feed/vstest/package/nuget/Microsoft.TestPlatform.TranslationLayer/15.0.0-preview-20170106-08)

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
