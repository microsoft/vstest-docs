# 0026 RunSettings Provider Extensibility

## Summary
Allow runtime updation of extension's configuration in runsettings by 3rd party runsettings provider extension.

## Motivation
Configuration settings are passed to TestPlatform extensions (like DataCollector, Logger) via runsettings. TestPlatform extensions might require test run specific settings (like Test sources) in addition to configuration settings. RunSettings provider extension point allows updating configuration settings of extension. Thus test run specific settings can be added in extension's configuration settings.

## Design
A new RunSettings Provider extension can be implemented by extending the abstract `RunSettingsProvider` class.

```csharp
using System.Xml;
using Microsoft.VisualStudio.TestPlatform.ObjectModel;
using Microsoft.VisualStudio.TestPlatform.ObjectModel.RunSettingsProvider;
using Microsoft.VisualStudio.TestPlatform.ObjectModel.RunSettingsProvider.Attributes;

[ExtensionUri("my://new/runsettingprovider/1.0")]
[SettingsType("datacollector")]
[SettingsUri("my://datacollector/1.0")]
public class NewRunSettingsProvider : RunSettingsProvider
{
	public override XmlElement Process(SettingsProviderOptions settingsProviderOptions, XmlElement extensionElement)
	{
		// Process and update extension element
		return extensionElement;
	}
}
```

Here is a brief descriptions of each attribute and argument used in RunSettingsProvider.

### ExtensionUri
TestPlatform uniquely identifies each of the `RunSettingsProvider` by `ExtensionUri`.

### SettingsType
Extension type which RunSettingsProvider is targeting to. Currently supported settings type are: `datacollector` and `logger`.

### SettingsUri
Uri of the extension which RunSettingsProvider is targeting to.

### SettingssProviderOptions
`SettingsProviderOptions` holds test platform options. These test platform options can be used to update the extension element in runsettings.
```csharp
public class SettingsProviderOptions
{
	public IEnumerable<string> Sources { get; }
}
```

### ExtensionElement
`ExtensionElement` is XmlElement of the target extension present in runsettings. If target extension is not present in runsettings, `null` value is passed for extensionElement argument.

### RunSettingsProvider assembly naming convention 
Separate assembly is not required for RunSettingsProvider. RunSettingsProvider can be specified in same assembly as of its target extension (like DataCollector, Logger). Thus, naming convention is similar to target extension (`*collector.dll` or `*logger.dll`)
