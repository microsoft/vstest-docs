# How to author a data collector
A new data collector can be implemented by extending the abstract `DataCollector` class. 

```csharp
using Microsoft.VisualStudio.TestPlatform.ObjectModel.DataCollection;

[DataCollectorFriendlyName("NewDataCollector")]
[DataCollectorTypeUri("my://new/datacollector")]
public class NewDataCollector : DataCollector
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
1. TestSessionStart : Raised when test execution session starts.
2. TestSessionEnd : Raised when test execution session ends.
3. TestCaseStart : Raised when test case execution starts.
4. TestCaseEng : Raised when test case execution ends.

```csharp
events.SessionStart += this.SessionStarted_Handler;
events.SessionEnd += this.SessionEnded_Handler;
events.TestCaseStart += this.Events_TestCaseStart;
events.TestCaseEnd += this.Events_TestCaseEnd;
```
```csharp
private void Events_TestCaseStart(object sender, TestCaseStartEventArgs e)
{
}
```
## DataCollectionSink
DataCollectors can create files while handling events and send these files to runner using `DataCollectionSink`.

```csharp
dataSink.SendFileAsync(context, filename, ture);
```

Files sent using above api gets associated with session level attachments or test case level attachments based on the context passed.

## DataCollectionEnvironmentContext
DataCollector framework maintains a session level context for test exectuion session and test level contexts for each test that gets executed.
`DataCollectionEnvironmentContext` passed as argument in constructor has session level context that can be accessed through property `SessionDataCollectionContext`.
Test case level context can be accessed through `TestCaseStartEventArgs.Context` or `TestCaseEndEventArgs.Context`.

## DataCollectionLogger
DataCollectors can also log errors or warnings using `DataCollectionLogger`.
```csharp
logger.LogError(this.context.SessionDataCollectionContext, new Exception("my exception"));
logger.LogWarning(this.context.SessionDataCollectionContext, "my warning");
```

## DataCollection Environment Variables
DataCollectors can choose to specify information about how the test execution environment should be set up by implementing `ITestExecutionEnvironmentSpecifier`

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