## Problem Statement - Motivation
Code targeting .NET 2.0/3.0/3.5 needs CLR 2.0 to run.
Code targeting.NET 4+ needs CLR 4.0 to run.
 
The vstest runner launches testhost.exe to discover/execute tests.
Testhost.exe itself is built against .NET 451. Therefore, it will run in CLR 4.0, and any DLLs it loads will be loaded into CLR 4.0.
But what if the test code/DLL was targeting .NET 2.0/3.0/3.5? Such “legacy” test code requires CLR 2.0 to run.
What should vstest do?

## Proposed Solution
1. By default, vstest will not run test code targeting <= NET3.5 . It will emit an error message and exit. The message will provide additional information by pointing to online documentation.
2. User will have to opt-in to run code targeting <= NET35. Such code will be run by vstest in CLR4.0's compat mode. The opt-in will be via the following existing mechanisms:
    1. a command line switch (using ```/Framework:```)
    2. runsettings file (from IDE) using ```<TargetFrameworkVersion>xxx</TargetFrameworkVersion>```
 
vstest will look at all of the test DLLs given to it, and then decide. If any of the test DLLs passed in is targeting <= NET35, then it will exit.
The following table captures the expected behaviour:

| Test DLL target Framework | Configuration switch    |                                 Runs on                                     |
| ------------------------- |-------------------------| ----------------------------------------------------------------------------|
|       <= NET3.5           | No switch present       | Will not run. vstest.console.exe exits with an error message.               |
|                           | /Framework:Framework35  | Will not run. vstest.console.exe exits with an error message.               |
|                           | /Framework:Framework40  | CLR 4.0's compat mode. Framework settings passed to the adapters as before. |
|                           | /Framework:Framework45  | CLR 4.0's compat mode. Framework settings passed to the adapters as before. |
|                           |                         |                                                                             |
|       >= NET4.0           | No switch present       | CLR 4.0. Framework settings passed to the adapters as before.               |
|                           | /Framework:Framework35  | CLR 4.0. Framework settings passed to the adapters as before.               |
|                           | /Framework:Framework40  | CLR 4.0. Framework settings passed to the adapters as before.               |
|                           | /Framework:Framework45  | CLR 4.0. Framework settings passed to the adapters as before.               |

## References
1. .NET 4 migration issues: https://docs.microsoft.com/en-us/dotnet/framework/migration-guide/net-framework-4-migration-issues
2. .NET Framework Versions and Dependencies: https://docs.microsoft.com/en-us/dotnet/framework/migration-guide/versions-and-dependencies
3. CLR <starstup> Element: https://docs.microsoft.com/en-us/dotnet/framework/configure-apps/file-schema/startup/startup-element
