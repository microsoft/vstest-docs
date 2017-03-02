# TestCase filter
This document will help you to selectively execute test based on filtering condition through `--filter` for `dotnet test` and `--testcasefilter` for `vstest.console.exe`.

### Syntax
   `dotnet test --filter <Expression>` or
   `vstest.console.exe --testcasefilter:<Expression>`

**Expression** is of the format __\<property>\<operator>\<value>[|&\<Expression>]__. Expressions can be
enclosed in paranthesis. E.g. `(Name~MyClass) | (Name~MyClass2)`.

> An expression without any **operator** is automatically considered as a `contains` on `FullyQualifiedName` property.
E.g. `dotnet test --filter xyz` is same as `dotnet test --filter FullyQualifiedName~xyz`.

**Property** is an attribute of the `Test Case`. For example, following are the properties
supported by popular unit test frameworks.

| Test Framework | Supported properties |
| -------------- | -------------------- |
| MSTest         | <ul><li>FullyQualifiedName</li><li>Name</li><li>ClassName</li><li>Priority</li><li>TestCategory</li></ul> |
| Xunit          | <ul><li>FullyQualifiedName</li><li>DisplayName</li><li>Traits</li></ul> |

Allowed **operators**:
* `=` implies an exact match
* `!=` imples an exact not match
* `~` implies a contains lookup

**Value** is a string. All the lookups are case sensitive.

Expressions can be joined with boolean operators. Following boolean operators are supported:
* `|` implies a boolean `OR`
* `&` implies a boolean `AND`

## Examples
Following examples use `dotnet test`, if you're using `vstest.console.exe` replace `--filter ` with `--testcasefilter:`.

### MSTest
```CSharp
namespace MSTestNamespace
{
    using Microsoft.VisualStudio.TestTools.UnitTesting;

    [TestClass]
    public class UnitTestClass1
    {
        [Priority(2)]
        [TestMethod]
        public void TestMethod1()
        {
        }

        [TestCategory("CategoryA")]
        [Priority(3)]
        [TestMethod]
        public void TestMethod2()
        {
        }
    }
}
```

| Expression | What it does? |
| ---------- | ------------- |
| `dotnet test --filter Method` | Runs tests whose `FullyQualifiedName` contains `Method` |
| `dotnet test --filter Name~TestMethod1` | Runs tests whose name contains `TestMethod1`. |
| `dotnet test --filter ClassName=MSTestNamespace.UnitTestClass1` | Runs tests which are in class  `MSTestNamespace.UnitTestClass1`. <br/>**Note:** ClassName value should have namespace, ClassName=UnitTestClass1 won't work. |
| `dotnet test --filter FullyQualifiedName!=MSTestNamespace.UnitTestClass1.TestMethod1` | Runs all tests excepts `MSTestNamespace.UnitTestClass1.TestMethod1`. |
| `dotnet test --filter TestCategory=CategoryA` | Runs tests which are annotated with `[TestCategory("CategoryA")]` |
| `dotnet test --filter Priority=3` | Runs tests which are annotated with `[Priority(3)]`.**Note:** `Priority~3` is invalid as Priority is int not a string. |

#### Using Logical operators `| and &`

| Expression | What it does? |
| ---------- | ------------- |
| `dotnet test --filter "FullyQualifiedName~UnitTestClass1|TestCategory=CategoryA"` | Runs tests which have `UnitTestClass1` in FullyQualifiedName __or__ TestCategory is CategoryA. |
| `dotnet test --filter "FullyQualifiedName~UnitTestClass1&TestCategory=CategoryA"` | Runs tests which have `UnitTestClass1` in FullyQualifiedName __and__ TestCategory is CategoryA. |
| `dotnet test --filter "(FullyQualifiedName~UnitTestClass1&TestCategory=CategoryA)|Priority=1"` | Runs tests which have either FullyQualifiedName contains `UnitTestClass1` and TestCategory is CategoryA or Priority is 1. |

### xUnit

| Expression | What it does? |
| ---------- | ------------- |
| `dotnet test --filter DisplayName=XUnitNamespace.TestClass1.Test1` | Runs only one test `XUnitNamespace.TestClass1.Test1`. |
| `dotnet test --filter FullyQualifiedName!=XUnitNamespace.TestClass1.Test1` | Runs all tests except `XUnitNamespace.TestClass1.Test1` |
| `dotnet test --filter DisplayName~TestClass1` | Runs tests whose display name containts `TestClass1`. |

#### Using traits for filter
```CSharp
namespace XUnitNamespace
{
    public class TestClass1
    {
        [Trait("Category", "bvt")]
        [Trait("Priority", "1")]
        [Fact]
        public void foo()
        {
        }

        [Trait("Category", "Nightly")]
        [Trait("Priority", "2")]
        [Fact]
        public void bar()
        {
        }
    }
}

```
In above code we defined traits with keys `Category` and `Priority` which can be used for filtering.

| Expression | What it does? |
| ---------- | ------------- |
| `dotnet test --filter XUnit` | Runs tests whose `FullyQualifiedName` contains `XUnit` |
| `dotnet test --filter Category=bvt` | Runs tests which has `[Trait("Category", "bvt")]`. |

#### Using Logical operators `| and &`

| Expression | What it does? |
| ---------- | ------------- |
| `dotnet test --filter "FullyQualifiedName~TestClass1|Category=Nightly"` | Runs tests which has `TestClass1` in FullyQualifiedName __or__ Category is Nightly. |
| `dotnet test --filter "FullyQualifiedName~TestClass1&Category=Nightly"` | Runs tests which has `TestClass1` in FullyQualifiedName __and__ Category is Nightly. |
| `dotnet test --filter "(FullyQualifiedName~TestClass1&Category=Nightly)|Priority=1"` | Runs tests which have either FullyQualifiedName contains `TestClass1` and Category is CategoryA or Priority is 1. |
