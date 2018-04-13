# 0020 User Specified Test Adapter Lookup

## Summary
This note outlines the proposed changes for lookup and initialization of the test adapters, based on User input.

### Current Adapter Lookup

In the current model, when ever a Run/Discovery call is made from IDE to TestPlatform, the test adapter initialization happens in multiple phases listed below

* InitializeExtensions(): In this call, the IDE passes list of all adapters it finds in current session, these include adapters referenced via nuget in entire solution, & adpaters acquired via Vsix(e.g. GoogleTestAdapter, BoostAdapters, etc..)
* TestAdapterPath: After InitializeExtensions call, TestPlatform then looks into adapters present in TestAdapterPath mentioned in RunSettings, & adds adapters to existing list.
* TestPlatform then adds default Adapters from **Extensions** directory to current list.
* Finally platform looks in adapters present in test source directory, & adds them to adapter list.

Once adapters are gathered from all the possible locations, this list is passed to testhost process, which then loads all these adapters, & passes test source(s) to all the adapters.

Following the above adapter look up logic, we pass down test sources to adapters which have no business running them, for e.g. passing a managed test source to a native adapter(GoogleTestAdapter, BoostAdapters, etc.), & vice-versa.

## Motivation

In .NetCore scenario, we only pick adapters from test Source location, this helps
* Testplatform, as it knows where to look for adapters
* Test Framework/Adapter writers, they know where to drop adapters so they are consumed by platform,& finally
* Users as they don't have to specify any additional location for adapters, & they know exactly what adapter is used for the run.

We want to move to the same model for FullCLR projects as well.

## Principles
1. The adapter referenced in the project should be used for test execution
2. Performance should not degrade.
3. Adapter lookup logic is consistent across runs.
4. Adapter lookup logic should be clear and consistent for both IDE/Editor and CLI runs.

## Proposed Changes
User can restrict adapter lookup to only adapters close to source location, & those present in TestAdapterPath under RunSettings, via setting an option IDE to true.

The option would be present at Tool->Option->Test.

Once enabled IDE will modify the runsettings it passes to platform during discovery/execution, by adding **UseSpecifedAdapterLocations** flag in RunSettings, & setting it to **true**.


### Details for lookup

* If the flag "UseSpecifedAdapterLocations" is set to true, then adapters only from source, & TestAdapterPaths would be picked.

### Perf Improvements
Restricting adapters via above logic also results in perf improvements, as it filters out unnecessary adapters which should be not used for a given test source, primarily for a managed test source, it filters our native adapters, as they are acquired only via Vsix, or from default **Extensions** folder.

The improvement is however seen when a few tests are run, for e.g. when running two tests via RunSelected options from IDE, we see the time reduced from **0:00:01.4782809** to **0:00:01.1312048** in IDE Test Output pane 

## Open Questions:
* Should there be a UI option to set value UseSpecifedAdapterLocations, under Tool->Option->Test ? Yes, this would be available in IDE.
* Should we spawn a new testhost for each test source when above option is enabled? No, as discussed internally this will cause a perf degradation.
