# Passing additional arguments through commandline
You are here because you are looking for syntax & details to pass additional arguments to either `vstest.console.exe` or `dotnet test` 

Additional arguments is a way to pass arguments as [name]=[value] with a separator `-- `. Note the space after --. This can be used to pass additional arguments to test extensions like test adapters. They will be available to the test extensions as part of `runsettings`. 
```
dotnet test  -- MSTest.MapInconclusiveToFailed=True
```

This syntax is another way of passing this argument through `runsettings` and you need not author a runsetting file to pass an additional argument to the adapter. More details about runsettings can be found [here](https://msdn.microsoft.com/en-us/library/jj635153.aspx). Runsetting for the same will look something like this:

```xml
<?xml version="1.0" encoding="utf-8"?>  
<RunSettings>  
  <!-- MSTest adapter -->  
  <MSTest>  
    <MapInconclusiveToFailed>True</MapInconclusiveToFailed>  
  </MSTest>   
</RunSettings> 
```
```
dotnet test --settings additionalargs.runsettings
```
  
This syntax can be used to pass any additional arguments to test framework adapters or extensions like logger through the CLI.

