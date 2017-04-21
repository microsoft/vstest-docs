  # RunSettings argument through commandline
  
  This argument will help you to specify runsettings settings through commandline arguments. For example, you can change the .NET Framework on which the tests will be run, the directory where test results are delivered during a test run.
  
  **Note:** Runsettings is a *.runsettings file which allow user to configure unit test. More info here :  https://msdn.microsoft.com/en-us/library/jj635153.aspx 
  
  ## Syntax
  
  `vstest.console.exe [Arguments] [Options] [[--] <args>...]]` or 
  `dotnet test [options] <PROJECT> [[--] <additional arguments>...]]`
  
  `args` or `additional arguments` may be specified as name-value pair of the form `n=v`, where `n` is the argument name, and `v` is the argument value. All arguments after `--` will be treated as `additional arguments`. Use a space to separate multiple arguments.
  
  
  ## Examples
  
  1) Use following Runsettings (lets say its name is `runLevel.runsettings`) to configure result directory and framework.
  
  ```XML
<?xml version="1.0" encoding="utf-8"?>  
<RunSettings>  
    <RunConfiguration>  
      <ResultsDirectory>.\TestOutputDirectory</ResultsDirectory>    
      <TargetFrameworkVersion>Framework40</TargetFrameworkVersion>  
    </RunConfiguration> 
</RunSettings>
```

we can run the tests using `runLevel.runsettings` by running following command

`vstest.console.exe testAssembly.dll --TestAdapterPath:PATH-TO-ADAPTER --Settings:runLevel.runsettings`

Using `additional arguments` syntax we can run tests with the same configuration as with tests.runsettings without using tests.runsettings as follows:

`vstest.console.exe testAssembly.dll --TestAdapterPath:PATH-TO-ADAPTER  -- RunConfiguration.ResultsDirectory=".\TestOutputDirectory" RunConfiguration.TargetFrameworkVersion=Framework40`

2) Use following Runsettings (lets say its name is `adapterlevel.runsettings`) to configure inconclusive tests to failed.
  
  ```XML
<?xml version="1.0" encoding="utf-8"?>  
<RunSettings>  
    <MSTest>  
      <MapInconclusiveToFailed>True</MapInconclusiveToFailed>      
    </RunConfiguration> 
</MSTest>
```

we can run the tests using `adapterlevel.runsettings` by running following command

`vstest.console.exe testAssembly.dll --TestAdapterPath:PATH-TO-ADAPTER --Settings:adapterlevel.runsettings`

we can run the tests using `additional arguments` syntax by running following command

`vstest.console.exe testAssembly.dll --TestAdapterPath:PATH-TO-ADAPTER  -- MSTest.MapInconclusiveToFailed=True`
