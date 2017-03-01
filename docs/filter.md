# TestCase filter
This article will help you to selectively execute test based on filtering condition through `--filter` for `dotnet test` and `--testcasefilter` for `vstest.console.exe`.

### Syntax
   `--filter <Expression>` or
   `--testcasefilter:<Expression>`

Expression is of the format __\<property>Operator\<value>[|&\<Expression>]__
where Operator is one of __=, != or ~__  (Operator ~ has 'contains'
semantics and is applicable for string properties like FullyQualifiedName).
Parenthesis () can be used to group sub-expressions.

`--filter` properties depends on adapter.

- MSTest supports TestCategory, Priority, FullyQualifiedName, Name and ClassName.

- xUnit supports DisplayName, FullyQualifiedName and traits.

## Examples
   __Following example are for `dotnet test` case, for `vstest.console.exe` case replace `--filter ` with `--testcasefilter:`__.

### MSTest
```
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
- `dotnet test --filter Name~TestMethod1`

   Runs tests whose name contains `TestMethod1`.

- `dotnet test --filter ClassName=MSTestNamespace.UnitTestClass1`

   Runs tests which are in class  `MSTestNamespace.UnitTestClass1`.
   **Note:** ClassName value should have namespace, ClassName=UnitTestClass1 won't work.

- `dotnet test --filter FullyQualifiedName!=MSTestNamespace.UnitTestClass1.TestMethod1`

   Runs all tests excepts `MSTestNamespace.UnitTestClass1.TestMethod1`.

- `dotnet test --filter TestCategory=CategoryA`

   Runs tests which are annotated with `[TestCategory("CategoryA")]`

- `dotnet test --filter Priority=3`

   Runs tests which are annotated with `[Priority(3)]`.**Note:** `Priority~3` is invalid as Priority is int not a string.

#### Using Logical operators `| and &`

- `dotnet test --filter "FullyQualifiedName~UnitTestClass1|TestCategory=CategoryA"`

   Runs tests which have `UnitTestClass1` in FullyQualifiedName __or__ TestCategory is CategoryA.

- `dotnet test --filter "FullyQualifiedName~UnitTestClass1&TestCategory=CategoryA"`

   Runs tests which have `UnitTestClass1` in FullyQualifiedName __and__ TestCategory is CategoryA.

-  `dotnet test --filter "(FullyQualifiedName~UnitTestClass1&TestCategory=CategoryA)|Priority=1"`

   Runs tests which have either FullyQualifiedName contains `UnitTestClass1` and TestCategory is CategoryA or
   Priority is 1.

### xUnit

- `dotnet test --filter DisplayName=XUnitNamespace.TestClass1.Test1`

  Runs only one test `XUnitNamespace.TestClass1.Test1`.

- `dotnet test --filter FullyQualifiedName!=XUnitNamespace.TestClass1.Test1`

   Runs all tests except `XUnitNamespace.TestClass1.Test1`

- `dotnet test --filter DisplayName~TestClass1`

   Runs tests whose display name containts `TestClass1`.

#### Using traits for filter
```
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

- `dotnet test --filter Category=bvt`

   Runs tests which has `[Trait("Category", "bvt")]`.

#### Using Logical operators `| and &`

- `dotnet test --filter "FullyQualifiedName~TestClass1|Category=Nightly"`

   Runs tests which has `TestClass1` in FullyQualifiedName __or__ Category is Nightly.

- `dotnet test --filter "FullyQualifiedName~TestClass1&Category=Nightly"`

   Runs tests which has `TestClass1` in FullyQualifiedName __and__ Category is Nightly.

-  `dotnet test --filter "(FullyQualifiedName~TestClass1&Category=Nightly)|Priority=1"`

   Runs tests which have either FullyQualifiedName contains `TestClass1` and Category is CategoryA or
   Priority is 1.
