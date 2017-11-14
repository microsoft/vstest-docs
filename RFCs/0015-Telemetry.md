# 0015 Telemetry

## Summary
This document outlines the telemetry data points to be collected by vstest platform along with the expectations from any vstest consuming platform, wanting to use these telemetry data points for their own needs.

## Overview
Going forward vstest platform will enable collection of rich telemetry data points to helps us and any vstest consuming platform in making the right choices to improve end user experience. The telemetry data points we plan to collect in vstest, doesn't contain any information that can be used to identify an individual e.g. name, email, username etc. More details on telemetry data points below.

## Data Points
Following telemetry data points will be collected by vstest and also enabled for collection by any vstest consuming platform:
* Size of tests (e.g. numberOfTestsSources, numberOfTestsRun, duration etc.)
* Configuration of tests (e.g. parallelExecution, dataCollectorUsed, adapterVersion etc.)
* Composition of tests (e.g. targetOS, targetPlatform, targetFramework etc.)
* Features used (e.g. codeCoverage, settings etc.)
* Time (time of operation)
* Source of invocation (vstest consuming platform)
For more details please refer to the **Detailed List of Data Points** section at the end

## Conceptual Flow
![alt text](https://github.com/Microsoft/vstest-docs/blob/master/RFCs/Images/vstest.telemetry.png) 

## Scope
* vstest and vstest.console.exe will emit telemetry data points that any vstest consuming platform can listen to
* vstest consuming platform needs to provide the following information to the vstest
  * indicator of user consent
  * source of invocation
* Consuming platform needs to create a listener that can collect the data points and route it to their respective telemetry backend
* No PII or EUII data will be collected by vstest
* vstest will respect the user consent flowing in from the consuming platform

## User Consent [Opt-In, Opt-Out]
Any vstest consuming platform can collect the telemetry events and redirect to the backend of their choice, however it is the responsibility of the consuming platform to
* Enable opt-in | opt-out experience for their users
* Ensure compliance (data, security, privacy etc.)

## License
The Microsoft distribution of vstest is licensed with the [Link](https://www.visualstudio.com/microsoft-visual-studio-test-platform/). This license includes the "DATA" section to enable telemetry (shown below).
* **DATA.**  The software may collect information about you and your use of the software, and send that to Microsoft. Microsoft may use this information to provide services and improve our products and services.  You may opt-out of many of these scenarios, but not all, as described in the product documentation.  There are also some features in the software that may enable you and Microsoft to collect data from users of your applications. If you use these features, you must comply with applicable law, including providing appropriate notices to users of your applications and you should provide a copy of Microsoft’s privacy statement to your users. The Microsoft privacy statement is located here https://go.microsoft.com/fwlink/?LinkId=521839. You can learn more about data collection and use in the help documentation and our privacy statement. Your use of the software operates as your consent to these practices.

## Detailed List of Data Points
| Group          | Attributes      |
|----------------|-----------------|
| Size           | numberOfTestsSources |
|                | numberOfTestsRun |
|                | duration |
|                | discoveryState |
|                | totalTests (Discovered) |
|                | totalTimeTakenInSeconds (Discovered) |
|                | duration |
|                | totalTests (Executed) |
|                | totalTimeTakenInSeconds (Executed) |
| Composition    | adapterVersion |
|                | targetFramework |
|                | targetPlatform |
|                | targetDevice (UWP or Not) |
|                | testPlatformVersion |
|                | targetOS |
| Configuration  | loggerUsed |
|                | dataCollectorUsed |
|                | parallelExecution |
|                | maxCpuCount |
|                | adapterUsedCount (Discovered) |
|                | adapterUsedCount (Executed) |
|                | platform (commandLineSwitches) |
|                | framework (commandLineSwitches) |
| Features       | setting (commandLineSwitches) |
|                | parallel (commandLineSwitches) |
|                | enableCodeCoverage (commandLineSwitches) |
|                | inIsolation (commandLineSwitches)|
|                | useVSIXExtensions (commandLineSwitches) |
|                | logger (commandLineSwitches) |
| Time           | dateTime |
| Source         | consumingPlatform |






