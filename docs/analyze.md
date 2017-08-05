# Monitor and analyze test run
This document will walk you through enabling data collection for a test run. This document covers:
1. A brief overview of data collectors.
2. Configuring data collectors in TPV2.
3. Key differences for using `DataCollectors` in TPv2 v/S TPv1.
3. Instructions for using [code coverage][coverage].

> **Version note:**
>
> Data collectors are supported on test platform `15.3.0` onwards. It is part of
> VS 2017 15.3 and dotnet-cli 2.0.0 builds.

[coverage]: #coverage

## Data collector
A data collector is a test platform extension to monitor test run. It can be extended to perform tasks on specific test exectuion events. Currently, four events are exposed to `DataCollectors`:
1. Test Run Start event.
2. Test Case Start event
3. Test Case End event.
4. Test Run End event.

You can author a data collector to collect code coverage data for a test run,to collect logs when a test case or test run fails, etc.. These additional filesare called Attachments, they can be attached to a test result (trx).

Please refer [here](https://github.com/Microsoft/vstest-docs/blob/master/docs/extensions/datacollector.md) for instructions on creating a data collector and [here](https://github.com/Microsoft/vstest-docs/blob/master/RFCs/0006-DataCollection-Protocol.md)
if you're interested in the architecture of data collection.
 
#### Naming
When test platform is looking for a data collector it will likely need to examine many
assemblies. As an optimization, test platform will only look at distinctly named
assemblies; specifically, a data collector must follow the naming convention
`*collector.dll`. By enforcing such a naming convention, test platform can speed up
locating a data collector assembly. Once located, test platform will load the data
collector for the entire run.

## Configure DataCollectors
`DataCollectors` can be configured for monitoring test execution through runSettings, testSettings or vstest.console args.

### Using RunSettings
Below is the sample runsettings for code coverage DataCollector
```xml
<?xml version="1.0" encoding="utf-8"?>  
<RunSettings>
   <RunConfiguration>      
    <!-- Path to Test Adapters -->  
    <TestAdaptersPaths>PathToAdapters;PathToDataCollectors</TestAdaptersPaths>  
  </RunConfiguration>  

  <!-- Configurations for data collectors -->  
  <DataCollectionRunSettings>  
    <DataCollectors>  
      <DataCollector friendlyName="MyDataCollector" uri="datacollector://MyCompany/MyDataCollector/1.0">  
        <Configuration>
                    <LogFileName>DataCollectorLogs.txt</LogFileName>
        </Configuration>  
      </DataCollector>
    </DataCollectors>  
  </DataCollectionRunSettings>  
</RunSettings>
```
Below is the sample command for enabling DataCollectors using testsettings
```
> vstest.console.exe test_project.dll /settings:datacollection.runsettings
```
### Using vstest.console args
`DataCollectors` can be configured and used throgh first class command line arguments `/collect` and `/testadapterpath`. Hence, for common DataCollection scenarios, separate runsettings file may not be required.

Below is the sample command to configure and use DataCollectors through vstest.console command line.
```
> vstest.console.exe test_project.dll /collect:"Code Coverage"
> vstest.console.exe test_project.dll /collect:"MyDataCollector" /testadapterpath:<Path to MyDataCollector assembly>
```

### Using TestSettings
While the recommended way is to use [runsettings](#Using-RunSettings) or [vstest.console args](#Using-vstest.console-args), there are few DataCollectors which only worked with testsettings.
E.g.: `System Information` DataCollector. Below is the sample testsettings for using `System Information` DataCollctor.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<TestSettings name="TestSettings1" id="2d572055-54c0-4cac-8a55-9d7ffb48ac17" xmlns="http://microsoft.com/schemas/VisualStudio/TeamTest/2010">
  <Description>These are default test settings for a local test run.</Description>
  <Deployment enabled="false" />
  <Execution>
    <AgentRule name="LocalMachineDefaultRole">
      <DataCollectors>
        <DataCollector uri="datacollector://microsoft/SystemInfo/1.0" assemblyQualifiedName="Microsoft.VisualStudio.TestTools.DataCollection.SystemInfo.SystemInfoDataCollector, Microsoft.VisualStudio.TestTools.DataCollection.SystemInfo, Version=15.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" friendlyName="System Information">
        </DataCollector>
      </DataCollectors>
    </AgentRule>
  </Execution>
  <Properties />
</TestSettings>
```
Below is the sample command for enabling DataCollectors using testsettings
```
> vstest.console.exe test_project.dll /settings:datacollection.testsettings
```
### Enable/Disable a data collector
All data collectors configured in the .runsettings files are loaded automatically and are enabled to participate for run, unless explicitely disabled using boolean valued attribute attribute named `enabled`.

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

A specific data collector can be explicitely enabled using the `/collect:<friendly name>` command line switch.

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

## Key differences for using `DataCollectors` in TPv2 v/S TPv1.

1. In TPv1, DataCollectors are loaded from `<<VisualStudio Installation Directory>>\Common7\IDE\PrivateAssemblies\DataCollectors`.
In TPv2, DataCollectors are loaded from `TestAdaptersPaths` specified in runSettings or `/testadapterpath` argument of `vstest.console.exe`. `DataCollector` assemblies must follow the naming convention *collector.dll.

2. Previous DataCollector settings will continue to work, but additional `TestAdaptersPaths` must be specified in runsettings if `DataCollector` is not shipped along with TPv2. `TestAdapterPath` can also be specified through [vstest.console args](#Using-vstest.console-args) from command line.

3. There are breaking changes in latest `DataCollector` interface. Hence, older DataCollectors need to be rebuilt against latest APIs to work with TPv2. For details, refer [here(todo)]();

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
