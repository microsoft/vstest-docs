# Using DataCollectors
DataCollectors can be configured and used to monitor test execution through runSettings, testSettings and vstest.console args.

In this walkthrough, you will learn:
1. How `DataCollectors` were configured and used in previous version of TestPlatform (TPv1).
2. How `DataCollectors` are configured and used in latest version of Test Platform (TPv2).

This will help in understanding the key differences for using `DataCollectors`, thereby ensuring smooth migration to latest version.


## Using RunSettings
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

Please note that:
1. In previous version, DataCollectors are loaded from `<<VisualStudio Installation Directory>>\Common7\IDE\PrivateAssemblies\DataCollectors`.
In current version, DataCollectors are loaded from `TestAdaptersPaths` specified in runSettings. `DataCollectors` assemblies must follow the naming convention [*collector.dll](https://github.com/Microsoft/vstest-docs/blob/master/docs/analyze.md).

2. Previous DataCollector settings will continue to work, but additional `TestAdaptersPaths` must be specified in runsettings if `DataCollector` is not shipped along with TPv2. `TestAdapterPath` can also be specified through [CLI](# Using vstest.console args).

3. There are breaking changes in latest `DataCollector` interface. Hence, older DataCollectors need to be rebuilt against latest APIs to work with TPv2. For details, refer [here(todo)]();

## Using TestSettings
While the recommended way is to use (runsettings)[# Using RunSettings] or (vstest.console args)[# Using vstest.console args], there are few DataCollectors which only worked with testsettings.
E.g.: `System Information` DataCollector.

```xml
```

Please note that using testsettings will execute the tests through legacy test platfrom and invokes QtAgent*.exe.

Such DataCollectors can also be rebuilt againt latest APIs in order to work directly with TPv2.

## Using vstest.console args
In TPv2, DataCollectors can be configured and used throgh first class command line arguments `/collect` and `testadapterpath`. Hence, for common DataCollection scenarios, separate runsettings file may not be required.

Below is the sample command to configure and use Code Coverage DataCollector through vstest.console command line.
```
> vstest.console.exe test_project.dll /collect:"Code Coverage"
> vstest.console.exe test_project.dll /collect:"MyDataCollector" /testadapterpath:<Path to MyDataCollector assembly>
```

Please note that `testadapterpath` is not required for `DataCollectors` shipped along with TPv2.