# Testplatform Migration Known issues
Here are the current known issues you may face when running tests, along with available workarounds.

# Known Issues
- [Change in Thread.CurrentPrincipal value.](CurrentPrincipal)
- [Change in test execution processes name.](processname)

### <b>Change in Thread.CurrentPrincipal value.</b><a name="CurrentPrincipal"></a>
- <b>Issue:</b> <br/>
Tests depends on `Thread.CurrentPrincipal` may fail. This is due to change in inter process commincation in Testplatform.
- <b>Workaround:</b> <br/>
Use alternative like `System.Security.Principal.WindowsIdentity.GetCurrent()`

### <b>Change in test execution processes name.</b><a name="processname"></a>
- <b>Issue:</b> <br/>
Tests depends on currnet running process name may fail.
- <b>Workaround:</b> <br/>
Tests runs in one of following process vstest.console.exe, testhost.exe, testhost.x86.exe and dotnet.exe based on run configuration (/platform and /framework). Update test according to current process name.


