# 0028 Blame collector hang detection

## Summary
Blame data collector now supports a new mode meant to help detect and fix hangs in test code. This mode does not introduce any perf hit on the test run as the proc dump process is only started after the specified timeout interval has elapsed. 

## Motivation
Whenever running tests in CI systems if a hang occurred it would generally lead to a timeout and abrupt cancelling of the CI pipeline without giving an oppurturnity for the test platform or other scripts to attach the necessary logs/dumps required to analyse the hang.

## Working
If the testhost does not send any messages to the datacollector for the specified duration then it is inferred as a hang and a dump is collected and the testhost process is killed to ensure any available attachments and logs are gracefully attached to the trx file and propagated up to the chain in case of a CI system for further analysis of the hang.

## Steps to configure
Proc dump path needs to be set using the environment variable PROCDUMP_PATH
Add the required settings as shown below in the runsettings file

Sample runsettings

```
<RunSettings>
    <DataCollectionRunSettings>
        <DataCollectors>
            <DataCollector friendlyName="blame" enabled="True">
                <Configuration>
                    <CollectDumpOnTestSessionHang TestTimeout="300000" DumpType="mini" />
                    <ResultsDirectory>%AGENT_TEMPDIRECTORY%\TestResults</ResultsDirectory>
                </Configuration>
            </DataCollector>
        </DataCollectors>
    </DataCollectionRunSettings>
</RunSettings>
```

Note: This works along with (but can also be used independent of) the existing collect dump option introduced in https://github.com/microsoft/vstest-docs/blob/master/RFCs/0024-Blame-Collector-Options.md

## Supported options
DumpType: If you choose to collect a full process dump. It takes values mini/full. By default, a mini dump will be created.
TestTimeout: Duration of inactivity in milliseconds (no test events from the test host) after which the data collector assumes a hang has occurred and proceeds to collect a dump and kill the test host process.
ResultsDirectory: Location to temporarily store the collected process dump

## VsTest task usage
As of now this can be used in the vstest task by making the above changes to runsettings and also enabling "advanced diagnostics" with collect dump set to "never" in the task UI if you just want hang dumps. (If both crash and hang detection needs to be enabled then set collect dump to "on abort only").
