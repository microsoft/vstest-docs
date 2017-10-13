# Testplatform Migration Known issues
This document tracks known issues those customer may encounter during the migration to latest [vstest](https://github.com/Microsoft/vstest).


| S.No | Issue | Workaround|
| ---- | ----- | --------- |
| 1 | JavaScript Test Runner Chutzpah < 4.0.0 not supported. | Update Chutzpah NuGet package to >= 4.0.0.
| 2 | In previous version, Tests runs in processes like vstest.console.exe, vstest.executionengine.exe and vstest.executionengine.x86.exe depending on run configuration. Test depends on process name which runs the tests may fail. | Update the process name to vstest.console.exe, testhost.exe,testhost.x86.exe and dotnet.exe.

### TODO: More issues need to be added.


