# 0028 Dotnet test on multi target project logging on multiple targets

## Summary
Dotnet test on a multi-target projects logs only the last target. In multi target project, the log file name provided is being overwritten and ending up in data loss. Issue: [https://github.com/microsoft/vstest/issues/1603](https://github.com/microsoft/vstest/issues/1603)

Example: `dotnet test "--logger:trx;LogFileName=results.trx"` on a multi-target project (e.g. `<TargetFrameworks>netcoreapp2.0;net45</TargetFrameworks>` in the .csproj) causes the logger to only log on the last target.

## Design

### Option 1: Separate folders for separate targets

There are 2 ways to specify the LogFileName.
&nbsp;&nbsp;&nbsp;&nbsp;a. Relative filename: `dotnet test "--logger:trx;LogFileName=results.trx"`
&nbsp;&nbsp;&nbsp;&nbsp;b. Absolute path: `dotnet test "--logger:trx;LogFileName=d:/results.trx"`

In case of (a), the trx is generated in the test results directory of the multi target project.

Solution: Generate different target trx files in separate folders inside the test results directory.
&nbsp;&nbsp;&nbsp;&nbsp;UnitTestProject/TestResults/net45/results.trx
&nbsp;&nbsp;&nbsp;&nbsp;UnitTestProject/TestResults/netcoreapp2.0/results.trx

For case (b), the trx file will still be overwritten with a warning.

### Option 2: Specify LogFilePrefix Parameter

Introduce a LogFilePrefix parameter in trx logger. Example : `dotnet test "--logger:trx;LogFilePrefix=results"`
With this, if we want all trx files in a multi target project, instead of specifying a logFileName, we provide a LogFilePrefix.
The trx file name prefix is appended with time stamp to generate multi target trx files.

For example : `dotnet test "--logger:trx;LogFilePrefix=results"` will generate
&nbsp;&nbsp;&nbsp;&nbsp;UnitTestProject/TestResults/results_2018-12-24_14-01-07-176.trx
&nbsp;&nbsp;&nbsp;&nbsp;UnitTestProject/TestResults/results_2018-12-24_14-01-08-111.trx

The behavior of  `dotnet test "--logger:trx;LogFileName=results.trx"` will remain same with overwriting being done, and warning to switch to LogFilePrefix.