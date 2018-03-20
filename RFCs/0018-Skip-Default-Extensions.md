# 0018 Skip Default Extensions

## Summary
This note outlines the proposed changes for adding option for skipping lookup and initialization of default extensions.

## Motivation
In addition to test adapters provided via TestAdaptersPaths, test platform loads default adapters present in Extensions folder. This folder is present alongside vstest.console.exe. Even for test sources where default extensions can't run/discover tests, we still pass test source assembly to them, this causes both increase adapter lookup, their initialization cost, & adds overhead to execution time.

Example: Default extensions can't run/discover XUnit tests, still testplatform initializes default adapters and pass XUnit test assemblies to them.

Proposed changes are focused on improving performance of test run/discovery by allowing option to skip default extensions.

## Proposed Changes
1. Design mode clients can skip default extensions by setting TestPlatformOptions.SkipDefaultExtensions as true.
2. TestRequestManager passes SkipDefaultExtensions flag to TestPlatform via CreateDiscoveryRequest/CreateTestRunRequest.
3. TestPlatform passes SkipDefaultExtensions flag to ProxyDiscoveryManager/ProxyExecutionManager via initialize method.
4. ProxyDiscoveryManager/ProxyExecutionManager stores this value and uses it to skip default extensions to be passed to test host whenever test host extensions are initialized.

## API Changes
1. Adding of field SkipDefaultExtensions in TestPlatformOptions.
2. TestPlatform's CreateDiscoveryRequest/CreateTestRunRequest will accept TestPlatformOptions as additional argument.
3. Making TestPlatform internal as it is not meant to be exposed. TestPlatform supports entry point only via command line and translation layer.
4. IProxyDiscoveryManager and IProxyExecutionManager's Initialize method will accept SkipDefaultExtensions as additional argument.

## Performance Improvement Analysis
Following are the performance improvements which are achieved when default extensions are skipped.
**Sample**: XUnit test project
**Discovery Request**: We save around 500 ms while adapter initialization and 250 ms while adapter lookup.
**Execution Request**: We save around 500 ms while adapter initialization.

## Alternatives
**Alternative 1**: Passing SkipDefaultExtensions via runsettings
Issues:
SkipDefaultExtensions is something which is neither understood by test user nor by test adapter. So, it should not be part of runsettings.

**Alternative 2**: Instead of passing TestPlatformOptions to CreateDiscoveryRequest/CreateTestRunRequest, pass only SkipDefaultExtensions as we don't need TestPlatformOptions in TestPlatform.cs for anything other than SkipDefaultExtensions.
Issue:
If in future similar field needs to be added, we can directly add in TestPlatformOptions instead of updating the API.

## Questions
1. Are we fine with changing TestPlatform API? Should we set default value for TestPlatformOptions as null for backward compatibility?
2. Should we take changes for command line as well along with design mode changes?
