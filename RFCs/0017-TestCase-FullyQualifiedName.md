# 0017 Guidelines for setting the FullyQualifiedName on TestCase

## Summary
This note clarifies the guidelines that test adapters should consider when setting the FullyQualifiedName on test cases before returning them from the discovery process.

## Overview
There are a broad variety of choices that current Test Adapter implementers have made when setting the FullyQualifiedName on TestCase objects created during test discovery. This note lays out some basic guidelines to make the usage of FullyQualifiedName more useful across adapters. These guidelines are focused on languages that support namespaces, classes and methods for structuring test cases (e.g. C# & VB). Other languages may not fit these guidelines.

## Usage of FullyQualifiedName
The Test Platform uses FullyQualifiedName as a string moniker to name tests during discovery. Visual Studio may filter tests by FullyQualifiedName in order to more quickly filter and run specific tests. The guidelines below clarify the usage of FullyQualifiedName so that these optimized test execution scenarios can be realized.

## Guidelines
1. **FullyQualifiedName should be unique across your test set.** Internally, TestCase objects are tracked by a unique ID (GUID) which can either be set by the Test Adapter implementor, or automatically generated otherwise. The FullyQualifiedName should be unique if possible, but it's not a requirement.
1. **FullyQualifiedName should be deterministic** FullyQualifiedName should have the same value for the same test across different discovery sessions. This means that including random data, time-dependent data or environment specific data in the FullyQualifiedName should be avoided.
1. **FullyQualifiedName is expected to be a reference to the method that implements the test** The Test Platform is expecting the FullyQualifiedName to refer to a particular test case. If there are multiple tests that are instantiated from a test method (data-driven tests for instance), then the FullyQualifiedName should distinguish these using parentheses to represent data parameters and angle brackets to represent type parameters. See below.

## Recommended Form
FullyQualifiedName is expected to be a reference to the TestCase method that implements the test (or tests). The FullyQualifiedName should be unique to a particular TestCase instance, if possible.

The recommended forms of FullyQualifiedName are described by the following examples:

    Namespace.Namespace.Class.Method
    Namespace.Namespace.Class.Method()
    Namespace.Namespace.Class<Int32>.Method()
    Namespace.Namespace.Class<Int32>.Method<String>()
    Namespace.Namespace.Class+InnerClass.Method
    Namespace.Namespace.Class.Method(x: 1, msg: "string")
    Namespace.Namespace.Class.Method(1, "string")
    Namespace.Namespace.Class(init: "Value").Method(param: 23)
    Namespace.Namespace.Class<String>("Value").Method(23)

## Normalized Form
When referencing test cases by FullyQualifiedName, the test platform recognizes a normalized form of the FullyQualifiedName. This normalized form is the FullyQualifiedName with segments in parentheses and segments in angle brackets removed. The normalized form will not be unique among TestCases.

| Fully Qualified Name | Normalized Fully Qualified Name |
|---|---|
| `Namespace.Namespace.Class.Method()` | `Namespace.Namespace.Class.Method` |
| `Namespace.Namespace.Class<Int32>.Method()` | `Namespace.Namespace.Class.Method` |
| `Namespace.Namespace.Class<Int32>.Method<String>()` | `Namespace.Namespace.Class.Method` |
| `Namespace.Namespace.Class+InnerClass.Method` | `Namespace.Namespace.Class+InnerClass.Method` |
| `Namespace.Namespace.Class.Method(x: 1, msg: "string")` | `Namespace.Namespace.Class.Method` |
| `Namespace.Namespace.Class.Method(1, "string")` | `Namespace.Namespace.Class.Method` |
| `Namespace.Namespace.Class(init: "Value").Method(param: 23)` | `Namespace.Namespace.Class.Method` |
| `Namespace.Namespace.Class<String>("Value").Method(23)` | `Namespace.Namespace.Class.Method` |


The normalized form allows the test platform to reference groups of tests in a more general form without having to interpret the logic that the test adapter uses when constructing the fully qualified name. 

NOTE: Normalization is currently only used for languages that support source-based test discovery. At the time of this writing, that includes MSTest, NUnit and xUnit tests written in C# or VB.