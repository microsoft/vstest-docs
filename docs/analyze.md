# Monitor and analyze test run
This document will walk you through enabling data collection for a test run.

> Note, this is a draft document. This feature will come in Q2 CY 2017.

> Version note: Data collectors are supported on test platform `15.1.0` onwards.

## Data Collectors
A data collector is a test platform extension to monitor test run. It can
perform tasks when a test run starts, before and after each individual test
is run, and when the test run finishes.

You can author a data collector to collect code coverage data for a test run,
to collect logs when a test case or test run fails. These additional files
are called Attachments, they can be attached to a test result (trx).

You can provide default input to your custom diagnostic data adapter using a
configuration settings file. For example, you can provide information about the
location of the file you want to collect and attach to your test results. This
data can be configured for each test settings that you create.

Please refer [todo]() for instructions on creating a data collector and [todo]()
if you're interesting in the architecture of data collection.

## Acquisition
A data collector should be made available either as a NuGet package (preferred)
or as zip file (for e.g. data collectors for say, Python/C++).
 
If made available as a NuGet package, it should support a build script that
when invoked will "copy local" the data collector bits alongside the built test
assemblies. When looking for a data collector, vstest will look for them to be
alongside the test assemblies. Thus, the user adds a reference to the data
collector in his IDE project (just as in the case of test framework/adapter),
and everything just works. In the CI system, as part of the NuGet package
resolution during CI, the data collector will similarly get copied alongside
the test assemblies, and everything just works.
 
If the data collector is made available as a zip file, it should be extracted
to one of the following locations:

1. the `Extensions` folder along side `vstest.console.exe`. E.g. in case of 
dotnet-cli, the path could be `/sdk/<version>/Extensions` directory.
2. any well known location on the filesystem
 
In case of #2, user can specify the full path to the location using `/extensions:<path>`
command line switch. Test platform will locate extensions from the provided
directory.
 
### Naming
When test platform is looking for a data collector it will likely need to examine many
assemblies. As an optimization, test platform will only look at distinctly named
assemblies; specifically, a data collector must follow the naming convention
`*datacollector.dll`. By enforcing such a naming convention, test platform can speed up
locating a data collector assembly. Once located, test platform will load the data
collector for the entire run.
 
## Enable a data collector
Although loaded, a data collector must be explicitly enabled for it to
participate during the test run. A data collector can be enabled using the
`/collect:<friendly name>` command line switch.

For example, below command line will enable a data collector named `coverage`:
```
> vstest.console test_project.dll /collect:coverage
```
 
All data collectors specified in the .runsettings files are loaded
automatically. However, they too need to be explicitly enabled to participate
during the run. The data collector node in the .runsettings file, will be
augmented with a boolean valued property named `<enable>`.

For example, only `coverage` data collector will be enabled for a test run with
below runsettings:

```xml
<DataCollectionRunSettings> 
    <DataCollectors> 
      <DataCollector friendlyName="coverage" enable="true">
      </DataCollector> 
  
      <DataCollector friendlyName="systeminfo">
      </DataCollector> 
    </DataCollectors> 
  </DataCollectionRunSettings>
```
 
## Configure data collection
Additional configuration for a data collector should be done via a `.runsettings`
file. For e.g. a code coverage data collector might want to specify a set of
assemblies to ignore – this is additional configuration, and would be specified
in a `.runsettings` file.

```xml
<DataCollectionRunSettings> 
    <DataCollectors> 
      <DataCollector friendlyName="coverage"> 
        <Configuration> 
          <CodeCoverage> 
            <ModulePaths> 
              <Exclude> 
                <ModulePath>.*CPPUnitTestFramework.*</ModulePath> 
              </Exclude> 
            </ModulePaths> 
          </CodeCoverage> 
        </Configuration> 
      </DataCollector> 
    </DataCollectors> 
  </DataCollectionRunSettings>
```
