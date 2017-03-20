# 0009 Editors API Revision Update

## Summary
This note outlines the proposed changes for the JSON protocol between an Editor/IDE
and the test platform.

## Overview of changes

### Communication Message
Protocol related communication messages between Editor and Test Platform will have the following structure:

#### API Payload
| Key         | Type   | Description                                            |
|-------------|--------|--------------------------------------------------------|
| MessageType | string | Type of message                                        |
| Payload     | object | Payload for an operation input or output. Can be null. |

#### Example
```json
{
    "MessageType": "ProtocolVersion",
    "Payload": 1
}
```

### Versioned Message
All other messages between an Editor and Test Platform will be versioned and have the following structure:

#### API Payload
| Key         | Type   | Description                                            |
|-------------|--------|--------------------------------------------------------|
| MessageType | string | Type of message                                        |
| Version     | int    | Version based on which message should be deserialized  |
| Payload     | object | Payload for an operation input or output. Can be null. |

#### Example
```json
{
  "MessageType": "Extensions.Initialize",
  "Version": 2,
  "Payload": [
    "E:\\UnitTest1\\UnitTest1\\bin\\Debug\\net452\\Microsoft.VisualStudio.TestPlatform.MSTest.TestAdapter.dll"
  ]
}
```

Since now we have two kind of messages, the default serializer should be capable of deserializing both kind of messages.
For messages with version, this version will be used to choose the respective serializer for serializing and deserializing the payload.

### Version Operation
An Editor uses the version operation to check the protocol version supported
by the available test platform. It may modify the protocol for further communication if needed.

#### Version (Request)
Editor will have a range of versions it supports. Editor sends version request with maximum supported version.
Following is the structure of the version message.

##### API Payload
| Key         | Type   | Description                |
|-------------|--------|----------------------------|
| MessageType | string | ProtocolVersion            |
| Payload     | int    | Maximum supported version  |

##### Example
```json
{
    "MessageType": "ProtocolVersion",
    "Payload": 1
}
```

#### Version (Response)
Test Platform also has the range of versions it supports. Testplatform then sends back the maximum supported version that
Editor and Test Platform have in common.  

##### API Payload
| Key         | Type   | Description     |
|-------------|--------|-----------------|
| MessageType | string | ProtocolVersion |
| Payload     | int    | 1               |

##### Example
```json
{
    "MessageType": "ProtocolVersion",
    "Payload": 2
}
```

#### Version Negotiation
Editor sends version request with maximum supported version. Testplatform then sends back the maximum common supported version.

For Example:
* Editor with range (1-3) sends Version(Request) with version = 3, and then Test Platform with range (1-2) will send back version as 2.
* Editor with range (1-2) sends version(Request) with version = 2, and then Test Platform with range (1-3) will send back version as 2.

If TestPlatform does not support the Editor, it will send RnnerProtocolError message as discussed in the section below.

At this point the initial handshake between Editor and Test Platform is
complete. Above operation is required only once per launch of test platform.
All the messages henceforth from Editor will have version set based on the protocol negotiation.

## Discover Tests
### Start Discovery (Request)
The TestDiscovery.Start request will have the negotiated version as part of the message. 

#### API Payload
| Key         | Type   | Description            |
|-------------|--------|------------------------|
| MessageType | string | TestDiscovery.Start    |
| Version     | int    | Version of the message |
| Payload     | object | See below              |

##### Message Payload
| Key         | Type   | Description                    |
|-------------|--------|--------------------------------|
| Sources     | array  | Array of test container paths. |
| RunSettings | string | Run settings xml               |

#### Example
```json
{
  "MessageType": "TestDiscovery.Start",
  "Version" : 2,
  "Payload": {
    "Sources": [
      ".\\samples\\UnitTestProject\\bin\\Debug\\netcoreapp1.0\\UnitTestProject.dll"
    ],
    "RunSettings": null
  }
}
```

### Tests Found (Response)
TestFound response will also have the version based on which Editor will be able to deserialize the message.
Verbosity for the json of TestCase object inside the TestFound payload has been reduced significantly. Checkout the example for the new json.

This version will be based on the negotiation that happens between TestHost and Test Platform.
Hence the version stamped on the response will be the maximum common supported version for all the three components.
Example:
Let us say, Editor supports range (1-3) and Test Platform Runner supports range (1-3), so the negotiated stamped on the discovery request will be 3 (maximum common supported version).
* Test Host supports range (1-2) : This means TestHost will send back version as 2.
* Test Host supports range (1-3) : This means TestHost will send back version as 3.

If the TestHost does not support the version it will send an error message to Editor via Runner. 

#### API Payload
| Key         | Type   | Description                       |
|-------------|--------|-----------------------------------|
| MessageType | string | TestDiscovery.TestFound           |
| Version     | string | Version of the message            |
| Payload     | array  | See below for details of Property |

#### Example
```json
{
  "MessageType": "TestDiscovery.TestFound",
  "Version": 2,
  "Payload": [
    {
      "Id": "850ad69f-0dc9-fb92-8500-8d2f8d8dfe2a",
      "FullyQualifiedName": "_20TestProject.UnitTest1.Test1",
      "DisplayName": "Test1",
      "ExecutorUri": "executor://MSTestAdapter/v2",
      "Source": ".\\samples\\UnitTestProject\\bin\\Debug\\netcoreapp1.0\\UnitTestProject.dll",
      "CodeFilePath": null,
      "LineNumber": 0,
      "Properties": [
        {
          "Key": {
            "Id": "MSTestDiscovererv2.IsEnabled",
            "Label": "IsEnabled",
            "Category": "",
            "Description": "",
            "Attributes": 1,
            "ValueType": "System.Boolean"
          },
          "Value": true
        },
        {
          "Key": {
            "Id": "MSTestDiscovererv2.TestClassName",
            "Label": "ClassName",
            "Category": "",
            "Description": "",
            "Attributes": 1,
            "ValueType": "System.String"
          },
          "Value": "TestProject.UnitTest1"
        },
        {
          "Key": {
            "Id": "TestObject.Traits",
            "Label": "Traits",
            "Category": "",
            "Description": "",
            "Attributes": 5,
            "ValueType": "System.Collections.Generic.KeyValuePair`2[[System.String],[System.String]][]"
          },
          "Value": []
        }
      ]
    }
  ]
}
```

Similarly, DiscoveryComplete result will also have the version stamping.

## Run Tests
Similar to discovery requests, run tests request will also have the version as part of the message. Here are the examples.

### Run Tests (Request) Example
```json
{
  "MessageType": "TestExecution.RunAllWithDefaultHost",
  "Version": 2,
  "Payload": {
    "Sources": [
      ".\\samples\\UnitTestProject\\bin\\Debug\\netcoreapp1.0\\UnitTestProject.dll"
    ],
    "TestCases": null,
    "RunSettings": null,
    "KeepAlive": false,
    "DebuggingEnabled": false
  }
}
```

### Test Run Statistics (Response) Example
```json
{
  "MessageType": "TestExecution.Completed",
  "Version": 2,
  "Payload": {
    "TestRunCompleteArgs": {
      "TestRunStatistics": {
        "ExecutedTests": 1,
        "Stats": {
          "Passed": 1
        }
      },
      "IsCanceled": false,
      "IsAborted": false,
      "Error": null,
      "AttachmentSets": [],
      "ElapsedTimeInRunningTests": "00:00:00.8677523"
    },
    "LastRunTests": {
      "NewTestResults": [
        {
          "TestCase": {
            "Id": "850ad69f-0dc9-fb92-8500-8d2f8d8dfe2a",
            "FullyQualifiedName": "_20TestProject.UnitTest1.Test1",
            "DisplayName": "Test1",
            "ExecutorUri": "executor://MSTestAdapter/v2",
            "Source": "C:\\\\Users\\\\sasin\\\\Documents\\\\Visual Studio 2017\\\\Projects\\\\20TestProject\\\\20TestProject\\\\bin\\\\Debug\\\\net452\\\\20TestProject.dll",
            "CodeFilePath": null,
            "LineNumber": 0,
            "Properties": [
              {
                "Key": {
                  "Id": "MSTestDiscovererv2.IsEnabled",
                  "Label": "IsEnabled",
                  "Category": "",
                  "Description": "",
                  "Attributes": 1,
                  "ValueType": "System.Boolean"
                },
                "Value": true
              },
              {
                "Key": {
                  "Id": "MSTestDiscovererv2.TestClassName",
                  "Label": "ClassName",
                  "Category": "",
                  "Description": "",
                  "Attributes": 1,
                  "ValueType": "System.String"
                },
                "Value": "_20TestProject.UnitTest1"
              },
              {
                "Key": {
                  "Id": "TestObject.Traits",
                  "Label": "Traits",
                  "Category": "",
                  "Description": "",
                  "Attributes": 5,
                  "ValueType": "System.Collections.Generic.KeyValuePair`2[[System.String],[System.String]][]"
                },
                "Value": []
              }
            ]
          },
          "Attachments": [],
          "Outcome": 1,
          "ErrorMessage": null,
          "ErrorStackTrace": null,
          "DisplayName": null,
          "Messages": [],
          "ComputerName": null,
          "Duration": "00:00:00.0072901",
          "StartTime": "2017-03-20T19:57:18.2262042+05:30",
          "EndTime": "2017-03-20T19:57:18.2921987+05:30",
          "Properties": []
        }
      ],
      "TestRunStatistics": {
        "ExecutedTests": 1,
        "Stats": {
          "Passed": 1
        }
      },
      "ActiveTests": []
    },
    "RunAttachments": [],
    "ExecutorUris": [
      "executor://mstestadapter/v2"
    ]
  }
}
```

All the other messages like Cancel, Abort or debugging related messages follow the same pattern.

## Error message for ProtocolVersion mismatch

##### API Payload
| Key         | Type   | Description                                  |
|-------------|--------|----------------------------------------------|
| MessageType | string | ProtocolError                                |
| Payload     | object | String containing the supported range        |

##### Example
```json
{
    "MessageType": "ProtocolError",
    "Payload": "Protocol version is not supported. Supported range is (1-2)"
}
```









