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
    [TestMethod]
    void foo(){}
```

## NUnit

1. Install NUnit Nuget
2. Install NUnit Test Adapter Nuget (Help VS to Understand NUnit)

```c#
[TestFixture]
class x{
    [Test]
    void foo(){}
```
