# 0012 Initialization of Test Adapter and Extensions

## Summary
This note outlines the proposed changes to TestPlatform for handling various scenarios related to
initialization of adapters and extensions.

## Motivation
Issues with the current design for initialization of the extensions when multiple versions of same
extension are involved.

## Problem
There are 2 main scenarios when there are multiple versions of same adapter competing.

### Upgrade of packages
User can upgrade the adapter nuget packages in the same VS session.
In this case, older version of extension had already been initialized and then new extension is sent for
initialization.

### Multiple versions in the same solution
User can have projects targeting different version of the test adapter.
In case of net46 framework where host process is shared, the right adapter does not get initialized.

## Proposed Changes
Here are a few proposed changes in this regard:

1. All the dependencies including test adapters are copied to the bin directory of the project.
This is similar to setting /testAdapterPath to bin directory.
2. Each test container will be hosted in a separate host. An option can be given to the user to choose
between shared and unshared hosts.

Note:
* For C# based test, explicit initialization of adapters can be avoided, and hosts will pick the appropriate
adapters from the bin directory.
* In case of cli, user will still be able to use /testAdapterPath to initialize the extensions.
* Having Unshared hosts will impact performance. <TODO: Add numbers>
* Extensions shipping as VSIX will continue to be initialized.