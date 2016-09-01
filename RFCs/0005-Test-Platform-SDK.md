# 0005 Test Platform SDK
## Summary
This document outlines various components of test platform sdk and the usage scenarios for each of them. It will also cover versioning and compatibility.

## Motivation
Test platform exposes various extensibility points in the architecture. These allow a developer to customize the test framework, test host, logger and so on. In addition, an editor can use test platform to list and execute test runs.

It is necessary to establish clear contract in several aspects:
* Packages: which package a developer can use for each scenario.
* Versioning: how are the packages versioned?
* Compatibility: what is the compatibility provided by packages (in terms of previous versions of test platform)?

The contract (in case of extensions), and protocol (in case of editors) are outlined in previous specification documents. This document will pivot around scenarios and will cover above aspects for each.

## Scenarios
### Authoring an extension
Test platform allows a developer to author an extension to customize the behavior of test platform. At the time of writing, following extensibility points are available:

| Extension type    | Purpose                                  |
|-------------------|------------------------------------------|
| Adapter           | Customize test framework                 |
| Data collector    | Monitor and collect data during test run |
| Logger            | Customize test execution logging         |
| Test host         | Control process/runtime for a test run   |

#### SDK requirements
Extensions are `.NET` assemblies. They require to implement a set of APIs provided in the [Microsoft.TestPlatform.ObjectModel][ObjectModelNuget] package.

Following is the `.NET` libraries supported by the ObjectModel package:

| Version   | .NET runtime                      |
|-----------|-----------------------------------|
| 11.0.0    | net35, netstandard1.0             |
| 15.0.0    | netstandard1.3                    |

[ObjectModelNuget]: http://www.nuget.org/packages/Microsoft.TestPlatform.ObjectModel/

#### Compability

| Version   | Compatibility                      |
|-----------|------------------------------------|
| 11.0.0    | Supports VS 2012 - present         |
| 15.0.0    | Supports VS 2016 - present         |

The `15.0.0` version of `Microsoft.TestPlatform.ObjectModel` introduces several additional capabilities:
* In process data collection
* Test host extensibility
* Better serialization (to support JSON wire protocol)

Newer versions of test platform will be able to load extensions authored with `11.0.0` version of ObjectModel. However to use newer functionality, extension authors may consider providing multiple versions of the extension targeting VS 2015 or older and the newer VS respectively.

### Editor integration
Test platform allows integration with an editor using a JSON wire protocol. The editor can launch the test platform to list, execute tests and report statistics for a run.

#### SDK requirements
There is no strict requirement for a authoring an editor integration in a particular language since the communication can be driven with JSON over the wire. At the moment, a `.NET` implementation is available. It is used by Visual Studio to drive test execution from the Test Explorer.

Developers can use `Microsoft.TestPlatform.TranslationLayer` nuget package. It is a *redistributable* package.

| Version   | .NET runtime                      |
|-----------|-----------------------------------|
| 15.0.0    | netstandard1.3                    |

#### Compatibility
Editor integration is available from Test Platform `15.0.0` onwards.

| Version   | Compatibility                           |
|-----------|-----------------------------------------|
| 15.0.0    | Supports Test Platform 15.0.0 - present |

## Open questions
None.
