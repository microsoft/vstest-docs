# Syntax
```vstest.console.exe --collect:"code coverage"``` or ```dotnet test --collec:"code coverage"```

# Output

A coverage file, which contains detailed report on what all code was hit when unit tests were run for specific(s) project. The generated file can be viewed in Visual Studio Enterprise, for a detailed analysis.


# Known Issues

* We have often observed failures/crashes when tests are run with Code Coverage enabled on Windows 8.1(&Lower), or Windows Server 2012(& Lower), failing with ```Access Violation in covrun32.dll```

  For such issues we recommened users to use coverage configuration specified at https://github.com/Microsoft/vstest/blob/master/src/DataCollectors/TraceDataCollector/VanguardCollector/DefaultCodeCoverageConfig.xml

* Coverage file fails to open in VS E.g. https://github.com/Microsoft/vstest/issues/1814

    One of the possible reason for this is when there are too many blocks in a single function. Currently we support ```65535(USHRT_MAX)``` blocks in a single method, beyond that we go into serialization issue while reading this data from coverage file.
