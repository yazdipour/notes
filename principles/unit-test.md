# Unit Test

## Process

1. Write Failing Test
2. Code to make it pass
3. Refactor Code

## Test Structure

Arrange - Act - Assert

## Naming

`theFuncName_scenario_expexctedOutCome()`

## MSTest

```c#
[TestClass]
class x{
    [ClassInitialize]
    public void static BarClass(TestContext tc){} // This method executes before any of test methods in class - ONLY ONCE

    [ClassCleanup]
    public void static BazClass(){} // This method executes after test last method in class - ONLY ONCE

    [TestInitialize]
    void Bar(){} // This method executes before each method

    [TestCleanUp]
    void Baz(){} // This method executes after each method

    [TestMethod]
    void Foo(){}
```

## NUnit

1. Install NUnit Nuget
2. Install NUnit Test Adapter Nuget (Help VS to Understand NUnit)

```c#
[TestFixture]
class x{
    [Test]
    void Foo([Values(1,3,2)] int arg){
        var output = TheClass.PlusOne(arg);
        Assert.AreEqual(arg+1, output);
    }
```
