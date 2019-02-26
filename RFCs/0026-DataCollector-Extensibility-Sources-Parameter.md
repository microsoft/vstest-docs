# 0026 DataCollector Extensibility - Adding testSources parameter

## Summary
Exposing `testSources` parameter to datacollector extensions. List of test sources can be used by datacollectors for processing before test run start.

## Motivation
Data collector might need test sources list while initialization. Example: Static code coverage data collector needs to instrument the test sources before test run start.

## Using testSources parameter in DataCollector

Refer [datacollector](https://github.com/Microsoft/vstest/tree/master/test/TestAssets/OutOfProcDataCollector) doc for more details on how to write a datacollector.
To use `testSources` parameter in `DataCollector`:

```csharp
using Microsoft.VisualStudio.TestPlatform.ObjectModel.DataCollection;

[DataCollectorFriendlyName("NewDataCollector")]
[DataCollectorTypeUri("my://new/datacollector")]
public class NewDataCollector : DataCollector
{
    private string logFileName;
	private IEnumerable<string> testSources;
    private DataCollectionEnvironmentContext context;

    public override void Initialize(
            System.Xml.XmlElement configurationElement,
            DataCollectionEvents events,
            DataCollectionSink dataSink,
            DataCollectionLogger logger,
            DataCollectionEnvironmentContext environmentContext)
    {
        events.SessionStart += this.SessionStarted_Handler;
        events.TestCaseStart += this.Events_TestCaseStart;
        this.logFileName = configurationElement["LogFileName"];
		this.context = environmentContext;
    }

	public override void Initialize(
            System.Xml.XmlElement configurationElement,
			IEnumerable<string> testSources,
            DataCollectionEvents events,
            DataCollectionSink dataSink,
            DataCollectionLogger logger,
            DataCollectionEnvironmentContext environmentContext)
    {
		this.testSources = testSources;
		base.Initialize(configurationElement, events, dataSink, logger, environmentContext);
    }
    
    private void SessionStarted_Handler(object sender, SessionStartEventArgs args)
    {
        var filename = Path.Combine(AppContext.BaseDirectory, logFileName);
        File.WriteAllText(filename, "SessionStarted");
        this.dataCollectionSink.SendFileAsync(this.context.SessionDataCollectionContext, filename, true);
        this.logger.LogWarning(this.context.SessionDataCollectionContext, "SessionStarted");
    }


    private void Events_TestCaseStart(object sender, TestCaseStartEventArgs e)
    {
        this.logger.LogWarning(this.context.SessionDataCollectionContext, "TestCaseStarted " + e.TestCaseName);
    }
}
```
DataCollector exposes

`Initialize(System.Xml.XmlElement configurationElement, IEnumerable<string> testSources, DataCollectionEvents events, DataCollectionSink dataSink, DataCollectionLogger logger, DataCollectionEnvironmentContext environmentContext)`

in addition to existing

`Initialize(System.Xml.XmlElement configurationElement, DataCollectionEvents events, DataCollectionSink dataSink, DataCollectionLogger logger, DataCollectionEnvironmentContext environmentContext)`

to expose `testSources` list to `DataCollector`.
`testSources` parameter is a IEnumerable of test source file path.
