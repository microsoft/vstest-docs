# 0026 DataCollector Extensibility - Getting testSources in property bag 

## Summary
Getting `testSources` as part of property bag. List of test sources can be used by datacollectors for processing before test run start.

## Motivation
Data collector might need test sources list while initialization. Example: Static code coverage data collector needs to instrument the test sources before test run start.

The datacollector will receive a property bag in sessionStartEventArgs

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
    
    private void SessionStarted_Handler(object sender, SessionStartEventArgs sessionStartEventArgs)
    {
        var filename = Path.Combine(AppContext.BaseDirectory, logFileName);
        File.WriteAllText(filename, "SessionStarted");
        this.testSources = sessionStartEventArgs.Properties.GetPropertyValue(Properties.TestSources);
        this.dataCollectionSink.SendFileAsync(this.context.SessionDataCollectionContext, filename, true);
        this.logger.LogWarning(this.context.SessionDataCollectionContext, "SessionStarted");
    }


    private void Events_TestCaseStart(object sender, TestCaseStartEventArgs e)
    {
        this.logger.LogWarning(this.context.SessionDataCollectionContext, "TestCaseStarted " + e.TestCaseName);
    }
}
```

The property bag will be added in DataCollectionEventArgs so that it is available to all EventArgs which inherits from it.

`SessionStartEventArgs.Property` will contain an `IEnumerable<string>` of `testSources` which can be taken use by the datacollector and is an extensible model.
This can be further extended for sending other properties to the datacollector.