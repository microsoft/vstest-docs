# How to author a data collector
A new data collector can be implemented by extending the abstract DataCollector class. 

```csharp
[DataCollectorFriendlyName("NewDataCollector")]
[DataCollectorTypeUri("my://new/datacollector")]
class NewDataCollector : DataCollector
{
    public override void Initialize(
            System.Xml.XmlElement configurationElement,
            DataCollectionEvents events,
            DataCollectionSink dataSink,
            DataCollectionLogger logger,
            DataCollectionEnvironmentContext environmentContext)
        {
        }
}
```
## Configuration Element
Configuration xml can be passed to DataCollectors using runsettings.
```xml
<RunSettings>
    <DataCollectionRunSettings>
        <DataCollectors>
            <DataCollector friendlyName="NewDataCollector">
                <Configuration>
                    <!-- Add your configuration here-->
                </Configuration>
            </DataCollector>
        </DataCollectors>
    </DataCollectionRunSettings>
</RunSettings>
```

## DataCollectionEvents
DataCollectors can choose to subscribe to any of the four events exposed by `DataCollectionEvents` 
a. TestSessionStart : Raised when test execution session starts.
b. TestSessionEnd : Raised when test execution session ends.
c. TestCaseStart : Raised when test case execution starts.
d. TestCaseEng : Raised when test case execution ends.

```csharp
events.SessionStart += this.SessionStarted_Handler;
events.SessionEnd += this.SessionEnded_Handler;
events.TestCaseStart += this.Events_TestCaseStart;
events.TestCaseEnd += this.Events_TestCaseEnd;
```

## DataCollectionSink
DataCollectors can create files while handling these events and send these files to runner using `DataCollectionSink`.

```csharp
dataSink.SendFileAsync(context, filename, ture);
```

Files send using above api gets associated with session level attachments or test case level attachments based on the context passed.

## DataCollectionEnvironmentContext
DataCollector framework maintains a session level context for test exectuion session and test level contexts for each test that gets executed.
`DataCollectionEnvironmentContext` passed as argument in constructor has session level context that can be access through property `SessionDataCollectionContext`
Test case level context is available as part of `TestCaseStartEventArgs` and `TestCaseEndEventArgs` through property `Context`.

## DataCollectionLogger
DataCollectors can also log errors or warnings using `DataCollectionLogger`.
```csharp
logger.LogError(this.context.SessionDataCollectionContext, new Exception("my exception"));
logger.LogWarning(this.context.SessionDataCollectionContext, "my warning");
```

## DataCollection Environment Variables
DataCollectors can choose to specify some information about how the test execution environment should be set up by implementing `ITestExecutionEnvironmentSpecifier`

```csharp
DataCollectorFriendlyName("NewDataCollector")]
[DataCollectorTypeUri("my://new/datacollector")]
class NewDataCollector : DataCollector, ITestExecutionEnvironmentSpecifier
{
    public IEnumerable<KeyValuePair<string, string>> GetTestExecutionEnvironmentVariables()
    {
    }
}
```
Environment variables returned by the above method are set in the test exectuion process while bootstraping.