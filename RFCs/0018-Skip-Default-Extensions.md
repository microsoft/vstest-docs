# 0018 Skip Default Extensions

## Summary
This note outlines the proposed changes for adding option for skipping lookup and initialization of default extensions.

## Motivation
In addition to test adapters provided via TestAdaptersPaths, test platform requires default adapters present in Extensions folder. This folder lies where vstest.console.exe lies. Even if default extensions can't run/discover tests, we still pass test assembly to default extensions and thus increase adapter lookup and initialization cost. 

Example: Default extensions can't run/discover XUnit tests, still we initialize default adapters and pass test assembly to them. Thus we   

## Proposed Changes
1. Design mode clients can skip default extensions by setting TestPlatformOptions.SkipDefaultExtensions as true.
2. TestRequestManager passes SkipDefaultExtensions flag to TestPlatform via CreateDiscoveryRequest/CreateTestRunRequest.
3. TestPlatform passes SkipDefaultExtensions flag to ProxyDiscoveryManager/ProxyExecutionManager via initialize method.
4. ProxyDiscoveryManager/ProxyExecutionManager stores this value and uses it to skip default extensions to be passed to test host whenever test host extensions are initialized.

## API Changes
1. Adding of field SkipDefaultExtensions in TestPlatformOptions.
2. TestPlatform's CreateDiscoveryRequest/CreateTestRunRequest will accept TestPlatformOptions as additional argument.
3. IProxyDiscoveryManager and IProxyExecutionManager's Initialize method will accept SkipDefaultExtensions as additional argument.

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
