# 0014 Telemetry Design

## Summary
This note details the Telemetry design for the Test Platform.

## Motivation
Telemetry will help us make the test experience better.

## Events to be gathered
1. Discover Tests
2. Run Tests
3. Run Selected Tests

* We will be collecting the data points for all the above events end to end to improve our features. This events will be gathered for both design mode scenarios and command Line Interfaces which will help us reach out to every possible customers.

## Data Points
1. Total number of tests discovered/ran by each adapter.
2. Total number of adapters discovered.
3. Time taken to start Execution/Discovery Engine.
4. Number of sources sent for discovery/execution.
5. Total time taken by each adapter to run/discover Tests.
6. Total adapters used to run/discover tests.
7. Total time taken for discovery/execution.
8. Paralled enabled or not.
9. Data Collectors Enabled or not.
10. Peak Working set for Run.
11. Discovery/Execution State.

## Telemetry Design 

### Collecting Data
* Collect Telemetry Data Points in various process(testhost,datacollector etc) and send it to vstest.console process where it will be uploaded.

**For eg:**
* In Test Host Process:
We have to collect how much time does each executor took to run test, Time taken to load adapters etc.

* In Vstest.console:
We have to collect Total Discovery Time taken, Total Tests Run in case of parallel scenarios.

#### Aggregating data points in Test Host and Data Collector process
We will create a Dictonary which will contain dictionary as <string,string> key pair and we will collect all the data points in this dictionary. 

    /// <summary>
    /// This Interface Provides API's to Collect Metrics in TestHost and DataCollector Processes.
    /// </summary>
    public interface IMetricsCollector
    { 
        /// <summary>
        /// Add Metric in the Metrics Cache
        /// </summary>
        /// <param name="message">Metirc Message</param>
        /// <param name="value">Value associated with Metric</param>
        void AddMetric(string message, string value);

        /// <summary>
        /// Get Metrics
        /// </summary>
        /// <returns>Returns Metrics</returns>
        IDictionary<string, string> GetMetrics();

        /// <summary>
        /// Flush the Metrics
        /// </summary>
        void FlushMetrics();
    }

This class will be part of TestPlatform.Common and will have access in TestHost and DataCollector processes.


#### Sending Metrics from TestHost process to vstest.console process
Currently, At the end of Discovery Complete, we are sending ** TestDiscovery.Complete ** message event along with DiscoveryCompletePayload, so we will add our collected Metrics along with DiscoveryCompletePayload. Similar will be done at end of ** TestExecution.Complete ** event where we will add the Metrics in TestExecutionCompletePayload. This helps us in sending whole metrics in one go and helps us to decrease performance overhead of sending messages from test host process to vstest.console process.

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
        /// Gets or sets the Metrics
        /// </summary>
        public IDictionary<string, string> Metrics { get; set; }
    }

* Similar approach can be used for Data Collector process, where when the session ends then we will append our metrics to last event sent.

### Publishing Data

For Publishing data, there are two scenarios:
* Design Mode: We will be aggregating all the data in vstest.console and send to various IDE's(VS, VSCode etc) giving the IDE's options to add this telemetry data along with thier own Telemetry. This will require a protcol change at translation layer.

* Non-Design Mode:
We will be using VSTelemetry for first phase as of now to cover all windows scenarios. In phase 2, we will be extending support for crossplat.


### Posting data back to server.
* We will have IUnitTestTelemetryServiceProvider which be used in vstest.console.exe to aggregate the events and sending back to the server.
        
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

* Since, we want a minimal change if in future if API(like VSTelemetry, Application Insights) is changed, we will be creating TelemetryServiceProviderFactory to return the API to be used.

        /// <summary>
        /// The telemetry service provider factory.
        /// </summary>
        public static class TelemetryServiceProviderFactory
        {
        /// <summary>
        /// The Default telemetry service provider.
        /// Returns the default Telemetry Service Provider.
        /// </summary>
        /// <returns>
        /// The <see cref="IUnitTestTelemetryServiceProvider"/>.
        /// </returns>
        public static IUnitTestTelemetryServiceProvider GetDefaultTelemetryServiceProvider()
        {
            return new UnitTestTelemetryServiceProvider();
        }
        }
