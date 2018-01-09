# 0016 Loggers

## Summary
This note outlines the proposed changes for:
1. Enabling logger support in test platform for TranslationLayer clients.
2. Allowing users to provide loggers from the runsettings.

## Motivation
1. Enabling logger support for TranslationLayer clients will allow clients to use logger extensibility feature.

2. Allowing users to provide loggers from the runsettings enables:
  * TranslationLayer clients to provide loggers to the test platform.
  * Alternative way to provide loggers in addition to the existing command line logger argument.

## Specifying a logger
Loggers can be provided to the test platform in one of the following ways:

1.  "/Logger:"UriOrFriendlyName";Key1=Value1;Key2=Value2" This is a switch to vstest.console.exe that feeds logger information to the test platform. For instance:

    ```
    /Logger:"logger://Microsoft/TestPlatform/TrxLogger/v1"
    ```

    This loads and initializes logger with "logger://Microsoft/TestPlatform/TrxLogger/v1" as uri.

    ```
    /Logger:sampleLogger;Key1=Value1;Key1=Value2
    ```

    This loads and initializes logger with "sampleLogger" as friendly name. Key1=Value1 and Key2=Value2 are passed as dictionary parameters to the logger while initialization.

2. Runsettings via "Logger" node in the LoggerRunSettings section. Here is a sample on how this can be specified:

    ```xml
    <RunSettings>
        <LoggerRunSettings>
            <Loggers>
                <Logger friendlyName="sampleLoggerwithParameters">
                    <Configuration>
                        <Key1>Value1</Key1>
                        <Key2>Value2</Key2>
                    </Configuration>
                </Logger>
                <Logger uri="logger://sample/sampleLoggerWithoutParameters1"
                        friendlyName="sampleLoggerWithoutParameters1" />
                <Logger uri="logger://sample/sampleLoggerWithoutParameters2"
                        assemblyQualifiedName="Sample.Sample.Sample.SampleLogger, Sample.Sample.Logger, Version=0.0.0.0, Culture=neutral, PublicKeyToken=xxxxxxxxxxxxxxxx"
                        friendlyName="sampleLoggerWithoutParameters2" />
            </Loggers>
        </LoggerRunSettings>
    </RunSettings>
    ```

    This loads and initializes:
    * Logger with friendlyName="sampleLoggerwithParameters". Key1=Value1 and Key2=Value2 are passed as dictionary parameters to the logger while initialization.
    * Logger with uri="logger://sample/sampleLoggerWithoutParameters1". FriendlyName is ignored in this case as uri takes more precedence.
    * Logger with assemblyQualifiedName="Sample.Sample.Sample.SampleLogger, Sample.Sample.Logger, Version=0.0.0.0, Culture=neutral, PublicKeyToken=xxxxxxxxxxxxxxxx". Uri and friendlyName are ignored in this case as assemblyQualifiedName takes more precedence.

Test platform loads custom logger assemblies from test adapter paths and source directory. Check [adapter extensibility] (0004-Adapter-Extensibility.md) to know about how to provide test adapter paths to test platform.

## Specification
1. If same logger is specified both in command line and run settings, command line takes precedence.
2. Multiple Loggers can be added in runsettings by adding additional Logger node in LoggerRunSettings.Loggers section.
3. Configuration is optional in Logger node.
4. Atleast one attribute among uri, friendlyName, assemblyQualifiedName should be present in Logger node.
5. If more than one attributes among uri, friendlyName, assemblyQualifiedName are present, then precedence order is assemblyQualifiedName > uri > friendlyName. Attributes other than precedent attribute are ignored.

## Design
Following are the proposed design changes for enabling logger support for TranslationLayer clients:
1. TestLoggerManager will manage all the loggers.  TestLoggerManager will be responsible for:
  * Initializing loggers from run settings.
  * Enabling and triggering logger events.
  * Disposing logger events.
  * Uninitializing loggers.

2. TestLoggerManager will implement both ITestRunEventsHandler and ITestDiscoveryEventsHandler2. On receiving any run/discovery event, corresponding logger event will be triggered by TestLoggerManager.

3. ProxyOperationManager will manage TestLoggerManager as loggers can register to both execution and discovery events. ProxyOperationManager will do following to manage TestLoggerManager:
  * Create the instance of TestLoggerManager.
  * Initialize loggers.
  * Dispose the instance of TestLoggerManager in its dispose method.

4. ProxyExecutionManager and ProxyDiscoveryManager will trigger TestLoggerManager events whenever any execution and discovery event is received.

5. TestTunRequest's dispose will dispose ProxyExecutionManager resulting in disposing of TestLoggerManager. Similarly DiscoveryRequest's dispose will dispose ProxyDiscoveryManager.
