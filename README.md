# Boundary Value Test Case Generator

A Java console application that turns integer parameter ranges into structured CSV test suites. Developed as a software testing exercise, it makes three boundary-oriented test design strategies concrete and inspectable.

## Test generation strategies

| Strategy | Values explored | Number of cases for `n` parameters |
| --- | --- | --- |
| Normal boundary value checking | Minimum, minimum + 1, maximum − 1, maximum; other parameters held nominal | `4n + 1` |
| Robust boundary value checking | Normal boundaries plus values immediately outside each range | `6n + 1` |
| Worst-case boundary combinations | Cartesian product of five values per parameter, including nominal | `5^n` |

The nominal value uses integer midpoint arithmetic. CSV rows include a test case identifier and parameter values; an `ExpectedValue` header provides a place to associate the generated inputs with a test oracle.

## Run

Use a JDK and run from the `BVC` directory, where the application resolves its `files/` output folder:

```bash
cd BVC
javac -d /tmp/bvc-classes src/MainClass.java
java -cp /tmp/bvc-classes MainClass
```

Enter the parameter count, then the minimum and maximum for each parameter. For example, two parameters with ranges `1 10` and `20 30` produce 9 normal, 13 robust, and 25 worst-case combinations.

The program writes `files/BVC.csv`, `files/robust.csv`, and `files/worst.csv`. Existing examples are included in that directory.

## Implementation

[MainClass.java](BVC/src/MainClass.java) handles interactive input, constructs the three suites, and serializes them with Java's buffered file APIs. Worst-case enumeration uses positional indexing over each parameter's five candidate values, demonstrating systematic combinatorial test generation without external libraries.
