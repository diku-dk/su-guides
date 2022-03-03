# NUnit Guide
These are some guidelines on how to better use the NUnit framework.
We provide some code examples, as well as make some arguments about how to
create well-structured tests.


### Providing arguments
You can provide arguments to a test method by using the `[TestCase]` attribute.
```csharp
namespace Tests;

using NUnit.Framework;

[TestFixture]
public class Test {
    
    [TestCase(12, 45, 13)]
    [TestCase(24, 90, 26)]
    [TestCase(48, 180, 52)]
    public void ParameterizedSameTest (int a, int b, int c) {
        Assert.AreEqual(SomeMethod(a, b), c);
    }
    // This test is run 3 times
}
```


### Setup
NUnit provides the `SetUp` attribute that can be attached to any method within
an NUnit test class. This method will then be called automatically prior to any
other test method that you have defined within the same class.
```csharp
namespace Tests;

using NUnit.Framework;

[TestFixture]
public class Test
{
    private int counter;
    
    [SetUp]
    public void Init() {
        this.counter = 0;
    }
    
    [Test(), Repeat(100)]
    public void TestCounter() {
        counter++;
        Assert.AreEqual(counter, 1);
    }
    // this test will be run 100 times
}

```


### Constraint-based assertion model
The idea is to provide constraints to the assertion function.
Use `Assert.That` to provide an assertion model that expects a constraint,
then use `Is.<...>` to provide the constraint.
```csharp
namespace Tests;

using NUnit.Framework;

[TestFixture]
public class Test {

    [Test]
    public void ConstraintNullTest() {
        var x = SomeObjectCreatorMethod();
        Assert.That (x, Is.Not.Null);
    }
    
    [Test]
    public void ConstraintNegativeTest() {
        var x = Factorial(-23);
        Assert.That (x, Is.Positive);
    }
}
```