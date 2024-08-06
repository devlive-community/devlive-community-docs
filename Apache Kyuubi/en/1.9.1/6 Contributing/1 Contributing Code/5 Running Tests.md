[TOC]


**Kyuubi** can be tested based on [Apache Maven](https://maven.apache.org) and the ScalaTest Maven Plugin,
please refer to the [ScalaTest documentation](https://www.scalatest.org/user_guide/using_the_scalatest_maven_plugin),

## Running Tests Fully

The following is an example of a command to run all the tests:

```bash
./build/mvn clean install
```

## Running Tests for a Module

```bash
./build/mvn clean install -pl kyuubi-common
```

## Running Tests for a Single Test

When developing locally, it’s convenient to run one single test, or a couple of tests, rather than all.

With Maven, you can use the -DwildcardSuites flag to run individual Scala tests:

```bash
./build/mvn clean install -Dtest=none -DwildcardSuites=org.apache.kyuubi.service.FrontendServiceSuite
```

If you want to make a single test that need to integrate with kyuubi-spark-sql-engine module, please build the package
for kyuubi-spark-sql-engine module at first.

You can leverage the ready-made tool for creating a binary distribution.

```bash
./build/dist
```


