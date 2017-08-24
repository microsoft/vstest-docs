# DataCollector Migration 
TestPlatform has introduced differences and enhancements to the data collection infrastructure. If you already have written data collectors for previous versions of TestPlatform, then you will need to migrate them.
This document will walk you through the changes that are required to migrate your TMI/MSTest.exe based DataCollector to work with TestPlatform.

## Referencing DataCollector Framework
Previously, `DataCollector` absract class was present in `Microsoft.VisualStudio.QualityTools.ExecutionCommon.dll` under namespace `Microsoft.VisualStudio.TestTools.Execution`.

Now, `DataCollector`abstract class is present in Object Model. Add reference to [`Microsoft.TestPlatform.ObjectModel`](https://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/15.5.0-preview-20170810-02)  (preview) nuget package. DataCollector APIs are present under namespace `Microsoft.VisualStudio.TestPlatform.ObjectModel.DataCollection`.
It is recommended to target your DataCollector to netstandard, so that it can also run cross-plat (on non Windows OS).
For more info, refer [here](https://github.com/Microsoft/vstest-docs/blob/master/docs/extensions/datacollector.md)

## Deprecated Attributes
Currently `DataCollectorFriendlyNameAttribute` and `DataCollectorTypeUriAttribute` are the only attirbutes that are supported. 
Following attributes have been deprecated and should be removed if already being used.
1. `DataCollectorEnabledByDefaultAttribute`
2. `DataCollectorDescriptionAttribute`
3. `DataCollectorConfigurationEditorTypeUriAttribute`
4. `DataCollectorSupportsTailoredApplicationsAttribute`
5. `DataCollectorVersionObsoleteAttribute` 
6. `DataCollectorConfigurationEditorAttribute`

These attributes don't serve any purpose in TestPlatform and therefore, removed.

## Deprecated Events
Currently, four events are exposed to DataCollectors through `DataCollectionEvents`:
1. Session Start.
2. Test Case Start.
3. Test Case End.
4. Session End.

Following ten events that were exposed to DataCollectors through `DataCollectionEvents` have been deprecated and should be removed if already being used:
1. Session Pause.
2. Session Resume.
3. Test Case Pause.
4. Test Case Resume.
5. Test Case Reset.
6. Test Case Failed.
7. Test Step Start.
8. Test Step End.
9. Data Request.
10. Custom Notification.

These events are no longer supported in TestPlatform and hence, these have been removed from DataCollection infra as well.

## DataCollector RunSettings
DataCollector RunSettings are highly compatible in all the versions of TestPlatform and old settings should continue to work with TestPlatform. For more info on runsettings, refer [Configure DataCollectorss](https://github.com/Microsoft/vstest-docs/blob/master/docs/analyze.md#configure-datacollectors)