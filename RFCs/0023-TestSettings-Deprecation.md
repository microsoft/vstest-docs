# 0023 TestSettings Deprecation

## Summary

This note outlines the proposed changes to deprecate support for testsettings in test runs.

## Motivation

Today there are two types of files to configure tests: *.testsettings and *.rusnettings. To simplify the experience, we are planning to deprecate support for *.testsettings.

## RoadMap

RunSettings will start supporting the features previously supported only via TestSettings. The following table specifies the new nodes and attributes, that will be introduced in runsettings and how they are mapped from the existing nodes in testsettings.

| TestSettings Node                                                   | RunSettings Node                                                           |
|---------------------------------------------------------------------|----------------------------------------------------------------------------|
|/TestSettings/Deployment                                             |/RunSettings/LegacySettings/Deployment                                      |
|/TestSettings/Scripts                                                |/RunSettings/LegacySettings/Scripts                                         |
|/TestSettings/Execution/TestTypeSpecific/UnitTestRunConfig           |/RunSettings/LegacySettings/Execution/TestTypeSpecific/UnitTestRunConfig    |
|/TestSettings/Execution/Timeouts: testTimeout                        |/RunSettings/LegacySettings/Execution/Timeouts: testTimeout                 |
|/TestSettings/Execution/Timeouts: runTimeout                         |/RunSettings/RunConfiguration/TestSessionTimeout                            |
|/TestSettings/Execution: parallelTestCount                           |/RunSettings/LegacySettings/Execution: parallelTestCount                    |
|/TestSettings/Execution: hostProcessPlatform                         |/RunSettings/LegacySettings/Execution: hostProcessPlatform                  |
|/TestSettings/Execution/Hosts                                        |/RunSettings/LegacySettings/Execution/Hosts                                 |
|/TestSettings/Execution/TestTypeSpecific/WebTestRunConfiguration     |/RunSettings/WebTestRunConfiguration                                        |

You can migrate your existing testsettings file to runsettings file using a migrator tool that will ship with test platform.

## Expected Ship Date

These changes are expected to be in effect from the next major release.
