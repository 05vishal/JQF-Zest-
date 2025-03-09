# JQF + Zest: Feedback-Directed Fuzz Testing for Java

## Introduction

JQF is a **fuzz testing framework for Java** that utilizes **feedback-directed** techniques to generate meaningful test inputs. Unlike traditional random fuzzing, JQF **biases input generation using code coverage information**, making it more effective in finding deep semantic bugs.

JQF integrates with **JUnit-QuickCheck**, allowing developers to write **parameterized JUnit test methods** as fuzz drivers.

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Installation](#installation)
- [Writing a Fuzz Test](#writing-a-fuzz-test)
- [Running JQF](#running-jqf)
- [Why Use JQF?](#why-use-jqf)
- [References](#references)
- [License](#license)

## Features

- **Coverage-Guided Fuzzing:** Uses execution feedback to generate inputs that explore more program paths.
- **Semantic Fuzzing with Zest:** Prioritizes generating valid inputs that satisfy structural and semantic properties.
- **Modular Fuzzing Frontends:** Supports multiple fuzzing approaches:
  - **Zest** (default) – Structure-aware fuzzing.
  - **AFL** – Binary fuzzing (like American Fuzzy Lop).
  - **PerfFuzz** – Complexity-guided fuzzing.
  - **RLCheck** – Reinforcement learning-based fuzzing.
  - **Mu2** – Mutation-analysis-guided fuzzing.
- **Automated Test Case Generation:** Generates and refines test cases automatically.
- **Structured Input Support:** Can fuzz **JSON, XML, SQL queries, JavaScript programs, JVM class files**, etc.

## Installation

To install JQF, use the following steps:

```bash
# Clone the JQF repository
git clone https://github.com/rohanpadhye/JQF.git
cd JQF

# Build JQF using Maven
mvn install -DskipTests
```

## Writing a Fuzz Test

JQF uses **JUnit-based fuzz tests**. Below is an example:

```java
@RunWith(JQF.class)
public class ExampleTest {
    @Fuzz
    public void testExample(Map<String, Integer> map, String key) {
        assumeTrue(map.containsKey(key));
        assertTrue(map.get(key) != null);
    }
}
```

This method will be repeatedly executed with automatically generated values for `map` and `key`.

## Running JQF

To run fuzzing using the **Zest** guidance, use:

```bash
mvn jqf:fuzz -Dclass=ExampleTest -Dmethod=testExample
```

JQF will generate test cases and report any assertion violations found.

## Why Use JQF?

✔ **Finds Deep Bugs:** Identifies logical flaws beyond simple error handling. ✔ **More Efficient than Random Testing:** Uses feedback-driven input generation. ✔ **Automates Input Generation:** No need to manually write extensive test cases. ✔ **Supports Complex Inputs:** Can fuzz structured data like JSON, XML, and SQL queries. ✔ **Used in Real-World Projects:** Found bugs in **OpenJDK, Apache Maven, Google Closure Compiler**, and more.

## References

- **Zest Research Paper:** [Semantic Fuzzing with Zest (ISSTA 2019)](https://doi.org/10.1145/3293882.3330576)
- **JQF Tool Paper:** [JQF: Coverage-Guided Property-Based Testing in Java (ISSTA 2019)](https://doi.org/10.1145/3293882.3339002)
- **Official Repository:** [JQF on GitHub](https://github.com/rohanpadhye/JQF)

## License

JQF is licensed under the **MIT License**.

---

**Contributions & Issues:** If you find a bug or have feature requests, feel free to open an issue on the [GitHub repository](https://github.com/rohanpadhye/JQF/issues).

