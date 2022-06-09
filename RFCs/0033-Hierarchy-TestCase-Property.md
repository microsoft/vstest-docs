

# 0033 Hierarchy TestCase Property

## Summary
This document standardizes an additional `Hierarchy` property on TestCase to support more flexible visual display of tests in the Visual Studio Test Explorer.

## Overview
The `ManagedType` and `ManagedMethod` properties [have been defined](0017-Managed-TestCase-Properties.md) as a way of deterministically identifying the type and method to which a test case belongs (in managed code). However, the legacy `FullyQualifiedName` property is still required to deduce a Namespace, Classname and TestGroup for display in the Test Explorer hierarchy. When the Test Explorer added a hierarchy for easier grouping and navigation of tests, there was no specified way for a TestCase to provide those values so they were heuristically deduced from `FullyQualifiedName`. 

This document specifies a way for the TestCase to provide these display values directly to the test explorer, granting flexibility and control back to the test adapter.

## Specification

TestCases for managed code may include a string array (string[]) valued property named `Hierarchy`. The specification below outlines the requirements for the contents of the property.

### `Hierarchy` Property

The `Hierarchy` test case property represents the text strings used to display the test in the Visual Studio Test Explorer window. 

* The property must be a string array with 4 elements. If the property is null, or missing or doesn't have 4 elements then it is is ignored.
* The element values are arranged as `[TestGroup, Class, Namespace, Container]`, which is the reverse of the order of display in the Test Explorer. i.e. Container is the top level node, Namespace is next, etc... Each TestCase is coalesced into a tree using the following order from the root. `Container`, `Namespace`, `Class`, `TestGroup`, `DisplayName`.
* If `TestGroup` is the same for all tests under a particular `Class`, then the `TestGroup` level is omitted from the hierarchy.
* `Container` usually represents the project name or the assembly name.
* `Namespace` represents the namespace containing the test suite (or a suitable semantic equivalent).
* `Class` normally represents the test suite.
* `TestGroup` typically represents the method that implements a particular test or set of tests (if data-driven).
* `DisplayName` is the name of a particular single test case.
