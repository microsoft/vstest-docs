# 0012 Telemetry for Test Platform

## Summary
This note details the Telemetry design for the Test Platform. 

## Requirements
1. Telemetry should work seamlessly xplat.
2. Extensible, integration with VSTelemetry should be possible.
3. Telemetry should be available cross components.

## Telemetry Design 


### Collect Data
* Collect Telemetry Data Points in various process(testhost,datacollector etc) and send it to vstest.console process where it will be uploaded.

**For eg:**
* In Test Host Process:
We have to log how much time does each executor took to run test, Time taken to load adapters etc.

* In Vstest.console:
We have to log total adapters used ,Total tests run etc.

#### Problem:
* Telemetry Data points are generated in various process and all the telemetry data points are getting aggregated in vstest console process. We need a way to send telemetry data from process(testhost,datacollector) to vstest process in an efficient way.


#### Proposal:
We will create a cache which will contain dictionary as <string,string> key pair and we will add all the data points in this cache. 

    public class IMetricCollector
    {
        /// <summary>
        /// Add the data point in the Telemetry Cache.
        /// </summary>
        /// <param name="message">The message to be logged</param>
        /// <param name="value">The value associated with the Property</param>
        public void AddDataPoint(string message, string value);

        /// <summary>
        /// Returns the Metrics in Key Value Pair.
        /// </summary>
        public IDictionary<string, string> GetMetrics();
    }

This class will be part of TestPlatform.Common and will have access in TestHost and DataCollector processes.

#### Problem:
Since we have gather all the data points in the cache now issue is **when and how** to send the data points back to the vstest.console.exe

#### When? Since we have to gather telemetry for three events:
1. Discover Tests
2. Run Tests
3. Run Selected Tests

For all these three events data points have to be gathered end to end.
So, at the end of these events in the test host process we will send the whole data back to the vstest process.

For Data collector process, when the session will close, we will send the whole data back.
#### How?
For this problem there are two approaches:

#### Approach 1:
We are sending TestDiscovery.Complete event along with DiscoveryCompletePayload, so we can add our Telemetry data along with it only.
Similar can be done for TestExecution.Completed event and we can add Telemetry data in TestExecutionCompletePayload. Similar can be done for datacollector process as well as we can send all our data along with end sesssion.

    public class DiscoveryCompletePayload
    {
        /// <summary>
        /// Gets or sets the total number of tests discovered.
        /// </summary>
        public long TotalTests { get; set; }

        /// <summary>
        /// Gets or sets the last chunk of discovered tests.
        /// </summary>
        public IEnumerable<TestCase> LastDiscoveredTests { get; set; }

        /// <summary>
        /// Gets or sets a value indicating whether discovery was aborted.
        /// </summary>
        public bool IsAborted { get; set; }

        /// <summary>
        /// Gets or sets the Telemetry Data
        /// </summary>
        public IDictionary<string, string> TelemetryData { get; set; }
    }

##### Pros:
1. Same event already available.

##### Cons:
1. Need to do extra processing in vstest.console to filter raw message for design mode scenarios.

#### Approach 2:

We can send messages using IMessageLogger from any process to vstest.coonsole.

##### Pros:
1. Cleaner Approach

##### Cons:
1. Performance issue would be there as we are sending all the messages in real time.

#### Finalized:
We decided to go with Approach 1 as its not better to send messages in real time via IMessageLogger. It will have greater performance issue.



### Publish Data

For Publishing data, there are two scenarios:
* Design Mode: We will be aggregating all the data in vstest.console and send to various IDE's(VS,VSCode,Rider etc) giving the IDE's option to add this telemetry data along with thier own Telemetry.This will require a protcol change at translation layer.

* Non-Design Mode:
We will be using VSTelemetry for first phase as of now to cover all windows scenarios. In phase 2, we will be extending support for crossplat.


### Aggregating Data and Posting data back to server.
* We will have IUnitTestTelemetryServiceProvider which be used in vstest.console.exe to aggregate whole data and sending back to the server
        
        public interface IUnitTestTelemetryServiceProvider
        {
        /// <summary>
        /// Log Event
        /// This Method will Aggregate all the properties with values in the eventName
        /// </summary>
        /// <param name="eventName">Name of the event</param>
        /// <param name="property">Name of the property in that event</param>
        /// <param name="value">Value of Property</param>
        public void LogEvent(string eventName, string property, string value);

        /// <summary>
        /// Post Event
        /// This method will Post the event back to the server
        /// </summary>
        /// <param name="eventName">Name of the event</param>
        pubic void PostEvent(string eventName);

        /// <summary>
        /// Dispose the Telemetry Service Provider
        /// </summary>
        public void Dispose();
        }

* Since, we want a minimal change if in future if API is changed, we will be creating TelemetryServiceProviderFactory to return the API to be used.

        public interface ITelemetryServiceProviderFactory
        {
        /// <summary>
        /// The default telemetry service provider.
        /// This Method will return the default Telemetry Service Provider.
        /// </summary>
        /// <returns>
        /// The <see cref="IUnitTestTelemetryServiceProvider"/>.
        /// </returns>
        public IUnitTestTelemetryServiceProvider GetDefaultTelemetryServiceProvider();
        }