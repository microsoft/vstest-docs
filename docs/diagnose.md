# Test platform diagnostics

This document outlines troubleshooting and diagnosis instructions for test platform.

## Collect traces using command line

The console test runner (`vstest.console`) provides a `diag` switch to collect
traces to a log file. Invoke the runner using below command line:

```
> vstest.console testApp.dll --diag:log.txt
```

Verbose trace information will be available in the `log.txt` file. You can also
provide a path `/tmp/dir/log.txt`. `/tmp/dir` will be created for you if it
doesn't exist.

## Collect trace using config file

Second technique to enable tracing is via a configuration file. Create
a `vstest.console.exe.config` configuration file in the same directory as
`vstest.console`. Similar configuration is also possible for `testhost.exe` or `testhost.x86.exe`.

```
> where vstest.console
d:\tmp\vstest.console.exe

> notepad d:\tmp\vstest.console.exe.config
```

Add the following content to the config file (`vstest.console.exe.config` or `testhost.exe.config`).

```
<configuration>
  <system.diagnostics>
    <sources>
      <source name="TpTrace" 
        switchName="sourceSwitch" 
        switchType="System.Diagnostics.SourceSwitch">
        <listeners>
          <!-- This will spew out all traces to stdout. Add as appropriate -->
          <!-- <add name="console" 
            type="System.Diagnostics.ConsoleTraceListener">
            <filter type="System.Diagnostics.EventTypeFilter" 
              initializeData="Warning"/>
          </add> -->

          <add name="logfile"/>

          <remove name="Default"/>
        </listeners>
      </source>
    </sources>
    <switches>
      <add name="sourceSwitch" value="All"/>
    </switches>
    <sharedListeners>
      <!-- This will add all verbose logs to d:\tmp\log.txt -->
      <add name="logfile" 
        type="System.Diagnostics.TextWriterTraceListener" 
        initializeData="d:\tmp\log.txt">
        <filter type="System.Diagnostics.EventTypeFilter" 
          initializeData="Verbose"/>
      </add>
    </sharedListeners>
  </system.diagnostics>
</configuration>
```

## Debug test platform components

The runner and test host processes support waiting for debugger attach. You can
enable following environment variable to keep `vstest.console.exe` waiting for
debugger attach:

```
> set VSTEST_RUNNER_DEBUG=1
> vstest.console testApp.dll
Waiting for debugger attach...
Process Id: 51928, Name: vstest.console
```

For test host process (`testhost.exe`) use the following environment variable.
Note that there will be no message on console for test host. Execution will
halt until debugger is attached.

```
> set VSTEST_HOST_DEBUG=1
> vstest.console testApp.dll
Microsoft (R) Test Execution Command Line Tool Version 15.0.0.0
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...
```
