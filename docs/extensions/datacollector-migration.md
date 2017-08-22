# Migrate your TestPlatform v0(TPv0)/TestPlatoformv1(TPv1) datacollector to TestPlatform v2(current version) datacollector
DataCollectors were supported in TPv0(mstest.exe)/TPv1(vstest.console.exe). 
This document will walk you through the changes that are required to migrate your TPv0/TPv1 DataCollector to work with TPv2.

## Referencing DataCollector Framework
Previously, `DataCollector` absract class was present in `Microsoft.VisualStudio.QualityTools.ExecutionCommon.dll` under namespace `Microsoft.VisualStudio.TestTools.Execution`.

Now, `DataCollector`abstract class is present in Object Model. Add reference to `Microsoft.TestPlatform.ObjectModel` (preview) nuget package. DataCollector APIs are present under namespace `Microsoft.VisualStudio.TestPlatform.ObjectModel.DataCollection`

## Deprecated Attributes
Currently `DataCollectorFriendlyNameAttribute` and `DataCollectorTypeUriAttribute` are the only attirbutes that are supported. 
Following attributes have been deprecated and should be removed if already being used.
1. `DataCollectorEnabledByDefaultAttribute`
2. `DataCollectorDescriptionAttribute`
3. `DataCollectorConfigurationEditorTypeUriAttribute`
4. `DataCollectorSupportsTailoredApplicationsAttribute`
5. `DataCollectorVersionObsoleteAttribute` 
6. `DataCollectorConfigurationEditorAttribute`

## Deprecated Events
Currently, four events are exposed to DataCollectors through `DataCollectionEvents`:
1. Session Start.
2. Test Case Start.
3. Test Case End.
4. Session End.

Following ten events that were exposed to DataCollectors through `DataCollectionEvents` have been deprecated and should be removed if already being used:
1. Session Start.
2. Session End.
3. Session Pause.
4. Session Resume.
5. Test Case Start.
6. Test Case End.
7. Test Case Pause.
8. Test Case Resume.
9. Test Case Reset.
10. Test Case Failed.
11. Test Step Start.
12. Test Step End.
13. Data Request.
14. Custom Notification.

## DataCollector RunSettings
DataCollector RunSettings are highly compatible in all the versions of TestPlatform.
