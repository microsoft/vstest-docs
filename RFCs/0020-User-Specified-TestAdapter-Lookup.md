# 0020 User Specified Test Adapter Lookup

## Summary
This note outlines the proposed changes for lookup and initialization of the test adapters, based on User input.

## Motivation

As per the current adapter lookup model, when ever a Run/Discovery call is made from IDE to TestPlatform, the test adapter initialization happens in multiple phases listed below

* InitializeExtensions(): In this call, the IDE passes list of all adapters it finds in current session, these include adapters referenced via nuget in entire solution, & adpaters acquired via Vsix(e.g. GoogleTestAdapter, BoostAdapters, etc..)
* TestAdapterPath: After InitializeExtensions call, TestPlatform then looks into adapters present in TestAdapterPath mentioned in RunSettings, & adds adapters to existing list.
* TestPlatform then adds default Adapters from **Extensions** directory to current list.
* Finally platform then looks in adapters present in test source directory, & adds them to adapter list.

Once adapters are gathered from all the possible locations, this list is passed to testhost process, which then loads all these adapters, & passes test source(s) to all the adapters.

Following the above adapter look up logic, we pass down test sources to adapters which have no business running them, for e.g. passing a managed test source to a native adapter(GoogleTestAdapter, BoostAdapters, etc.), & vice-versa.

## Principles
1. The adapter referenced in the project should be used for test execution
2. Performance should not degrade.
3. Adapter lookup logic is consistent across runs.
4. Adapter lookup logic should be clear and consistent for both IDE/Editor and CLI runs.

## Proposed Changes
Here are the proposed changes based on the sources available for lookup of the adapters.
User can restrict adapter lookup to only adapters close to source location, & those present in TestAdapterPath under RunSettings, via setting **UseSpecifedAdapterLocations** flag in RunSettings to **true**.

### Details for lookup

* If the flag "UseSpecifedAdapterLocations" is set to true, then adapters only from source, & TestAdapterPaths would be picked.
* If no adapters are found in above locations, then platform will use other adapters sent by IDE, which include adapters from nugets, & Vsix.
