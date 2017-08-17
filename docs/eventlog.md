# Event Log Data Collector
This document introduces Event Log DataCollector. We will start with a brief overview of Event Log DataCollector, followed by steps to enable it and use cases where it will be useful.

## Introduction
Event Log DataCollector is a Windows only DataCollector that is used to get event logs logged into Windows Event Viewer during test execution. Event logs are saved in a file `Event Log.xml` and this file is available as Attachment as part of test result report (trx).

More info on Event Viewer [here](https://technet.microsoft.com/en-us/library/cc938674.aspx)

## Eanbling Event Log DataCollector
There are two ways of enabling Event Log DataCollector for a test run:
### 1. Using vstest.console argument. 
Use the following command to enable Event Log DataCollector with default configuration:

> "%vsinstalldir%\Common7\IDE\Extensions\TestPlatform\vstest.console.exe" test_project.dll /testadapterpath:<<Path to test adapter>> /collect:"Event Log"

### 2. Using runsettings.
Below runsettings can be used to enable Event Log DataCollector.

```xml
<?xml version="1.0" encoding="utf-8"?>  
<RunSettings>
  <!-- Configurations for DataCollectors -->  
  <DataCollectionRunSettings> 
    <DataCollectors> 
      <DataCollector friendlyName="Event Log" uri="datacollector://Microsoft/EventLog/2.0">
        <Configuration>
            <Setting name="EventLog" value="System,Application" />
            <Setting name="EntryTypes" value="Error,Warning" />
            <Setting name="EventSources" value="CustomEventSource" />
        </Configuration>
      </DataCollector>
    </DataCollectors>
  </DataCollectionRunSettings>
</RunSettings>
```
The above runsettings will collect event logs from `System` and `Application` event logs which are logged as `Error` or `Warning` and event source is specified as `CustomEventSource`.

In default configuration (through vstest.console.exe args or when <Configuration> section is empty in runsettings), `System`, `Application` and `Security` logs with entry types `Error`, `Warning` or `FailureAudit` and with any event source are collected.

## Use cases for Event Log DataCollector
Event Log DataCollector is used to get event logs as Attachment and is particularly useful for remote scenarios where logging into the machine and viewing the Event Viewer is not possible. 