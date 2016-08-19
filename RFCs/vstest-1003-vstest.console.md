# RFC vstest-1003 vstest.console

## Summary
This documents deals with the overall basic design of the test platform and the client - vstest.console runner.

## Motivation
There needs to be an infrastructure in place that is able to run unit tests based on different programming languages(C#/VB/C++/JS etc.) and different platforms(Windows Desktop/Linux/Mac/UWP etc.) and across different architectures(x86/x64/arm). This framework also needs to be extensible enough so that anyone can plugin easily into the key areas of the system.

## Detailed Design

The overall architecture of the test platform is detailed in the block diagram below with all the extensibility points colored in green. 

![vstest.console overall architecture]()

The test platform has 3 major processes:
	1. Runner
	2. Test host
	3. Data Collector

### Runner
The runner is the entry point to the test platform. The main functionality of the runner is to take in the test container with user specified settings, figure out what architecture, framework is required to run the tests and spawn of a host process with that setting to host and run the tests. It also houses two key extensibility points - Logger and Host extensibility. **Logger extensibility** provides users with an ability to save test results in a format of their choice which could be in a file or posted on a server. **Host extensibility** provides users with an ability to write their own custom test host process that can be in a different environment(inside of a UWP app)/ built for a different architecture, framework. These two extensibility points will be detailed in a different document.

### Test host
The test host actually hosts the test containers and runs the test. Its main functionality is to drive test discovery and execution via Adapters for a test framework. This constitutes the **adapter extensibility** which allows test framework writers like xunit/nunit/mstest to write adapters that can understand tests written in that framework and run them. Adapter extensibility is detailed in a separate document. Another key functionality that the test host house's is **In-Proc Data Collection extensibility**. This allows users to listen to test session or test case start and end events within the test host process, which one can use to figure out for instance the the code coverage for a test case. More on this extensibility point is covered in a different document.

### Data Collector
The data collector process takes care of loading the Data Collection extensibility provider that allows users to write Data collectors for a test session. This component gets test session/ test case start and end events from the test host process and notifies the registered data collectors. The data collectors can use this data to identify how much memory a test is taking or the cpu usage for a test etc. This is a separate process because:
1. We do not want the collector to affect the resources used by the test host process.
2. The test host process can be of a totally different architecture, framework which not all data collectors can load in.
This process is spawned off only when data collection is turned on. In a vanilla flow only runner and test host process are required. 

### Runner - test host interaction
1. A user would spawn of the runner with a set of test containers and settings for the test session. 
2. The runner would then process those settings to figure out key decision parameters for the run some of which are:
	* The architecture the tests should run on.(x86/x64)
	* The framework that the tests are on.(Desktop Fx/Core Fx)
	* Data collectors if enabled.
	* Path to user specified extension assemblies.
3. It uses the architecture and framework specified to spawn of a test host process that satisfies these settings.
4. The runner also starts of a TCP server to communicate with the test host process. 
5. After the test host launches it sets up a client connection with the runner. 
6. The runner would then send through the test containers with the user specified settings to the test host process.
7. The test host process performs the requested operation either discovery/execution and returns back the results in batches to the runner.
8. The test host signals an operation end to the runner which then notifies the loggers and bails out.

The protocol between the runner and the test host for discovery and execution is detailed below. The interaction between the runner, test host and data collector is detailed in a different document.

#### Discovery:	
![Discovery Protocol](https://github.com/AbhitejJohn/vstest-docs/blob/RFCvstestconsole/RFCs/Images/vstest.console-discovery.png)								
1. After launching the test host process as detailed above the runner sends a TestDiscovery.Initialize message with the full path to extension assemblies as an IEnumerable<string>. The test host then uses this to load the extensions before hand. This is an optional step and will not be sent if there are no additional extensions but the default.
2. The runner then sends a TestDiscovery.Start message with a [DiscoveryPayload](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/Client/DiscoveryCriteria.cs) which contains the test containers and the session level settings.
3. The TestPlatform.Engine component in test host process invokes the loaded adapters with these containers to discover tests.
4. When the adapter finds a test it notifies the TestPlatform.Engine which caches these test cases.
5. When the maximum cache size is hit or on a cache timeout the TestPlatform.Engine passes on a list of test cases in a TestDiscovery.TestsFound message as a List<[TestCase](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.ObjectModel/TestCase.cs)>
6. The adapter can also notify the TestPlatform.Engine of any errors/warnings during discovery via a message. This messages are then sent to the runner as a TestSession.Message with a [TestMessagePayload](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.CommunicationUtilities/Messages/TestMessagePayload.cs) This is an optional message.
7. On discovery completion the adapter notifies the TestPlatform.Engine which then sends a TestDiscovery.Completed message to the runner with a [DiscoveryCompletePayload](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.CommunicationUtilities/Messages/DiscoveryCompletePayload.cs)
8. On receiving a discovery complete from the test host the runner then ends the communication with a TestSession.Terminate.
9. On receiving a terminate message the test host process cleanly exits.
	
#### Execution:
![Execution Protocol](https://github.com/AbhitejJohn/vstest-docs/blob/RFCvstestconsole/RFCs/Images/vstest.console-execution.png)
1. After launching the test host process as detailed above the runner sends a TestExecution.Initialize message with the full path to extension assemblies as an IEnumerable<string>. The test host then uses this to load the extensions needed for execution before hand. This is an optional step and will not be sent if there are no additional extensions but the default.
2. The runner then sends a TestExecution.StartWithSources message with a [TestRunCriteriaWithSources](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.CommunicationUtilities/ObjectModel/TestRunCriteriaWithSources.cs) which contains the test containers and the session level settings.
3. The TestPlatform.Engine component in test host process invokes the loaded adapters with these containers to execute tests.
4. The adapter notifies the TestPlatform.Engine of a test case start, test result and a test case end. It maintains the test results received in a cache.
5. When the maximum cache size is hit or on a cache timeout the TestPlatform.Engine passes on a list of test results in a TestExecution.TestResults message as a [TestRunStatsPayload](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.CommunicationUtilities/Messages/TestRunStatsPayload.cs)
6. The adapter can also notify the TestPlatform.Engine of any errors/warnings during execution via a message. This messages are then sent to the runner as a TestSession.Message with a [TestMessagePayload](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.CommunicationUtilities/Messages/TestMessagePayload.cs) This is an optional message.
7. On execution completion the adapter notifies the TestPlatform.Engine which then sends a TestExecution.Completed message to the runner with a [TestRunCompletePayload](https://github.com/Microsoft/vstest/blob/master/src/Microsoft.TestPlatform.CommunicationUtilities/Messages/TestRunCompletePayload.cs)
8. On receiving a discovery complete from the test host the runner then ends the communication with a TestSession.Terminate.
9. On receiving a terminate message the test host process cleanly exits.


<!--The exact set of switches the vstest.console runner supports is listed here([Todo] add link here.))--> 

#### Note:
All IPC within the test platform is via sockets and json. 

## Open questions
1. The design above isolates crashes due to a test from crashing the runner. For better performance can we just have one single process that runs the tests for default architecture and framework? This would remove IPC and hence improve performance for the default scenarios.
