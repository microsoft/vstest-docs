# Contribution Guide

This article will help you build, test and try out local builds of the VS test
platform.

## Prerequisites
The development machine should allow execution of powershell scripts. It can be
set with following command in an *Administrator* powershell session:

```powershell
> Set-ExecutionPolicy Unrestricted
```

Please ensure you have a `.net 4.6.2` or higher installed on the machine.

Clone the repository to a local directory. Rest of this article assumes
`/src/vstest` as the location of source enlistment.

```
> git clone https://github.com/Microsoft/vstest.git
```

If you're planning to use **Visual Studio** as development environment, please
install `VS 2015 Update 3` and the `.NET Tools for VS Preview 2`. Rest of the
instructions will have a separate category for VS and CLI/Editors.

## Build

### Build source code (Visual Studio)

Open `/src/vstest/TestPlatform.sln` in VS.

Use `Build Solution` to build the source code.

Binaries for each assembly are produced in the
`artifacts/src/<Assembly>/bin/Debug` directory.

### Building source code (CLI, CI, Editors)

To build the repository, run the following command:

```
> cd /src/vstest
> build.cmd
```

This command will fetch the latest `dotnet-cli` into `/src/vstest/tools/dotnet`
directory. It will use the `dotnet` executable present there to build the source
code. All the nuget required for build will be downloaded to
`/src/vstest/packages` directory.

Build will produce following assets:

* A portable `vstest.console` for desktop (net46 target) and xplat (netcoreapp)
  target
* A visual studio extension `Microsoft.TestPlatform.vsix` with the test platform
  components required in VS test explorer
* Test platform SDK packages for ObjectModel and TranslationLayer

Binaries for each assembly is produced along side the source. E.g. ObjectModel
assemblies can be found at
`/src/vstest/src/Microsoft.TestPlatform.ObjectModel/bin/Debug/net46/*.dll`.

To build a particular configuration, use the `-c` option. E.g. to trigger a
release build use

```
> build.cmd -c Release
```

For other options, check `/src/vstest/scripts/build.ps1`.

## Test

There are two sets of tests:

* Unit tests
    - Very fast tests primarily validating individual units
    - Named as `<UnitUnderTest>.UnitTests` where UnitUnderTest is any product
        assembly
* Smoke tests
    - Slower end to end tests. Typically these cover P0 scenarios (99% of users
        will use these, if these are broken, PR will not be merged)
    - Driven by a real `vstest.console` executable
    - Named as `Microsoft.TestPlatform.SmokeTests`
* End to end tests
    - Slower end to end tests for extensive coverage
    - Driven by a real `vstest.console` executable
    - Named as `Microsoft.TestPlatform.AcceptanceTests`

As a principle, most of tests are unit tests (~70-80%), few smoke tests
(~20-15%), fewer acceptance tests (~10-5%).

Unit tests and smoke/acceptance tests are run with the `vstest.console` built by
the `build` step above.

### Running tests (Visual Studio)

TBD

### Running tests (CLI, CI, Editors)

To execute tests, run the following command:

```
> cd /src/vstest
> test.cmd
```

By default, only unit tests are run. To run the smoke tests, provide the `-p`
option to `test.cmd` to set test assembly pattern:

```
> test.cmd -p smoke
```

The `-p` option can be used to run tests for any assembly as well. E.g.
following command will run tests for *datacollector*:

```
> test.cmd -p datacollector
```

Tests for a particular configuration can be run with following command. By
default, `Debug` configuration is run.

```
> test.cmd -c release
```
