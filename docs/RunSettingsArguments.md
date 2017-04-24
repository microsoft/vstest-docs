# Passing runsettings arguments through commandline
You are here because you are looking for syntax and details to pass runsettings configurations to either `vstest.console.exe` or `dotnet test` through commandline.

`RunSettings arguments` are used to add/update specific `runsettings configurations`. The updated `runsettings configurations` will be available to `TestPlatform` and `test extensions` (E.g. test adapter, etc.) through runsettings.

## Syntax

* `RunSettings arguments` are specified as name-value pair of the form `[name]=[value]` after `-- `. Note the space after --.
* Use a space to separate multiple `[name]=[value]`.
* All the arguments after `--` will be treated as `RunSettings arguments`, means `RunSettings arguments` should be at the end of the command line.

## Example

Passing argument `-- MSTest.MapInconclusiveToFailed=True` in (1) below is equivalent to passing argument 
`--settings additionalargs.runsettings` in (2) below.

```
1) dotnet test  -- MSTest.MapInconclusiveToFailed=True MSTest.DeploymentEnabled=False
```

```
2) dotnet test --settings additionalargs.runsettings
```

where `additionalargs.runsettings` is:

```xml
<?xml version="1.0" encoding="utf-8"?>  
<RunSettings>  
  <!-- MSTest adapter -->  
  <MSTest>  
    <MapInconclusiveToFailed>True</MapInconclusiveToFailed>
    <DeploymentEnabled>False</DeploymentEnabled>
  </MSTest>   
</RunSettings> 
```


The syntax in (1) is another way of passing runsettings configuration and you need not author a runsetting file while using `Runsettings arguments`. More details about runsettings can be found [here](https://msdn.microsoft.com/en-us/library/jj635153.aspx).


`Runsettings arguments` takes precedence over `runsettings`.

For example, in below command the final value for `MapInconclusiveToFailed` will be `False` and vale for `DeploymentEnabled` will be unchanged, that is `False`.

```
dotnet test --settings additionalargs.runsettings -- MSTest.MapInconclusiveToFailed=False
```
