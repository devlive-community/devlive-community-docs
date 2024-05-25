[TOC]

Welcome to Apache JDO, a project of the [Apache DB project](http://db.apache.org/). Our goal is a thriving community of users and developers of object persistence technology.

Java Data Objects (JDO) is a standard way to access persistent data in databases, using plain old Java objects (POJO) to represent persistent data. The approach separates data manipulation (done by accessing Java data members in the Java domain objects) from database manipulation (done by calling the JDO interface methods). This separation of concerns leads to a high degree of independence of the Java view of data from the database view of the data.

Interfaces are defined for the user’s view of persistence:

*   PersistenceManager: the component responsible for the life cycle of persistent instances, Query factory, and Transaction access

*   Query: the component responsible for querying the datastore and returning persistent instances or values

*   Transaction: the component responsible for initiating and completing transactions


JDO is being developed as a Java Specification Request in the Java Community Process. The original JDO 1.0 is [JSR-12](http://www.jcp.org/en/jsr/detail?id=12) and the current JDO 3.2 is [JSR-243](http://www.jcp.org/en/jsr/detail?id=243).

The Apache JDO project is focused on building the JDO API and the TCK for compatibility testing of JDO implementations. Commercial and open source implementations of JDO are available for relational databases, object databases, and file systems. If you need an implementation for building a JDO application, see [Implementations](https://db.apache.org/jdo/impls.html).

JDO News
--------

**JDO 3.2.1 is released**

> JDO 3.2.1 has been released. This release contains minor bug fixes, such as support for Java 18, fixed warnings when using Java 9, and migration of schema descriptor URLs to db.apache.org. For a complete list of changes (features plus bug fixes) see [JDO 3.2.1 changes](https://issues.apache.org/jira/issues/?jql=project%20%3D%20JDO%20AND%20fixVersion%20%3D%20%22JDO%203.2.1%22). You can download the release from the [downloads page](https://db.apache.org/jdo/downloads.html). You can also use the new release in maven projects simply by referencing the jdo-api artifact in your pom.xml.

**JDO 3.2 is released**

> JDO 3.2 has been released. This release contains minor bug fixes and several new features, such as support for `Optional`, typesafe queries and an upgrade to JDK 1.8. For a complete list of changes (features plus bug fixes) see [JDO 3.2 changes](https://issues.apache.org/jira/issues/?jql=project%20%3D%20JDO%20AND%20fixVersion%20%3D%20%22JDO%203.2%22). You can download the release from the [downloads page](https://db.apache.org/jdo/downloads.html). You can also use the new release in maven projects simply by referencing the jdo-api artifact in your pom.xml.

**JDO 3.1 is released**

> JDO 3.1 has been released. This release contains minor bug fixes. For a complete list of changes (features plus bug fixes) see [JDO 3.1 changes](https://issues.apache.org/jira/issues/?jql=project%20%3D%20JDO%20AND%20fixVersion%20%3D%20%22JDO%203.1%22).

**JDO 3.1-rc1 is released**

> JDO 3.1-rc1 has been released. This release contains minor bug fixes. For a complete list of changes (features plus bug fixes) see [JDO 3.1-rc1 changes](https://issues.apache.org/jira/issues/?jql=project%20%3D%20JDO%20AND%20fixVersion%20%3D%20%22JDO%203.1-rc1%22).

**JDO 3.0.1 is released**

> JDO 3.0.1 has been released. This release contains minor bug fixes. For a complete list of changes (features plus bug fixes) see [JDO 3.0.1 changes](https://issues.apache.org/jira/issues/?jql=project%20%3D%20JDO%20AND%20fixVersion%20%3D%20%22JDO%203%20update%201%20\(3.0.1\)%22).

**JDO 3.0 is released**

> JDO 3.0 has been released. This release contains significant new features for better support of tooling and runtime: enhancer API, dynamic class and metadata generation, locking, database timeouts, query cancel, and exact object ids. For a complete list of changes (features plus bug fixes) see [JDO 3.0 changes](https://issues.apache.org/jira/issues/?jql=project%20%3D%20JDO%20AND%20fixVersion%20%3D%20%22JDO%203%20\(3.0\)%22).

**JDO 2.2 is released**

**JDO 2.1.1 is released**

> JDO 2.1.1 has been released. This is a minor bug fix release.

**JDO 2.1 is released**

> JDO 2.1 has been released. The JDO 2.1 maintenance release provides support for JDK 1.5 features,including the use of annotations as a means of specifying mapping. It also includes many corrections and minor changes. For details, see [Change Log for JSR-000243 JavaTM Data Objects 2.0](http://jcp.org/aboutJava/communityprocess/maintenance/jsr243/243ChangeLog.html)

**JDO 2.0 has been approved by the JCP**

> JDO 2.0 has been released.xs JDO 2.0 builds on JDO 1 and includes many features requested by users:
>
> *   Standard mapping from objects to relational databases
>
> *   Multi-tier support without use of Data Transfer Objects
>
> *   Improved query support including projections and aggregates
>
> *   Stored queries in metadata
>
> *   Deletion by query
>
> *   Optimized fetching of object graphs without writing special queries
>
> *   Extensive List and Map support
>
> *   Lazy loading of large collections
>
> *   Improved support for single-field primary keys
>
> *   Object lifecycle event monitoring
>
> *   Improved support for bidirectional relationships
>

**Java Community Process!**  
JDO is being developed under the Java Community Process. The Apache JDO project is developing the API and the Technology Compatibility Kit for the JDO standard.

**Users!**  
We’d love to have you involved. Check out the [Wiki](http://wiki.apache.org/jdo). Check out the [Specification](http://www.jcp.org/en/jsr/detail?id=243), which has been approved. [Get Involved](https://db.apache.org/jdo/get-involved.html)!

_Archived articles are [here](https://db.apache.org/jdo/newshistory.html)_.
