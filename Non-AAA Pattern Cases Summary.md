# Non-AAA Pattern Cases Summary

Author: Chenhao Wei

## Not Having Assert

### Try Catch

Try-catch structure will mask the assert and error report, should add Assert inside catch branch.

### Print

Print function should be replaced with String Assert

## Multiple AAA

Test the same function with different inputs, so we should split it into single AAA unit tests.

* Repeat in AR AC AS order.
* Single AR section with repeating AC AS section.[easy]
* ~~Single AS section with repeating AR AC section.~~[More like Integration Test]

## Not Having Arrange

Static Method do not need the arrangement.

## Assert Before Action (One type of AAA)

All of these kind of cases are based on JUnit Rule System. Its assert procedure is based on the Try-Throw-Exception structure.

### Expected Annotation(A[s]AA)

````java
@Test(expected = AccumuloException.class)
public void testNoFiles() throws Exception {
    try (AccumuloClient client = Accumulo.newClient().from(getClientProps()).build()) {
      // Should throw an error as this property can't be changed in ZooKeeper
      client.instanceOperations().setProperty(Property.GENERAL_RPC_TIMEOUT.getKey(), "60s");
    }
  }
````

The Assert shown before the function itself.(Our parser can parse it into the case file.)

### Expected Rule(AA[s]A)

```java
    thrown.expect(IllegalStateException.class);
    thrown.expectMessage("consecutive " + LogEvents.COMPACTION_FINISH.name());
```

The Assert is stated right before the action.

## ~~Bad Name~~

~~The purpose is not stated in the case name. Using the name like `test2` or `testFields`.~~

~~Need to be rename with its action.~~

## Mock

TBD