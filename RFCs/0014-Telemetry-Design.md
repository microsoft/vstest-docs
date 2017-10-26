# 0014 Telemetry Design

## Summary
This note details the Telemetry design for the Test Platform.

## Motivation
Telemetry will help us make the test experience better.

## Data Points gathered
1. Total number of tests discovered/ran by each adapter.
2. Total number of adapters discovered.
3. Number of sources sent for discovery/execution.
4. Total time taken by each adapter to run/discover Tests.
5. Total adapters used to run/discover tests.
6. Total time taken for discovery/execution.
7. Paralled enabled or not.
8. List of Data Collectors Enabled.
9. List of loggers Used.
10. Discovery/Execution State.
11. TargetOS.
12. Target Framework.
13. Target Platform.
14. Target Device.
15. MaxCPU count.
16. TestPlatform Version.
17. CommandLine switches Used {/Settings, /Parallel, /EnableCodeCoverage, /InIsolation, /Platform, /Framework, /UseVsixExtensions}.

## Telemetry Design 
### Sending Consent for Collecting Metrics in Test Platform for Design Mode Scenarios.
The "CollectMetrics" field has been added in [TestPlatformOptions](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Client/TestPlatformOptions.cs) to send consent from Design Mode Scenarios(Visual Stusio IDE etc) to TestPlatform. The users have to set "CollectMetrics" so that TestPlatform can collect Metrics and send it back to the users.

The [IVsTestConsole Wrapper](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.VsTestConsole.TranslationLayer/Interfaces/IVsTestConsoleWrapper.cs) contains API's that support TestPlatformOptions. Users have to use that API's to send consent to the TestPlatform for collecting Metrics.

### Collecting Data
* Collect Telemetry Data Points in various process(testhost,datacollector etc) and send it to vstest.console process where it will be uploaded. 

**For eg:**
* In Test Host Process:
We have to collect how much time does each executor took to run test, Time taken to load adapters etc.

* In Vstest.console:
We have to collect Total Discovery Time taken, Total Tests Run in case of parallel scenarios.

**Collection in Test Platform will only happen if TestPlatform receives consent from the consumers.**

It may happen that TestHost is on a newer version whereas vstest.console is on older version. So,TestHost process should not collect Metrics if there is no consent given to test host by vstest.console process.
So, for sending consent from Vstest.console process to Test Host, Command line argument i.e. boolean "TelemetryOptedIn" is sent to TestHost Process from Vstest.console process.

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
Currently, At the end of Discovery Complete, we are sending ** TestDiscovery.Complete ** message event along with DiscoveryCompletePayload, so we will add our collected Metrics along with DiscoveryCompletePayload. Similar will be done at end of ** TestExecution.Complete ** event where we will add the Metrics in TestRunCompleteEventArgs. This helps us in sending whole metrics in one go and helps us to decrease performance overhead of sending messages from test host process to vstest.console process.


### Publishing Data

For Publishing data, there are two scenarios:
* Design Mode: We will be aggregating all the data in vstest.console and send to various IDE's(VS, VSCode etc) giving the IDE's options to add this telemetry data along with thier own Telemetry.

* Non-Design Mode:
We will be using VSTelemetry for first phase as of now to cover all windows scenarios. In phase 2, we will be extending support for crossplat.

### Posting data back to Design Mode Scenarios.
Consumers can get the Metrics in the Event Handler itslelf.

The whole aggregated metrics will be appended in vstest.console process in the final Execution/Disocvery Complete message and it will be send back to the consumers.When users use API's that are available in [IVSTestConsoleWrapper](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.VsTestConsole.TranslationLayer/Interfaces/IVsTestConsoleWrapper.cs), they have to pass the event handler which will contain API's to get back the Metrics from TestPlatform.

In Case of Execution, users will pass [ITestRunEventsHandler](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Client/Interfaces/ITestRunEventsHandler.cs), which contains [TestRunCompleteEventArgs](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Client/Events/TestRunCompleteEventArgs.cs) which will have Metrics in it which users can consume.


In Case of Discovery, users have to pass new interface [ITestDiscoveryEventsHandler2](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Client/Interfaces/ITestDiscoveryEventsHandler2.cs) which contains [DiscoveryCompleteEventArgs](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Client/Events/DiscoveryCompleteEventArgs.cs) which will have metrics in it which users can consume.

