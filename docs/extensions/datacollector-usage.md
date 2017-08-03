# Using DataCollectors
DataCollectors can be configured and used to monitor test execution in Visual Studio and CLI.

In this walkthrough, you will learn:
1. How `DataCollectors` were configured and used in previous version of TestPlatform.
2. How `DataCollectors` are configured and used in latest version of Test Platform.

This will help in understanding the key differences for using `DataCollectors`, thereby ensuring smoother migration to latest version.


## Visual Studio
### Visual Studio [2012, 2017 15.5)
In the previous versions of Visual Studio, configuring `DataCollectors` involved creating runsettings, adding datacollectors settings to it and executing the tests with runsettings selected.

Below is the sample runsettings for code coverage as documented in [msdn](https://msdn.microsoft.com/en-us/library/jj635153.aspx)
```xml
<?xml version="1.0" encoding="utf-8"?>  
<RunSettings>
  <!-- Configurations for data collectors -->  
  <DataCollectionRunSettings>  
    <DataCollectors>  
      <DataCollector friendlyName="Code Coverage" uri="datacollector://Microsoft/CodeCoverage/2.0" assemblyQualifiedName="Microsoft.VisualStudio.Coverage.DynamicCoverageDataCollector, Microsoft.VisualStudio.TraceCollector, Version=11.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a">  
        <Configuration>  
          <CodeCoverage>  
            <ModulePaths>  
              <Exclude>  
                <ModulePath>.*CPPUnitTestFramework.*</ModulePath>  
              </Exclude>  
            </ModulePaths>  
  
            <!-- We recommend you do not change the following values: -->  
            <UseVerifiableInstrumentation>True</UseVerifiableInstrumentation>  
            <AllowLowIntegrityProcesses>True</AllowLowIntegrityProcesses>  
            <CollectFromChildProcesses>True</CollectFromChildProcesses>  
            <CollectAspDotNet>False</CollectAspDotNet>  
  
          </CodeCoverage>  
        </Configuration>  
      </DataCollector>  

    </DataCollectors>  
  </DataCollectionRunSettings>  
</RunSettings>
```

While bootstrapping DataCollection, `DataCollectorPluginDirectory`, the directory where datacollector could be present was decided as below:
1. Look into app settings for key `DataCollectorPluginDirectory`. If specified, the path value is validated and used.
2. Look into `PrivateAssemblies\DataCollectors` folder.
3. Look into VS Installation directory from registry key.
4. Look for Test Agent Installation Path from registry key.

Additionally, `Codebase` attribute can be specified with DataCollector settings in runsettings and first attempt is made to load the DataCollector from this path, followed by `DataCollectorPluginDirectory`.

Going forward, from Visual Studio 2017 15.5 release onwards, DataCollectors will continue to use runsettings for configuration.
Below is the sample for code coverage.
```xml
<?xml version="1.0" encoding="utf-8"?>  
<RunSettings>
   <RunConfiguration>      
    <!-- Path to Test Adapters -->  
    <TestAdaptersPaths><<PathToAdapters>>;<<PathToDataCollectors>></TestAdaptersPaths>  
  </RunConfiguration>  

  <!-- Configurations for data collectors -->  
  <DataCollectionRunSettings>  
    <DataCollectors>  
      <DataCollector friendlyName="Code Coverage" uri="datacollector://Microsoft/CodeCoverage/2.0">  
        <Configuration>  
          <CodeCoverage>  
            <ModulePaths>  
              <Exclude>  
                <ModulePath>.*CPPUnitTestFramework.*</ModulePath>  
              </Exclude>  
            </ModulePaths>  
  
            <!-- We recommend you do not change the following values: -->  
            <UseVerifiableInstrumentation>True</UseVerifiableInstrumentation>  
            <AllowLowIntegrityProcesses>True</AllowLowIntegrityProcesses>  
            <CollectFromChildProcesses>True</CollectFromChildProcesses>  
            <CollectAspDotNet>False</CollectAspDotNet>  
  
          </CodeCoverage>  
        </Configuration>  
      </DataCollector>
    </DataCollectors>  
  </DataCollectionRunSettings>  
</RunSettings>
```

Please note that :
1. `assemblyQualifiedName` attribute is no more required.
In previous version, DataCollectors are loaded by finding the Assembly Name from assemblyQualifiedName and loaded from `DataCollectorPluginDirectory` folder.
In current version, `TestAdaptersPaths` are probed and a cache of `DataCollectors` is created while bootstrapping DataCollection. `DataCollectors` assemblies must follow the naming convention [*collector.dll](https://github.com/Microsoft/vstest-docs/blob/master/docs/analyze.md).

2. Previous DataCollector settings will continue to work, but additional `TestAdapterPaths` must be specified in runsettings.

## CLI

## Legacy DataCollectors