# Release Notes

## 16.7.0-preview-20200428-01

### Issue Fixed
* Update telemetry to latest [#2421](https://github.com/microsoft/vstest/pull/2421)
* Merge test run parameters that have spaces [#2409](https://github.com/microsoft/vstest/pull/2409)
* updated package version [#2412](https://github.com/microsoft/vstest/pull/2412)
* update externals [#2406](https://github.com/microsoft/vstest/pull/2406)
* VS Depencencies from 16.7.0 signed build [#2382](https://github.com/microsoft/vstest/pull/2382)
* Changed new configurator method name (#2397) [#2403](https://github.com/microsoft/vstest/pull/2403)
* Fix null reference [#2401](https://github.com/microsoft/vstest/pull/2401)
* Fix null reference [#2400](https://github.com/microsoft/vstest/pull/2400)
* Changed new configurator method name [#2398](https://github.com/microsoft/vstest/pull/2398)
* Changed new configurator method name [#2397](https://github.com/microsoft/vstest/pull/2397)

See full log [here](https://github.com/microsoft/vstest/compare/v16.6.1...v16.7.0-preview-20200428-01)

### Drops

* TestPlatform vsix: [16.7.0-preview-20200428-01](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/master/20200428-01;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.7.0-preview-20200428-01](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.7.0-preview-20200428-01)

## 16.6.1

### Issue Fixed

* Fix fakes version [#2412](https://github.com/microsoft/vstest/pull/2412)

See full log [here](https://github.com/microsoft/vstest/compare/v16.6.0...v16.6.1)

### Drops

* TestPlatform vsix: [16.6.1](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/16.6/20200423-06;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.6.1](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.6.1)

## 16.6.0

### Issue Fixed
* Fix null reference in Fakes [#2400](https://github.com/microsoft/vstest/pull/2400)
* Changed new configurator method name [#2397](https://github.com/microsoft/vstest/pull/2397)
* Fixes Test Platform. [#2393](https://github.com/microsoft/vstest/pull/2393)
* Fixing a typo for the method arguments for the Fakes utility method. [#2385](https://github.com/microsoft/vstest/pull/2385)
* Ignore flaky test [#2386](https://github.com/microsoft/vstest/pull/2386)
* LOC CHECKIN | Microsoft/vstest master | 20200403 [#2383](https://github.com/microsoft/vstest/pull/2383)
* Upgrade CppUnitTestFramework to newest version [#2381](https://github.com/microsoft/vstest/pull/2381)
* Added method to look for new api in fakes datacollector [#2339](https://github.com/microsoft/vstest/pull/2339)
* Take TestCaseFilter from runsettings [#2356](https://github.com/microsoft/vstest/pull/2356)
* Pin dotnet [#2373](https://github.com/microsoft/vstest/pull/2373)
* Fix writing to trx when error has no message [#2364](https://github.com/microsoft/vstest/pull/2364)
* Fix symbols [#2363](https://github.com/microsoft/vstest/pull/2363)
* Report informational messages when platform logs are enabled [#2361](https://github.com/microsoft/vstest/pull/2361)
* Add option to specify custom test host [#2359](https://github.com/microsoft/vstest/pull/2359)
* Fix running self-contained apps on Windows [#2358](https://github.com/microsoft/vstest/pull/2358)
* Remove unused usings. [#2350](https://github.com/microsoft/vstest/pull/2350)
* Better error when discoverer defaultExecutorUri is not set. [#2354](https://github.com/microsoft/vstest/pull/2354)
* Add coverlet smoke test [#2348](https://github.com/microsoft/vstest/pull/2348)
* Fix splitting of test name from fully qualified name [#2355](https://github.com/microsoft/vstest/pull/2355)
* Spelling / conventions and grammar fixes [#2338](https://github.com/microsoft/vstest/pull/2338)
* Small build fixes [#2345](https://github.com/microsoft/vstest/pull/2345)
* Fix race condition on testhost exit before we connect [#2344](https://github.com/microsoft/vstest/pull/2344)
* Move test publish to the bottom [#2342](https://github.com/microsoft/vstest/pull/2342)
* Do not crash on Debug.Assert [#2335](https://github.com/microsoft/vstest/pull/2335)
* Switch arguments for expected and actual in Assert.AreEquals in multiple tests [#2329](https://github.com/microsoft/vstest/pull/2329)
* Run acceptance tests against the locally built sources [#2340](https://github.com/microsoft/vstest/pull/2340)

See full log [here](https://github.com/microsoft/vstest/compare/v16.5.0...v16.6.0)

### Drops

* TestPlatform vsix: [16.6.0](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/16.6/20200414-04;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.6.0](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.6.0)

## 16.6.0-preview-20200318-01

### Issue Fixed
* Fix writing to trx when error has no message [#2364](https://github.com/microsoft/vstest/pull/2364)
* Fix symbols [#2363](https://github.com/microsoft/vstest/pull/2363)
* Report informational messages when platform logs are enabled [#2361](https://github.com/microsoft/vstest/pull/2361)
* Add option to specify custom test host [#2359](https://github.com/microsoft/vstest/pull/2359)

See full log [here](https://github.com/microsoft/vstest/compare/v16.6.0-preview-20200310-03...v16.6.0-preview-20200318-01)

### Drops

* TestPlatform vsix: [16.6.0-preview-20200318-01](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/master/20200318-01;/TestPlatform.vsix)        
* Microsoft.TestPlatform.ObjectModel : [16.6.0-preview-20200318-01](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.6.0-preview-20200318-01)

## 16.6.0-preview-20200310-03

### Issue Fixed
* Fix running self-contained apps on Windows [#2358](https://github.com/microsoft/vstest/pull/2358)
* Remove unused usings. [#2350](https://github.com/microsoft/vstest/pull/2350)
* Better error when discoverer defaultExecutorUri is not set. [#2354](https://github.com/microsoft/vstest/pull/2354)

See full log [here](https://github.com/microsoft/vstest/compare/v16.6.0-preview-20200309-01...v16.6.0-preview-20200310-03)

### Drops

* TestPlatform vsix: [16.6.0-preview-20200310-03](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/master/20200310-03;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.6.0-preview-20200310-03](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.6.0-preview-20200310-03)

## 16.6.0-preview-20200309-01

### Issue Fixed
* Add coverlet smoke test [#2348](https://github.com/microsoft/vstest/pull/2348)
* Fix splitting of test name from fully qualified name [#2355](https://github.com/microsoft/vstest/pull/2355)

See full log [here](https://github.com/microsoft/vstest/compare/v16.6.0-preview-20200226-03...v16.6.0-preview-20200309-01)

### Drops

* TestPlatform vsix: [16.6.0-preview-20200309-01](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/master/20200309-01;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.6.0-preview-20200309-01](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.6.0-preview-20200309-01)

## 16.6.0-preview-20200226-03

### Issue Fixed
* Spelling / conventions and grammar fixes [#2338](https://github.com/microsoft/vstest/pull/2338)
* Small build fixes [#2345](https://github.com/microsoft/vstest/pull/2345)
* Fix race condition on testhost exit before we connect [#2344](https://github.com/microsoft/vstest/pull/2344)
* Move test publish to the bottom [#2342](https://github.com/microsoft/vstest/pull/2342)
* Do not crash on Debug.Assert [#2335](https://github.com/microsoft/vstest/pull/2335)
* Switch arguments for expected and actual in Assert.AreEquals in multiple tests [#2329](https://github.com/microsoft/vstest/pull/2329)
* Run acceptance tests against the locally built sources [#2340](https://github.com/microsoft/vstest/pull/2340)

See full log [here](https://github.com/microsoft/vstest/compare/v16.5.0-preview-20200203-01...v16.6.0-preview-20200226-03)

### Drops

* TestPlatform vsix: [16.6.0-preview-20200226-03](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/master/20200226-03;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.6.0-preview-20200226-03](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.6.0-preview-20200226-03)

## 16.5.0

### Issues fixed (since 16.4.0)

* Use version of external package with fixes [#2315](https://github.com/microsoft/vstest/pull/2315)
* Use latest version of VS that is available [#2314](https://github.com/microsoft/vstest/pull/2314)
* Pass coverlet codebase in runsettings for inproc data collector initialization [#2288](https://github.com/microsoft/vstest/pull/2288)
* Make --verbosity case insensitive [#2300](https://github.com/microsoft/vstest/pull/2300)
* Revert "Use patched version of TestPlatform.Extensions (#2283)" [#2307](https://github.com/microsoft/vstest/pull/2307)
* Update arcade [#2302](https://github.com/microsoft/vstest/pull/2302)
* Fix SocketCommunicationManager [#2290](https://github.com/microsoft/vstest/pull/2290)
* Use patched version of TestPlatform.Extensions [#2283](https://github.com/microsoft/vstest/pull/2283)
* Cap version of VS to <16.0 [#2285](https://github.com/microsoft/vstest/pull/2285)
* Remove duplicate counting of test results in Consolelogger [#2267](https://github.com/microsoft/vstest/pull/2267)
* Test run parameter added as part of CLI runsettings args [#2251](https://github.com/microsoft/vstest/pull/2251)
* Initialize only coverlet data collector [#2274](https://github.com/microsoft/vstest/pull/2274)
* Use RunSettingsFilePath from when using dotnet test [#2272](https://github.com/microsoft/vstest/pull/2272)
* Eqt trace error was thrown if extension uri is not given [#2264](https://github.com/microsoft/vstest/pull/2264)
* Fix for discovery not working on Mac machines [#2266](https://github.com/microsoft/vstest/pull/2266)
* Disable reusing nodes when building localization [#2268](https://github.com/microsoft/vstest/pull/2268)
* Trx changes for fqdn mapping in test method name [#2259](https://github.com/microsoft/vstest/pull/2259)
* Expand environment variables in codeBase before loading extension [#1871](https://github.com/microsoft/vstest/pull/1871)
* Coverlet in-process collector is not loaded for version > 1.0.0 [#2221](https://github.com/microsoft/vstest/pull/2221)
* fix path in ngen [#2246](https://github.com/microsoft/vstest/pull/2246)
* LOC CHECKIN | Microsoft/vstest master | 20191104 [#2241](https://github.com/microsoft/vstest/pull/2241)
* Move Tp version to 16.5 [#2243](https://github.com/microsoft/vstest/pull/2243)
* Add support for an arg to enable progress indicator, disabled by default. [#2234](https://github.com/microsoft/vstest/pull/2234)
* Correct name and link for RFC 17 [#2232](https://github.com/microsoft/vstest/pull/2232)

See full log [here](https://github.com/microsoft/vstest/compare/v16.4.0...v16.5.0)
See changes since the last preview [here](https://github.com/microsoft/vstest/compare/16.5.0-preview-20200203-01...v16.5.0)

### Drops

* TestPlatform vsix: [16.5.0](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/master/20200205-01;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.5.0](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.5.0)

## 16.5.0-preview-20200203-01

### Issue Fixed
* Use version of external package with fixes [#2315](https://github.com/microsoft/vstest/pull/2315)
* Use latest version of VS that is available [#2314](https://github.com/microsoft/vstest/pull/2314)
* Pass coverlet codebase in runsettings for inproc data collector initialization [#2288](https://github.com/microsoft/vstest/pull/2288)
* Make --verbosity case insensitive [#2300](https://github.com/microsoft/vstest/pull/2300)

See full log [here](https://github.com/microsoft/vstest/compare/v16.5.0-preview-20200116-01...v16.5.0-preview-20200203-01)

### Drops

* TestPlatform vsix: [16.5.0-preview-20200203-01](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/master/20200203-01;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.5.0-preview-20200203-01](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.5.0-preview-20200203-01)  

## 16.5.0-preview-20200116-01

### Issue Fixed 
* Revert "Use patched version of TestPlatform.Extensions (#2283)" [#2307](https://github.com/microsoft/vstest/pull/2307)
* Update arcade [#2302](https://github.com/microsoft/vstest/pull/2302)
* Fix SocketCommunicationManager [#2290](https://github.com/microsoft/vstest/pull/2290)

See full log [here](https://github.com/Microsoft/vstest/compare/v16.5.0-preview-20200110-02...v16.5.0-preview-20200116-01)

### Drops

* TestPlatform vsix: [16.5.0-preview-20200116-01](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/master/20200116-01;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.5.0-preview-20200116-01](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.5.0-preview-20200116-01)

## 16.5.0-preview-20200110-02

### Issue Fixed 
* Remove duplicate counting of test results in Consolelogger [#2267](https://github.com/microsoft/vstest/pull/2267) 
* Cap version of VS to <16.0 [#2285](https://github.com/microsoft/vstest/pull/2285)
* Use patched version of TestPlatform.Extensions [#2283](https://github.com/microsoft/vstest/pull/2283)

See full log [here](https://github.com/Microsoft/vstest/compare/v16.5.0-preview-20200102-01...v16.5.0-preview-20200110-02)

### Drops

* TestPlatform vsix: [16.5.0-preview-20200110-02](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/master/20200110-02;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.5.0-preview-20200110-02](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.5.0-preview-20200110-02)

## 16.5.0-preview-20200102-01

### Issue Fixed
* Test run parameter added as part of CLI runsettings args [#2251](https://github.com/microsoft/vstest/pull/2251)

### Drops

* TestPlatform vsix: [16.5.0-preview-20200102-01](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/master/20200102-01;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.5.0-preview-20200102-01](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.5.0-preview-20200102-01)

## 16.5.0-preview-20191216-02

### Issue Fixed
* Trx changes for fqdn mapping in test method name [#2259](https://github.com/microsoft/vstest/pull/2259)
* Fix for test discovery not working on mac machines [#2266](https://github.com/microsoft/vstest/pull/2266)
* Use RunSettingsFilePath from project file when using dotnet test [#2272](https://github.com/microsoft/vstest/pull/2272)

### Drops

* TestPlatform vsix: [16.5.0-preview-20191216-02](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/master/20191216-02;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.5.0-preview-20191216-02](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.5.0-preview-20191216-02)

## 16.5.0-preview-20191115-01

### Issue Fixed
* Fixed Coverlet in-process collector not loaded for version > 1.0.0 [#2204](https://github.com/microsoft/vstest/pull/2221)

### Drops

* TestPlatform vsix: [16.5.0-preview-20191115-01](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/master/20191115-01;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.5.0-preview-20191115-01](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.5.0-preview-20191115-01)

## 16.4.0

### Issue Fixed
* Adding log prefixkey to html logger [#2204](https://github.com/microsoft/vstest/pull/2204)
* AnyCPU tests to choose default architecture based on process [#2206](https://github.com/microsoft/vstest/pull/2206)
* Only send Coverlet in proc datacollector dll to testhost [#2226](https://github.com/microsoft/vstest/pull/2226)
* Missing Cancel Implementation [#2227](https://github.com/microsoft/vstest/pull/2227)

### Drops

* TestPlatform vsix: [16.4.0](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/master/20191025-01;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.4.0](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.4.0)

##  16.4.0-preview-20191007-01

### Issues Fixed / Features Added

* Redirect procdump process output to diag files [#2181](https://github.com/microsoft/vstest/pull/2181)
* Implemented cancellation of individual source files discovery [#2134](https://github.com/microsoft/vstest/pull/2134)
* Enabling native code debugging of test host [#2190](https://github.com/microsoft/vstest/pull/2190)
* Logging Adapter Load issues to console [#2156](https://github.com/microsoft/vstest/pull/2156)
* Fixed DataCollector to load with only uri (and not friendly name) specified in Runsettings [#2177](https://github.com/microsoft/vstest/pull/2177)
* Added env var support to blame test results directory path and fixed blame aborting without killing the test host process on hang timeout when there is an error with dump collection/attachment [#2216](https://github.com/microsoft/vstest/pull/2216)

## 16.3.0

### Issue Fixed
* Html logger [#2103](https://github.com/microsoft/vstest/pull/2103)
* Add LogFilePrefix Parameter for supporting trx for multi-targetted projects [#2140](https://github.com/microsoft/vstest/pull/2140)
* Support x86 platform targeting for .NET core tests [#2161](https://github.com/microsoft/vstest/pull/2161)
* Add logging for Translation layer [#2166](https://github.com/microsoft/vstest/pull/2166)

### Drops

* TestPlatform vsix: [16.3.0](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/master/20190919-02;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.3.0](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.3.0)


## 16.3.0-preview-20190828-03

### Issue Fixed
* Add noprogress parameter to disable progress indicator [#2117](https://github.com/microsoft/vstest/pull/2117)
* Accept short names for framewwork [#2116](https://github.com/microsoft/vstest/pull/2116)
* Specifying environment variables in RunSettings file [#2128](https://github.com/microsoft/vstest/pull/2128)
* VsTestConsoleWrapper endsession should shut down vstest console process [#2145](https://github.com/microsoft/vstest/pull/2145)

### Drops

* TestPlatform vsix: [16.3.0-preview-20190828-03](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/master/20190828-03;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.3.0-preview-20190828-03](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.3.0-preview-20190828-03)


## 16.3.0-preview-20190715-02

### Issue Fixed
* TestPlatform targeting netstandard2.0. [#2076](https://github.com/microsoft/vstest/pull/2076)
* Implemented the cancellation of discovery request [#2076](https://github.com/microsoft/vstest/pull/2076)
* Generating manifest for publishing to BAR. [#2069](https://github.com/microsoft/vstest/pull/2069)

### Drops

* TestPlatform vsix: [16.3.0-preview-20190715-02](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/master/20190715-02;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.3.0-preview-20190715-02](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.3.0-preview-20190715-02)

## 16.2.0

### Issue Fixed
* Updated TestPlatform.ObjectModel.nuspec. [#2055](https://github.com/microsoft/vstest/pull/2055)
* Fixed incorrect timeout message when test host crashes [#2056](https://github.com/microsoft/vstest/pull/2056)
* Incompatible framework message fix. [#2044](https://github.com/microsoft/vstest/pull/2044)
* Cleaned up remaining set of dependencies for source build. [#2058](https://github.com/microsoft/vstest/pull/2058)

### Drops

* TestPlatform vsix: [16.2.0](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/microsoft/vstest/master/20190626-03;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.2.0](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.2.0)

## 16.2.0-preview-20190606-02

### Issue Fixed
* Spurious vstest.console process spin up fixed. [#2035](https://github.com/microsoft/vstest/pull/2035)
* Test host locking pdb fixed [#2029](https://github.com/microsoft/vstest/pull/2029)
* Encoding change from UCS-2 to UTF-8. [#2044](https://github.com/microsoft/vstest/pull/2044)
* Unable to find Microsoft.VisualStudio.ArchitectureTools.PEReader fixed. [#2008](https://github.com/microsoft/vstest/pull/2008)

### Drops

* TestPlatform vsix: [16.2.0-preview-20190606-02](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20190606-02;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.2.0-preview-20190606-02](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.2.0-preview-20190606-02)

## 16.1.1

### Issue Fixed
* Prevent unnecessary progress indicator refresh to improve test run time. [#2024](https://github.com/microsoft/vstest/pull/2024)
* Changes to allow clients to provide environment variable while initializing VsTestConsoleWrapper [#2023](https://github.com/microsoft/vstest/pull/2023)
* Fix for the trx classname being wrongly stamped when testname and fullyqualifiedname are same. [#2014](https://github.com/microsoft/vstest/pull/2014)
* Search datacollectors in output directory as well. [#2015](https://github.com/microsoft/vstest/pull/2015)
* Changes to avoid restoring of packages that are not required for the BuildFromSource scenario. [#2017](https://github.com/microsoft/vstest/pull/2017)

### Drops

* TestPlatform vsix: [16.1.1](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20190529-04;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.1.1](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.1.1)

## 16.0.2-Preview-20190502-01

### Issue Fixed
* Improve the cli experience for dotnet test. [#1964](https://github.com/Microsoft/vstest/pull/1964)
* Improve readability of dotnet test [#1960](https://github.com/Microsoft/vstest/pull/1960)
* Make testhost.x86 large address aware [#1986](https://github.com/Microsoft/vstest/pull/1986)
* Vstest.console Should not message to Testhost process if it has exited [#1994](https://github.com/Microsoft/vstest/pull/1994)
* [Revert] Fix for dotnet test on a multi-target projects logs only the last target [#1996](https://github.com/Microsoft/vstest/pull/1996)
* [Trxlogger] Fixing the code to preserve newline for adapter logs to stdout [#1999](https://github.com/Microsoft/vstest/pull/1999)

### Drops

* TestPlatform vsix: [16.0.2-preview-20190502-01](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20190502-01;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.0.2-preview-20190502-01](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.0.2-preview-20190502-01)

## 16.0.1

### Issue Fixed
* Reverted aborting test run when source and target frameworks/architectures are incompatible. [#1935](https://github.com/Microsoft/vstest/pull/1935)

### Drops

* TestPlatform vsix: [16.0.1](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20190304-05;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.0.1](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.0.1)

## 16.0.0

### Issue Fixed
* Added missing Utilities dependency to netstandard1.5 [#1913](https://github.com/Microsoft/vstest/pull/1913)
* Add support for xplat vstest console in translationlayer [#1893](https://github.com/Microsoft/vstest/pull/1893)
* Aborting test run when source and target frameworks/architectures are incompatible. [#1789](https://github.com/Microsoft/vstest/pull/1789)

### Drops

* TestPlatform vsix: [16.0.0](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20190228-02;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.0.0](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.0.0)

## 16.0.0-preview-20190201-03

### Issue Fixed
* Running NETFramework 3.5 tests in compat mode [#1906](https://github.com/Microsoft/vstest/pull/1906)
* Make timeouts for translation layer timeout configurable. [#1909](https://github.com/Microsoft/vstest/pull/1909)

### Drops

* TestPlatform vsix: [16.0.0-preview-20190201-03](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20190201-03;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.0.0-preview-20190201-03](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.0.0-preview-20190201-03)


## 16.0.0-preview-20190124-02

### Issue Fixed
* Downgrade Test.Sdk to net40 [#1860](https://github.com/Microsoft/vstest/pull/1860)
* Fix xml exception when we are dealing with special chars [#1872](https://github.com/Microsoft/vstest/pull/1872)
* Fix - dotnet test on a multi-target projects logs only the last target [#1877](https://github.com/Microsoft/vstest/pull/1877)
* Avoid usage of JsonConvert in test host process [#1881](https://github.com/Microsoft/vstest/pull/1881)
* Fixing logging error in event sources [#1897](https://github.com/Microsoft/vstest/pull/1897)

### Drops

* TestPlatform vsix: [16.0.0-preview-20190124-02](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20190124-02;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.0.0-preview-20190124-02](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.0.0-preview-20190124-02)


## 16.0.0-preview-20181205-02

### Issue Fixed
* Stop trying to connect if the test host exits unexpectedly [#1853](https://github.com/Microsoft/vstest/pull/1853)
* Move warning into a target to fix msbuild error [#1856](https://github.com/Microsoft/vstest/pull/1856)
* Adding the missing assemblyInfo files and updating the copyrights [#1859](https://github.com/Microsoft/vstest/pull/1859)

### Drops

* TestPlatform vsix: [16.0.0-preview-20181205-02](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20181205-02;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.0.0-preview-20181205-02](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.0.0-preview-20181205-02)


## 16.0.0-preview-20181128-01

### Issue Fixed
* Allow external use of the TRX Logger [#1792](https://github.com/Microsoft/vstest/pull/1792)
* Add "!~" operator to test filter [#1803](https://github.com/Microsoft/vstest/pull/1803)
* Simplify SDK languages support [#1804](https://github.com/Microsoft/vstest/pull/1804)
* Make Translation Layer connection timeout configurable [#1843](https://github.com/Microsoft/vstest/pull/1843)
* Fixed issue where proc dump was not getting terminated on no crash [#1849](https://github.com/Microsoft/vstest/pull/1849)

### Drops

* TestPlatform vsix: [16.0.0-preview-20181128-01](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20181128-01;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [16.0.0-preview-20181128-01](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/16.0.0-preview-20181128-01)


## 15.9.0

### Issue Fixed
* Unstable testId for nunit tests [#1785](https://github.com/Microsoft/vstest/pull/1785)
* Run tests only for test projects [#1745](https://github.com/Microsoft/vstest/pull/1745)
* Add info log if try to run tests with no IsTestProject prop [#1778](https://github.com/Microsoft/vstest/pull/1778)

### Drops

* TestPlatform vsix: [15.9.0](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/15.9/20181008-02;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [15.9.0](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.9.0)


## 15.9.0-preview-20180924-03

### Issue Fixed
* Fix Video Datacollector errors [#1719](https://github.com/Microsoft/vstest/pull/1719)
* Show error message on Framework35 [#1723](https://github.com/Microsoft/vstest/pull/1723)
* Suggest publish for running on an isolated machine[#1726](https://github.com/Microsoft/vstest/pull/1726)
* Fix UWP tests app socket exception [#1728](https://github.com/Microsoft/vstest/pull/1728)
* Run tests only for test projects in "dotnet test my.sln" scenario [#1745](https://github.com/Microsoft/vstest/pull/1745)


### Drops

* TestPlatform vsix: [15.9.0-preview-20180924-03](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20180924-03;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [15.9.0-preview-20180924-03](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.9.0-preview-20180924-03)


## 15.9.0-preview-20180807-05
	
### Issue Fixed
* Fix for VSTest to honor /nologo user input from dotnet cli [#1717](https://github.com/Microsoft/vstest/pull/1717)
* Fixed ISettingsProvider in TestAdapter assembly [#1704](https://github.com/Microsoft/vstest/pull/1704)
* Added `.NETCoreApp,Version=v2.0` example in error message [#1714](https://github.com/Microsoft/vstest/pull/1714)
* Print start of testhost standard error stacktrace [#1708](https://github.com/Microsoft/vstest/pull/1708)
* Use of culture specified by user in case it differs with that of OS [#1712](https://github.com/Microsoft/vstest/pull/1712)
* Added attributes for sequence file generated by blame [#1716](https://github.com/Microsoft/vstest/pull/1716)
* Trx Logger class name fix for Nunit Data Driven tests [#1677](https://github.com/Microsoft/vstest/pull/1677) 
* Trx Logger Fixed to generate trx file when test run aborts [#1710](https://github.com/Microsoft/vstest/pull/1710)
* Added trace level for diag argument [#1681](https://github.com/Microsoft/vstest/pull/1681)
	
### New Features introduced
* Enhancing Blame data collector options to include DumpType and AlwaysCollectDump [#1682](https://github.com/Microsoft/vstest/pull/1682)
* Procdump arguments enhanced to handle crash scenarios [#1700](https://github.com/Microsoft/vstest/pull/1700)
	
### Drops
* TestPlatform vsix: [15.9.0-preview-20180807-05](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20180807-05;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel : [15.9.0-preview-20180807-05](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.9.0-preview-20180807-05)

## 15.8.0

### Issue Fixed
* Fix vstest.console.exe grabs exclusive read access to its test container [#1660](https://github.com/Microsoft/vstest/pull/1660)
* Registring correct property attributes during deserialization [#1644](https://github.com/Microsoft/vstest/pull/1644)
* Fixed test platform messages on cancellation request [#1667](https://github.com/Microsoft/vstest/pull/1667)
* Fixed warning messages for scenario when no tests are found matching TestCaseFilter [#1656](https://github.com/Microsoft/vstest/pull/1656)
* Fixed UWP VC++ unit tests not executing [#1649](https://github.com/Microsoft/vstest/pull/1649)
* Handling null value deserialization in TestCategory [#1640](https://github.com/Microsoft/vstest/pull/1640)

### New Features introduced
* Auto-generate F# program file. [#1664](https://github.com/Microsoft/vstest/pull/1664)
* Added support for dotnet test --collect:"Code Coverage" (windows only) [#981](https://github.com/Microsoft/vstest/issues/981)

### Drops

* TestPlatform vsix: [15.8.0](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20180710-03;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [15.8.0](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.8.0)

## 15.8.0-preview-20180610-02

### New Features introduced
* Collect Code coverage with dotnet core sdk on windows. [#981](https://github.com/Microsoft/vstest/issues/981)

### Drops

* TestPlatform vsix: [15.8.0-preview-20180610-02](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20180610-02;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [15.8.0-preview-20180610-02](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.8.0-preview-20180610-02)

## 15.8.0-preview-20180605-02

### Issue Fixed
* Fix Exception thrown while creating framework based on default enums. [#1598](https://github.com/Microsoft/vstest/pull/1598)
* Deprecate Testplatform\Extensions path for Adapters [#1602](https://github.com/Microsoft/vstest/pull/1602)
* Update Test Source with Package for Inprogress Tests [#1605](https://github.com/Microsoft/vstest/pull/1605)
* Use DateTime.UtcNow instead of DateTime.Now for consistency across test reporting data [#1612](https://github.com/Microsoft/vstest/pull/1612)
* Fixed RecordResult to SendTestCaseEnd if not already for datacollectors to end and get attachments correctly [#1615](https://github.com/Microsoft/vstest/pull/1615)
* Fix attachment uri in trx if same attachment filename is same [#1625](https://github.com/Microsoft/vstest/pull/1625)
* Add support to escape/unescape testcase filter strings [#1627](https://github.com/Microsoft/vstest/pull/1627)

### New Features introduced
* Add a tool to migrate testsettings to runsettings [#1600](https://github.com/Microsoft/vstest/pull/1600)

### Drops

* TestPlatform vsix: [15.8.0-preview-20180605-02](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20180605-02;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [15.8.0-preview-20180605-02](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.8.0-preview-20180605-02)

## 15.8.0-preview-20180510-03

### Issue Fixed
* Extend FastFilter to support multiple properties. [#1523](https://github.com/Microsoft/vstest/pull/1523)
* Make all communication timeouts configurable. [#1538](https://github.com/Microsoft/vstest/pull/1538)
* Honoring cancel and abort request in test platform. [#1543](https://github.com/Microsoft/vstest/pull/1543)
* FilterOptions serialization issue when running .NET core tests. [#1551](https://github.com/Microsoft/vstest/pull/1551)
* Telemetry points for legacy settings. [#1564](https://github.com/Microsoft/vstest/pull/1564)
* Flushing test results even if RecordEnd is not called. [#1573](https://github.com/Microsoft/vstest/pull/1573)
* Searching adapters in Test Source directory in all scenarios. [#1574](https://github.com/Microsoft/vstest/pull/1574)
* Filtering non existent adapter paths. [#1578](https://github.com/Microsoft/vstest/pull/1578)

### New Features introduced
* Introduced category attribtue for adapter to specify supported assembly type.[#1528](https://github.com/Microsoft/vstest/pull/1528), [#1529](https://github.com/Microsoft/vstest/pull/1529), [#1537](https://github.com/Microsoft/vstest/pull/1537)

### Drops

* TestPlatform vsix: [15.8.0-preview-20180510-03](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20180510-03;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [15.8.0-preview-20180510-03](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.8.0-preview-20180510-03)

## 15.7.2

### Issue Fixed
* Code coverage fix for async functions. [242314](https://developercommunity.visualstudio.com/content/problem/242314/code-coverage-doesnt-show-async-methods.html)

### Drops

* TestPlatform vsix: [15.7.2]( https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/15.7/20180514-03;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [15.7.2](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.7.2)

## 15.7.0

### Issue Fixed
* Code coverage fix for runsettings. [#1510](https://github.com/Microsoft/vstest/pull/1510)
* Logging fix for UWP.[#1508](https://github.com/Microsoft/vstest/pull/1508)
* Perf improvements for LUT [#1517](https://github.com/Microsoft/vstest/pull/1517)
* Fix for preserving CR LF line endings in TRX file. [#1521](https://github.com/Microsoft/vstest/pull/1521)
* Fix socket exception on datacollection in parallel. [#1514](https://github.com/Microsoft/vstest/pull/1514)

### New Features introduced
* Introduced running UWP test using ".appx" file as input, for CLI.

### Drops

* TestPlatform vsix: [15.7.0]( https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/15.7/20180403-02;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [15.7.0](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.7.0)

## 15.7.0-preview-20180320-02

### Issue Fixed
* Fixing the tests for string comparison issue. [#1462](https://github.com/Microsoft/vstest/pull/1462)
* Sync for binarywriter writes.[#1470](https://github.com/Microsoft/vstest/pull/1470)
* Usability Fixes [#1478](https://github.com/Microsoft/vstest/pull/1478)
* Fix for Design mode clients hang for errors [1451](https://github.com/Microsoft/vstest/pull/1451)
* Fix datacollectors temporary files cleanup [1483](https://github.com/Microsoft/vstest/pull/1483)

### Drops

* TestPlatform vsix: [15.7.0-preview-20180320-02](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20180320-02;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [15.7.0-preview-20180320-02](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.7.0-preview-20180320-02)

## 15.7.0-preview-20180307-01

### Issue Fixed
* Fix CUIT tests fail to run on no VS installed machine.  [#1450](https://github.com/Microsoft/vstest/pull/1450)

### Drops

* TestPlatform vsix: [15.7.0-preview-20180307-01](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20180307-01;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [15.7.0-preview-20180307-01](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.7.0-preview-20180307-01)


## 15.7.0-preview-20180221-13

### Issue Fixed
* Adding Category to Test Category mapping for ListFullyQualifiedTests. [#1369](https://github.com/Microsoft/vstest/pull/1369)
* Support escaping "," in Test filter. [#1374](https://github.com/Microsoft/vstest/pull/1374)
* Generate proper default settings for EnableCodeCoverage. [#1390](https://github.com/Microsoft/vstest/pull/1390)
* Test run directory fix for loggers. [#1399](https://github.com/Microsoft/vstest/pull/1399)
* Fixed the normal verbosity level to not log the full information for non-failed tests. [#1396](https://github.com/Microsoft/vstest/pull/1396)
* Ignore case for targetframework input. [#1420](https://github.com/Microsoft/vstest/pull/1420)
* Fixed logger to have additonal lines after std output. [#1421](https://github.com/Microsoft/vstest/pull/1421)
* Fixed the error message. [#1422](https://github.com/Microsoft/vstest/pull/1422)
* Fix: Logger attachments not coming in vsts test run. [#1431](https://github.com/Microsoft/vstest/pull/1431)
* Fixed help test to mention default value of verbosity in console logger. [#1433](https://github.com/Microsoft/vstest/pull/1433)
* Exceptions flow to Translation layer [#1434](https://github.com/Microsoft/vstest/pull/1434)

### New Features introduced
* Logger support in run settings.[#1382](https://github.com/Microsoft/vstest/pull/1382)
* Added CUIT package in vstest xcopy package. [#1394](https://github.com/Microsoft/vstest/pull/1394)
* Making Trx Logger Hierarchical for ordered test and data driven tests. [#1330](https://github.com/Microsoft/vstest/pull/1330)

### Drops

* TestPlatform vsix: [15.7.0-preview-20180221-13](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20180221-13;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [15.7.0-preview-20180221-13](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.7.0-preview-20180221-13)

## 15.6.2

### Issue Fixed
* Fix socket exception on datacollection in parallel  [#1505](https://github.com/Microsoft/vstest/pull/1505)
* Fix datacollectors temporary files cleanup [#1506](https://github.com/Microsoft/vstest/pull/1506)


### Drops

* TestPlatform vsix: [15.6.2](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/15.6/20180326-08;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [v15.6.2](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.6.2)

## 15.6.1

### Issue Fixed
* Synchronize concurrent writes to communication channel  [#1457](https://github.com/Microsoft/vstest/pull/1457)


### Drops

* TestPlatform vsix: [15.6.1](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/15.6/20180307-08;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [v15.6.1](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.6.1)

## 15.6.0

### Issue Fixed
* Fix for Communication b/w testhost, & datacollector fails causing tests processes to hang. [#1406](https://github.com/Microsoft/vstest/pull/1406) 
* Fix for Cancellation hanging TestExplorer with the unclickable cancelling. [#1398](https://github.com/Microsoft/vstest/pull/1398)

### Drops

* TestPlatform vsix: [15.6.0](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/15.6/20180215-04;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [v15.6.0](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.6.0)

## 15.6.0-preview-20180207-05

### Issue Fixed
* Enabling diagnostics for UWP causes app to hang. [#1387](https://github.com/Microsoft/vstest/pull/1387) 

### Drops

* Microsoft.TestPlatform.ObjectModel: [v15.6.0-preview-20180207-05](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.6.0-preview-20180207-05)

## 15.6.0-preview-20180109-01

### Issue Fixed
* Make latest ObjectModel API compatible with ObjectModel 11.0.0. [#1251](https://github.com/Microsoft/vstest/pull/1251/) 
* Fix no error message in case of invalid runsettings. [#1344](https://github.com/Microsoft/vstest/pull/1344)
* Fix CodedUI debug broken. [#1352](https://github.com/Microsoft/vstest/pull/1352)
* Fix debug stop causing 10s or indefinite wait in test explorer.  [#1358](https://github.com/Microsoft/vstest/pull/1358)
* Fix video datacollector assemblies first changes exception while running tests .  [#1362](https://github.com/Microsoft/vstest/pull/1362)
* Fix datacollector initialization failure on slow machines. [#1355](https://github.com/Microsoft/vstest/pull/1355)
* Fix running fakes and code coverage with embedded testsettings in runsettings. [#1364](https://github.com/Microsoft/vstest/pull/1364)

### New Features introduced
* Support reflection based discovery for UWP C++ Unit tests projects.[#1336](https://github.com/Microsoft/vstest/pull/1336)
* Add testhost external dependencies for UWP to Microsoft.NET.Test.Sdk. [#1351](https://github.com/Microsoft/vstest/pull/1351)

### Drops

* TestPlatform vsix: [15.6.0-preview-20180109-01](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20180109-01;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [15.6.0-preview-20180109-01](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.6.0-preview-20180109-01)

## 15.6.0-preview-20171211-02

### Issue Fixed
* Removed warning for AnyCPU assemblies
* Fix updating runsettings in dotnet core.
* Fix exception in Event Log DataCollector. [#1288](https://github.com/Microsoft/vstest/pull/1288)
* Fix support for multiple paths is TestAdapterPath Argument. [#1320](https://github.com/Microsoft/vstest/pull/1320)
* Perf: Using Event based communication over sockets using LengthPrefix communication channel. [1294](https://github.com/Microsoft/vstest/pull/1294)

### Drops

* TestPlatform vsix: [15.6.0-preview-20171211-02](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20171211-02;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [15.6.0-preview-20171211-02](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.6.0-preview-20171211-02)


## 15.5.0

### Issue Fixed
* Removed compile time dependency on castle.core.dll. [#1246](https://github.com/Microsoft/vstest/pull/1246)
* Fix test run for x64 c++ tests. [#1269](https://github.com/Microsoft/vstest/pull/1269)
* Localization fixes for error scenarios. [#1266](https://github.com/Microsoft/vstest/pull/1266)
* Fix for FastFilter issue with TestCaseFilter. [#1252](https://github.com/Microsoft/vstest/pull/1252)
* Updating codecoverage analysis dll's in external package. [#1282](https://github.com/Microsoft/vstest/pull/1282)

### Drops

* TestPlatform vsix: [15.5.0](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/15.5/20171108-03;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [15.5.0](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.5.0)

## 15.5.0-preview-20171031-01

### Issue Fixed
* Add LocalExtensionData property to TestCase Class.
* Do not crash data collector if extension fails to initialize or set environment variables.
* Use TPv2 as default for .NET 3.5 test projects.
* Loading native dll's correctly for UWP release mode.
* Insertion PR: https://github.com/Microsoft/vstest/pull/1250

### Drops

* TestPlatform vsix: [15.5.0-preview-20171031-01](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/15.5/20171031-01;/TestPlatform.vsix)

* Microsoft.TestPlatform.ObjectModel: [15.5.0-preview-20171031-01](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.5.0-preview-20171031-01)

## 15.5.0-preview-20171012-09

### Issue Fixed
* Fixed Data Collector Attachment issues for legacy TMI test execution workflow.
* Added error message and help when vstest.console is invoked without arguments.
* Fixed failure in loading extensions without Identifier Data.
* Handled Test Host close.
* TestCase Display Name is displayed instead of FullyQualifiedName.
* Fixed issues with Static Cover Coverage, Ordered tests through TMI.

### New Features introduced
* Added Telemetry Infra for Design Mode.
* Supported running .Net Framework v35 in compat mode.
* Localization changes.
* Automatically find Platform and Framework if not specified explicitly.
* Adding object model changes and Telemetry optin status.

A list of all changes since last release are available [here](https://github.com/Microsoft/vstest/compare/v15.5.0-preview-20170923-02...v15.5.0-preview-20171012-09).

### Drops

* TestPlatform vsix: [15.5.0-preview-20171012-09](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20171012-09;/TestPlatform.vsix)

* Microsoft.TestPlatform.ObjectModel: [15.5.0-preview-20171012-09](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.5.0-preview-20171012-09)


## 15.5.0-preview-20170923-02

### Issue Fixed
* Feature flag for executing net35 tests through TPv2 in compat mode.
* Removed unnecessary binding redirects from app.configs. [More info here](https://github.com/Microsoft/vstest/pull/1117)
* Put quotes around TestHost path so in case of spaces in name it starts correctly. [More info here](https://github.com/Microsoft/vstest/pull/1108)
* Performance Automation Infra.

### New Features introduced
* Added filter support on test case discovery.
* Added Telemetry Collection Infrastructure.
* Added support for listing fully qualified test cases.
* Exposed discovery events to loggers. 

A list of all changes since last release are available [here](https://github.com/Microsoft/vstest/compare/f8020e56e418f3a14637d401928fd154a061c9c4...v15.5.0-preview-20170923-02).

### Drops

* TestPlatform vsix: [15.5.0-preview-20170923-02](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20170923-02;/TestPlatform.vsix)

* Microsoft.TestPlatform.ObjectModel: [15.5.0-preview-20170923-02](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.5.0-preview-20170923-02)


## 15.5.0-preview-20170914-09

### Issue Fixed
* https://github.com/Microsoft/vstest/issues/979
* https://github.com/Microsoft/vstest/pull/992
* Made TestPlatform.ObjectModel CLS-compliant
* Made Microsoft.CodeCoverage as nuget package dependency for Microsoft.NET.Test.Sdk nuget package. [More info here](https://github.com/Microsoft/vstest/issues/852)
* Perf improvements. [More info here](https://github.com/Microsoft/vstest/pull/1041)
* Fixed issue related to /EnableCodeCoverage. [More info here](https://github.com/Microsoft/vstest/pull/1072)
* https://github.com/Microsoft/vstest/issues/902
* Highest version filtering for extensions. [More info here](https://github.com/Microsoft/vstest/pull/1051)
* https://github.com/Microsoft/vstest/pull/1060


### New Features introduced
* InProc execution of tests inside vstest.console process. [More info here](https://github.com/Microsoft/vstest/pull/1009)
* Added Verbosity Level as prefix for loggers. [More info here](https://github.com/Microsoft/vstest/pull/967)
* Event Log Data Collector. [More info here](https://github.com/Microsoft/vstest-docs/blob/master/docs/analyze.md#event-log-data-collector)
* Introduced /UseVsixExtensions argument in CLI.

A list of all changes since last release are available [here](https://github.com/Microsoft/vstest/compare/v15.5.0-preview-20170810-02...f8020e56e418f3a14637d401928fd154a061c9c4).

### Drops

* TestPlatform vsix: [15.5.0-preview-20170914-09](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20170914-09;/TestPlatform.vsix)

* Microsoft.TestPlatform.ObjectModel: [15.5.0-preview-20170914-09](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.5.0-preview-20170914-09)


## 15.5.0-preview-20170810-02

### Issue Fixed
* https://github.com/Microsoft/vstest/issues/861
* https://github.com/Microsoft/vstest/issues/916
* Made latest testhost compat with older vstest.console and vice versa.
* Some performance improvement

### New Features introduced
* Added blame data collector support in `dotnet test`.
* Add ExecutionThreadApartmentState property in runsettings. [More info here](https://github.com/Microsoft/vstest-docs/blob/master/docs/configure.md#execution-thread-apartment-state)
* Added async APIs support in translationLayer.

A list of all changes since last release are available [here](https://github.com/Microsoft/vstest/compare/73f4a07adfa802257e3ebe11c197016010f2e080...v15.5.0-preview-20170727-01).

### Drops

* TestPlatform vsix: [15.5.0-preview-20170810-02](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20170810-02;/TestPlatform.vsix)

* Microsoft.TestPlatform.ObjectModel: [15.5.0-preview-20170810-02](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.5.0-preview-20170810-02)


## 15.5.0-preview-20170727-01

### Issue Fixed
* Support for devices: build up the TestHostRuntime APIs
* Console test runs will not collect File/LineNumber information
* Several performance improvements
* Reliability improvements to parallel runs
* Engineering fixes to build/test

### New Features introduced
* Blame for vstest. Reports the test which crashes a run
* Response file support for vstest
* `TestSessionTimeout` cancels a test run if it exceeds a timeout
* Mono support for vstest
* VSTest now runs on .NET 4.5.1 runtime

A list of all changes since last release are available [here](https://github.com/Microsoft/vstest/compare/73f4a07adfa802257e3ebe11c197016010f2e080...v15.5.0-preview-20170727-01).

### Drops

* TestPlatform vsix: [15.5.0-preview-20170727-01](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/master/20170727-01;/TestPlatform.vsix)

* Microsoft.TestPlatform.ObjectModel: [15.5.0-preview-20170727-01](http://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.5.0-preview-20170727-01)

## 15.3.0

### Issue Fixed
* Clean testhost before sending discoveryComplete/ExecutionCompltete. 
* Closing VS should also close vstest.console process.


A list of all changes since last release are available [here](https://github.com/Microsoft/vstest/compare/v15.3.0-preview-20170618-03...rel/15.3-rtm).

### Drops

* TestPlatform vsix: [15.3.0](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/15.3-rtm/20170807-05;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [15.3.0](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.3.0)


## 15.3.0-preview-20170618-03

### Issue Fixed
* https://github.com/Microsoft/vstest/issues/632 
* https://github.com/Microsoft/vstest/issues/844 
* https://github.com/Microsoft/vstest/issues/847 
* https://github.com/Microsoft/vstest/issues/840 
* https://github.com/Microsoft/vstest/issues/843


A list of all changes since last release are available [here](https://github.com/Microsoft/vstest/compare/v15.3.0-preview-20170601-03...v15.3.0-preview-20170618-03).

### Drops

* TestPlatform vsix: [15.3.0-preview-20170618-03](https://vsdrop.corp.microsoft.com/file/v1/Products/DevDiv/Microsoft/vstest/15.3-rtm/20170618-03;/TestPlatform.vsix)
* Microsoft.TestPlatform.ObjectModel: [15.3.0-preview-20170618-03](http://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.3.0-preview-20170618-03)


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
