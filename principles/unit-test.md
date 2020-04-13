# Unit Test

Unit tests are low-level tests that focus on testing a specific part of our system. They are cheap to write and fast to run. Test failures should provide enough contextual information to pinpoint the source of the error. These tests are typically written by developers during the Implementation phase of the Software Development Life Cycle (SDLC).

Unit tests should be independent and isolated; interacting with external components increases both the scope of our tests and the time it takes for tests to run. As we will see in a future post, replacing dependencies with test doubles results in deterministic tests that are quick to run.

## Process

1. Write Failing Test
2. Code to make it pass
3. Refactor Code

## Unit Test Example

```py
def find_top_word(words)
    # Return most common word & occurrences
    word_counter = Counter(words)
    return word_counter.most_common(1)[0]

def test_find_top_word():
    words = ["foo", "bar", "bat", "baz", "foo", "baz", "foo"]
    result = find_top_word(words)

    assert result[0] == "foo"
    assert result[1] == 3
```

## Test Structure

### AAA

- _Arrange_: The data used in a test should not depend on the environment in which the test is running. All the data needed for a test should be arranged as part of the test.
- _Act_: Invoke the actual method under test.
- _Assert_: A test method should test for a single logical outcome, implying that typically there
  should be only a single logical assert. A logical assert could have multiple physical asserts as
  long as all the asserts test the state of a single object. In a few cases, an action can update
  multiple objects.

### Given-When-Then (GWT)

GWT is widely used in Behavior Driven Development (BDD).

GWT provides a useful abstraction for separating the different phases of our test:

- Given a set of pre-conditions
- When we perform an action on the SUT
- Then our post-conditions should be as follows

```py
def test_find_top_word():
    # Given a list of word
    words = ["foo", "bar", "bat", "baz", "foo", "baz", "foo"]

    # When we run the function over the list
    result = find_top_word(words)

    # Then we should see `foo` occurring 3 times
    assert result[0] == "foo"
    assert result[1] == 3
```

## F.I.R.S.T Principles

### FAST

A developer should not hesitate to run the tests as they are slow.

### ISOLATED/INDEPENDENT

A test method should do the 3 As => Arrange, Act, Assert

### REPEATABLE

A test method should NOT depend on any data in the environment/instance in which it is running.
Deterministic results - should yield the same results every time and at every location where they run.
No dependency on date/time or random functions output.
Each test should setup or arrange it's own data.
What if a set of tests need some common data? Use Data Helper classes that can setup this data for re-usability.### SELF-VALIDATING

No manual inspection required to check whether the test has passed or failed.

### THOROUGH/TIMELY

- Should cover every use case scenario and NOT just aim for 100% coverage.
- Tests for corner/edge/boundary values.
- Tests for large data sets - this will test runtime and space complexity.
- Tests for security with users having different roles - behavior may be different based on user's role.
- Tests for large values - overflow and underflow errors for data types like integer.
- Tests for exceptions and errors.
- Tests for illegal arguments or bad inputs.

## Naming Conventions

```java
<ObjectName>TriggerTest
<ClassName>ControllerTest
<ClassName>Test
test<methodUnderTest>_<shortUseCaseScenarioName>_<ExpectedResult>
eg: testTheFuncName_scenario_expexctedOutCome()
```

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
