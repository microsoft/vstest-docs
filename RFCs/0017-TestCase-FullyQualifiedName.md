# 0017 Guidelines for setting the `FullyQualifiedName` on TestCase

## Summary
This note standardizes the form of `FullyQualifiedName` that test adapters should use when setting the `FullyQualifiedName` on test cases before returning them from the discovery process.

## Overview
There are a broad variety of choices that current Test Adapter implementers have made when setting the `FullyQualifiedName` on TestCase objects created during test discovery. By standardizing the format of `FullyQualifiedName`, components in the vstest infrastructure can be implemented more reliably. These guidelines are focused on unit tests written in managed languages (e.g. C# & VB). Other languages may derive less benefit from adopting these guidelines.

## Usage of `FullyQualifiedName`
The Test Platform uses `FullyQualifiedName` as a string moniker to name tests during discovery. Visual Studio may filter tests by `FullyQualifiedName` in order to more quickly filter and run specific tests. Visual Studio may also derive type information from the `FullyQualifiedName`. The guidelines below clarify the usage of `FullyQualifiedName` so that these optimized test execution scenarios can be realized.

## Background

`FullyQualifiedName` (also referenced as FQN) is an identifier supplied by each VS test adapter for each test during discovery. That same FQN value is supplied back to the adapter (along with other TestCase properties) when it's time to execute the tests. One exception to this case is the "Run All" operation which discovers all tests and executes them in one operation. There has historically been no standard for this value and each adapter has implemented its own strategy for creating FQNs.

There is a need in VS for each test to have a unique and deterministic method of identifying tests irrespective of the underlying test framework. A standardized FQN opens the path for a full and complete implementation of features like source-based discovery, dynamically fetching source information and UI elements like the hierarchy view in the Test Explorer window.

For example, in the case of source-based test discovery, we need to be able to identify tests from source code. Those same tests also need to be matched to tests discovered by reflection. Without unique and deterministic FQN identifiers, we don't have a reliable way to match corresponding tests. In other cases, such as the hierarchy view or dynamic source location fetching, we need to be able to reliably connect the source representation of a test with the type & method (via reflection) of a test. With this standard, FQN enables us to make those connections. NOTE: Our intent is that the test adapters take responsibility for source-based test discovery. Once this transition is complete, the need to keep the FQNs in sync between discovery methods will be reduced to only making sure the types and methods match up.

## Requirements of `FullyQualifiedName` and TestCase `ID`

* `FullyQualifiedName` should uniquely identify a method that represents test cases (with the optional application of a dataset). There may be duplicate FQNs within a project due to some methods being associated with multiple test cases. Note that it is possible for multiple assemblies, or multiple test executors to use the same FQNs. When comparing FQNs within a Visual Studio session, `Source`, `FQN`, and `ExecutorURI` must be combined to guarantee uniqueness.
* Each TestCase has an `ID` field that takes the form of a GUID. In the past, this field has been optional. It will now become required. The required `ID` field must be unique for a given test assembly. This `ID` field must also be deterministic, in the sense that a test with the same class, method and method arguments should have the same id. We envision generating this `ID` by hashing the test's class, method, method signature and method arguments into the GUID. 
* `FullyQualifiedName` should be immutable in that the test store keeps the exact value that is provided by the test adapter and supplies it back to the test adapter for test execution. The test adapter should be able to rely on receiving the same FQN for execution that it supplied when performing discovery.
* `FullyQualifiedName` should reference the semantic location of the method that defines the test. This means that the `FullyQualifiedName` references the method on the type where the test is discovered. In some situations, this could be different from the type where the method is defined. See later in this document for a more detailed discussion.

## `FullyQualifiedName` specification

We are standardizing the `FullyQualifiedName` property on a TestCase in the following way. The FQN will be parsed as a URI starting with the scheme value of `fqn`. 

**Method Form**

    fqn://clr/m/{type}/{method}

`fqn://` - Any FQN that starts with the characters `fqn://` will be considered to follow the standardized format.

`clr` – The first segment ("host" segment) specifies how to interpret the rest of the URI. The only valid value at the time of this writing is "clr" to reflect support for tests written in CLR managed languages. This portion can be expanded in the future to add support for non-managed languages such as Python, Javascript, C++, etc…

`m | o` – `'m'` indicates a method form FQN, `'o'` indicates a custom test case identifier that the test explorer will not attempt to interpret.

`{type}` - The `type` segment includes the fully specified type name in metadata format:

    NamespaceA.NamespaceB.ClassName`1+InnerClass`2

* The type name must be fully qualified (in the CLR sense), including its namespace. Any generic classes must also include an arity value using backtick notation (`# where # is the number of type arguments that the class requires).
* Nested classes are appended with a '+' and must also include an arity if generic.
* There should be no extra whitespace included in the segment

`{method}` - The `method` segment includes the fully specified method including the method name and a list of its parameter types inside parentheses separated by commas.

    MethodName`2(ParamTypeA,ParamTypeB,…)

* If the method accepts no parameters, then the parentheses should be omitted.
* If the method is generic, then an arity must be specified (in the same way as the type segment).
* Insignificant whitespace should not be included in the segment.
* The list of parameter types must be encoded in the same way that a type in the `{type}` segment of the FQN is encoded.

## Custom Test Naming

Some of the adapters currently modify the FQN when tests have custom names. This standard would disallow that. FQN can only represent Class/Method symbols, not test names. Test names should be reflected only in the DisplayName.

## Syntactic vs Semantic Test Location

We are defining syntactic location as the location in the code/syntax where the method is defined that implements the test. On the other hand, semantic location is the location in the type hierarchy at which point the method becomes recognized as a valid test. 

There can be a situation where a test is declared on an abstract base type (syntactic), but the test is only discovered in a derived class (semantic). The question is which type should the FQN point to? The base type, where the test code is located? Or the derived type, where the test is discovered. We will use the semantic location for the type because that is where the test adapter will find the test and it is where the test class would be instantiated. Also, there is a one to many relationship between the two. There can be many semantic test locations that each are implemented by the same base class method. If we were to standardize on using the syntactic location, we would risk having name collisions or fail to find the correct test case since there are multiple possible candidates.

## Managed Tests that are Not Type/Method Based

It is possible to create unit tests in managed code where tests are not necessarily based on types & methods. While this is somewhat uncommon, we need to be able to handle this situation gracefully. Some examples are gherkin-dotnet and custom discoverers in xUnit. In these examples, an externally parsed definition file may determine the tests. For these cases, we have defined the 'other' form of FQN. FQNs in this form will look similar to the following.

    fqn://clr/o/{extension}/{other}/{url}/{segments}…

The `'o'` indicates to the test window that we cannot interpret the contents of the FQN. The `{extension}` segment is to allow each adapter to add a custom string identifying the format. The rest of the URL is completely up to the interpretation of the test adapter. Type and method information will not be interpreted. Note that adapters using this format may lose hierarchy or code location benefits that are provided by the class/method FQN structure. There may be other ways to provide this information such as other properties on the test case. Those mechanisms are outside the scope of this document.

## Legacy Compatibility

We intend to implement a shared routine that can convert a legacy FQN into this standardized format. Throughout the TestWindow code, in all other locations, we would use the new standardized format. Any edge cases in interpretation can likely be addressed in the conversion routine. This does mean, however, that when handling test cases from adapters that do not support the format, we will need to allocate another property to save the original legacy FQN value. This is necessary so that when we call back into the adapter, we supply the original FQN rather than the new one. 

Also, when working with unmanaged test adapters, we will need to handle the case of not having a standardized FQN. One way to support non-conforming adapters is to define an FQN format specifically for them so that we can still have them "standardized" without interpreting the contents.

**Example**

    fqn://compat/Class::Method::Test()

## TestCase FQN Property Implementation

We intend for test adapter implementors to use this new FQN format for the `FullyQualifiedName` property that is supplied to the TestCase object. Even though it is not specified, there may be some compatibility concerns with existing tools that depend on the `FullyQualifiedName` being in the current format. For an intermediate period, while compatibility concerns are worked through, we would suggest providing the new FQN in an additional custom property on the TestCase object named "StdFullyQualifiedName". Adding this additional property will affect the performance and allocation profile of the testing infrastructure, and we recommend not using this technique unless it is necessary for compatibility.

## Tests Returning Multiple Results

There are some cases where the number of test cases cannot be determined at discovery time. In these cases, when the tests are executed multiple results are returned for a single discovered test case.

## Uniqueness Across Projects

FQNs (with their corresponding ID) can only be guaranteed to be unique for a Source (typically assembly) and ExecutorUri.

