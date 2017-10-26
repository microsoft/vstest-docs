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
### Sending Consent for Collecting Metrics in Test Platform for Design Mode Scenarios.
We have given options in TestPlatformOptions to send consent from Design Mode Scenarios. The users have to set CollectMetrics to send whether to collect Metrics or not.

    /// <summary>
    /// Options to be passed into the Test Platform during Discovery/Execution.
    /// </summary>
    [DataContract]
    public class TestPlatformOptions
    {
        /// <summary>
        /// Gets or sets the filter criteria for test cases.
        /// </summary>
        /// <remarks>
        /// This is only used when running tests with sources.
        /// </remarks>
        [DataMember]
        public string TestCaseFilter { get; set; }

        /// <summary>
        /// Gets or sets the filter options if there are any.
        /// </summary>
        /// <remarks>
        /// This will be valid only if TestCase filter is present.
        /// </remarks>
        [DataMember]
        public FilterOptions FilterOptions { get; set; }

        /// <summary>
        ///  Gets or sets whether Metrics should be collected or not.
        /// </summary>
        [DataMember]
        public bool CollectMetrics { get; set; }
    }
    
How to use?


### Collecting Data
* Collect Telemetry Data Points in various process(testhost,datacollector etc) and send it to vstest.console process where it will be uploaded.

**For eg:**
* In Test Host Process:
We have to collect how much time does each executor took to run test, Time taken to load adapters etc.

* In Vstest.console:
We have to collect Total Discovery Time taken, Total Tests Run in case of parallel scenarios.

#### Aggregating data points in Test Host process
We will create a Dictonary which will contain dictionary as <string,object> key pair and we will collect all the data points in this dictionary.

    /// <summary>
    /// This Interface Provides API's to Collect Metrics.
    /// </summary>
    public interface IMetricsCollection
    {
        /// <summary>
        /// Add Metric in the Metrics Cache
        /// </summary>
        /// <param name="metric">Metric Message</param>
        /// <param name="value">Value associated with Metric</param>
        void Add(string metric, object value);

        /// <summary>
        /// Get Metrics
        /// </summary>
        /// <value>Returns the Telemetry Data Points</value>
        IDictionary<string, object> Metrics { get; }
    }

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
        public IDictionary<string, object> Metrics { get; set; }
    }

### Publishing Data

For Publishing data, there are two scenarios:
* Design Mode: We will be aggregating all the data in vstest.console and send to various IDE's(VS, VSCode etc) giving the IDE's options to add this telemetry data along with thier own Telemetry.

* Non-Design Mode:
We will be using VSTelemetry for first phase as of now to cover all windows scenarios. In phase 2, we will be extending support for crossplat.

### Posting data back to Design Mode Scenarios.

