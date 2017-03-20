# Reporting test results
Test discovery, execution results in a test run can be controlled with test
loggers. This document will cover details on installation, usage and authoring
of test loggers.

> Version note: Changes in `15.1` are in draft at this time.

## Test loggers
A test logger is a test platform extension to control reporting of test results.
It can perform tasks when a test run message is generated, individual test
results or the test run completion events are reported by the test platform.

You can author a test logger to print messages on the console, generate result
files of a specific reporting format, or even report results to various CI/CD
services.

Default inputs to a test logger can be provided in the command line, or using
a `runsettings`. For example, you can provide the output path for a generated
test report.

Please refer [todo]() for instructions on creating a test logger and [todo]()
if you're interested in the architecture of a test logger.

### Available test loggers
| Scenario | Nuget Package | Source Repository |
| -------- | ------------- | ----------------- |
| Local, CI, CD | Inbuilt | [Trx Logger][] |
| Local, CI, CD | Inbuilt | [Console Logger][] |
| Local, CI, CD | XunitXml.TestLogger | [Xunit Logger][] |
| AppVeyor | AppVeyor.TestLogger | [AppVeyor Logger][] |
| TeamCity | TeamCity.VSTest.TestAdapter | [Teamcity Logger][] |

[Trx Logger]: https://github.com/Microsoft/vstest/tree/master/src/Microsoft.TestPlatform.Extensions.TrxLogger
[Console Logger]: https://github.com/Microsoft/vstest/blob/master/src/vstest.console/Internal/ConsoleLogger.cs
[Xunit Logger]: https://github.com/Faizan2304/LoggerExtensions
[AppVeyor Logger]: https://github.com/Faizan2304/LoggerExtensions
[TeamCity Logger]: https://github.com/JetBrains/TeamCity.VSTest.TestAdapter

Want to add your logger? Please send a PR with changes in this doc.

## Acquisition
A test logger should be made available as a NuGet package (preferred), or as
a zip file (for e.g. loggers for C++ etc.).

If it's a NuGet package, the test logger assemblies should get copied to the
build output directory. When looking for a test logger, vstest will look for
them in the same directory as the test assemblies.

If the test logger is made available as a zip file, it should be extracted
to one of the following locations:

1. the `Extensions` folder along side `vstest.console.exe`. E.g. in case of 
dotnet-cli, the path could be `/sdk/<version>/Extensions` directory.
2. any well known location on the filesystem
 
> Version Note: new in 15.1
In case of #2, user can specify the full path to the location using `/extensions:<path>`
command line switch. Test platform will locate extensions from the provided
directory.

## Naming
Test platform will look for assemblies named `*.testlogger.dll` when it's trying
to load test loggers.

> Version Note: < 15.1
> For 15.0 version, the test loggers are also discovered from *.testadapter.dll

## Enable a test logger
A test logger must be explicitly enabled using the command line. E.g.
```
> vstest.console test_project.dll /logger:mylogger
```

## Configure reporting
Additional arguments to a logger can also be passed in the command line. E.g.
```
> vstest.console test_project.dll /logger:mylogger;Setting=Value
```

It is upto the logger implementation to support additional arguments.

## Related links
TODO: link to author a test logger
