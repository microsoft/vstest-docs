# Monitor and analyze test run
This document will walk you through enabling data collection for a test run. We will
start with brief overview of data collectors, followed by instructions for [code
coverage][coverage].

> **Version note:**
>
> Data collectors are supported on test platform `15.3.0` onwards. It is part of
> VS 2017 15.3 and dotnet-cli 2.0.0 builds.

[coverage]: #coverage

## Data collectors
A data collector is a test platform extension to monitor test run. It can
perform tasks when a test run starts, before and after each individual test
is run, and when the test run finishes.

You can author a data collector to collect code coverage data for a test run,
to collect logs when a test case or test run fails. These additional files
are called Attachments, they can be attached to a test result (trx).

You can provide default input to your custom diagnostic data adapter using a
configuration settings file. For example, you can provide information about the
location of the file you want to collect and attach to your test results. This
data can be configured for each test settings that you create.

Please refer [todo]() for instructions on creating a data collector and [here](https://github.com/Microsoft/vstest-docs/blob/master/RFCs/0006-DataCollection-Protocol.md)
if you're interested in the architecture of data collection.

### Acquisition
A data collector should be made available either as a NuGet package (preferred)
or as zip file (for e.g. data collectors for say, Python/C++).
 
If made available as a NuGet package, it should support a build script that
when invoked will "copy local" the data collector bits alongside the built test
assemblies. When looking for a data collector, vstest will look for them to be
alongside the test assemblies. Thus, the user adds a reference to the data
collector in his IDE project (just as in the case of test framework/adapter),
and everything just works. In the CI system, as part of the NuGet package
resolution during CI, the data collector will similarly get copied alongside
the test assemblies, and everything just works.
 
If the data collector is made available as a zip file, it should be extracted
to one of the following locations:

1. the `Extensions` folder along side `vstest.console.exe`. E.g. in case of 
dotnet-cli, the path could be `/sdk/<version>/Extensions` directory.
2. any well known location on the filesystem
 
> Version Note: TBD, draft spec
In case of #2, user can specify the full path to the location using `/extensions:<path>`
command line switch. Test platform will locate extensions from the provided
directory.
 
#### Naming
When test platform is looking for a data collector it will likely need to examine many
assemblies. As an optimization, test platform will only look at distinctly named
assemblies; specifically, a data collector must follow the naming convention
`*collector.dll`. By enforcing such a naming convention, test platform can speed up
locating a data collector assembly. Once located, test platform will load the data
collector for the entire run.
 
### Enable a data collector
All data collectors configured in the .runsettings files are loaded
automatically and are enabled to participate for run, unless explicitely disabled
using boolean valued attribute attribute named `enabled`.

For example, only `coverage` data collector will be enabled for a test run with
below runsettings:

```xml
<DataCollectionRunSettings> 
    <DataCollectors> 
      <DataCollector friendlyName="coverage">
      </DataCollector> 
  
      <DataCollector friendlyName="systeminfo" enabled="false">
      </DataCollector> 
    </DataCollectors> 
  </DataCollectionRunSettings>
```

A specific data collector can be explicitely enabled using the
`/collect:<friendly name>` command line switch.

For example, below command line will enable a data collector named `coverage` 
(and disable other data collectors mentioned in .runsettings):
```
> vstest.console test_project.dll /collect:coverage
```
 
More than one data collectors can also be enabled using `/collect` command line switch

For example, below command will enable data collectors named `coverage` and `systeminfo`:
```
> vstest.console test_project.dll /collect:coverage /collect:systeminfo
```

### Configure data collection
Additional configuration for a data collector should be done via a `.runsettings`
file. For e.g. a code coverage data collector might want to specify a set of
assemblies to ignore – this is additional configuration, and would be specified
in a `.runsettings` file.

```xml
<DataCollectionRunSettings> 
    <DataCollectors> 
      <DataCollector friendlyName="coverage"> 
        <Configuration> 
          <CodeCoverage> 
            <ModulePaths> 
              <Exclude> 
                <ModulePath>.*CPPUnitTestFramework.*</ModulePath> 
              </Exclude> 
            </ModulePaths> 
          </CodeCoverage> 
        </Configuration> 
      </DataCollector> 
    </DataCollectors> 
  </DataCollectionRunSettings>
```

## Working with Code Coverage<a name="coverage"></a>
### Setup a project
Add a reference to the `Microsoft.CodeCoverage` [nuget package][coveragenuget] to your project. This will bring in
coverage infrastructure for a test project. Here's a sample project file, please note the xml entities marked as
`Required`.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netcoreapp1.1</TargetFramework>
    
    <!-- Required in both test/product projects. This is a temporary workaround for https://github.com/Microsoft/vstest/issues/800 -->
    <DebugType>Full</DebugType>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.3.0-preview-20170502-03" />
    <PackageReference Include="MSTest.TestAdapter" Version="1.1.17" />
    <PackageReference Include="MSTest.TestFramework" Version="1.1.17" />
    
    <!-- Required. Include this reference for coverage -->
    <PackageReference Include="Microsoft.CodeCoverage" Version="1.0.3" />
  </ItemGroup>

</Project>
```

[coveragenuget]: https://www.nuget.org/packages/Microsoft.CodeCoverage/

### Analyze coverage with Visual Studio
Use the `Analyze Code Coverage` context menu available in `Test Explorer` tool window to start a coverage run.

After the coverage run is complete, a detailed report will be available in the `Code Coverage Results` tool window.

Please refer the MSDN documentation for additional details: https://msdn.microsoft.com/en-IN/library/dd537628.aspx

### Collect coverage with command line runner
Use the following command line to collect coverage data for tests:

```
> C:\Program Files (x86)\Microsoft Visual Studio\xyz\Extensions\TestPlatform\vstest.console.exe --collect:"Code Coverage" --framework:".NETCoreApp,Version=v1.1" d:\testproject\bin\Debug\netcoreapp1.1\testproject.dll
```

This will generate a `*.coverage` file in the `d:\testproject\TestResults` directory.

> NOTE: Support for code coverage in `dotnet test` command line is work in progress.
