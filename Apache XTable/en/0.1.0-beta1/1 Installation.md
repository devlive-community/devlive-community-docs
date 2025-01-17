[TOC]

This page covers the essential steps to setup OneTable in your environment.

## Pre-requisites
1. Building the project requires Java 11 and Maven to be setup and configured using PATH or environment variables.
2. Clone the OneTable project GitHub [repository](https://github.com/onetable-io/onetable) in your environment.

## Steps
#### Building the project
Once the project is successfully cloned in your environment, you can build the jars from the source using the below command.

```shell
mvn clean package
```
For skipping the tests while building, add `-DskipTests`.

```shell
mvn clean package -DskipTests
```

For more information on the steps, follow the project's GitHub [README.md](https://github.com/onetable-io/onetable/blob/main/README.md)

## Next Steps
See the [Quickstart]($Creating-Your-First-Interoperable-Table) guide to learn to use OneTable to add interoperability between
different table formats.