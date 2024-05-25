[TOC]

To understand the JDO Query [![Javadoc](https://db.apache.org/jdo/images/javadoc.png)](https://db.apache.org/jdo/api32/apidocs/javax/jdo/Query.html) API we firstly need to look at a typical Query.

Let’s create a JDOQL string-based query to highlight its usage

```java
Query q = pm.newQuery("SELECT FROM mydomain.Product p WHERE p.price <= :threshold ORDER BY p.price ASC");
List results = q.execute(my_threshold);
```

In this Query, we implicitly select the *JDOQL* language by just passing in a query string to the method *PersistenceManager.newQuery(String)*, and the query is specified to return all objects of type *Product* (or subclasses) which have the price less than or equal to some threshold value and ordering the results by the price. We’ve specified the query like this because we want to pass the threshold value in as a parameter (so maybe running it once with one value, and once with a different value). We then set the parameter value of our *threshold* parameter. The Query is then executed to return a List of results. The example is to highlight the typical methods specified for a (JDOQL) string-based Query.

### Creating a query

The principal ways of creating a query are

+   Specifying the query language, and using a single-string form of the query

```java
Query q = pm.newQuery("javax.jdo.query.JDOQL",
    "SELECT FROM mydomain.MyClass WHERE field2 < threshold PARAMETERS java.util.Date threshold");
```

or alternatively

```java
Query q = pm.newQuery("SQL", "SELECT * FROM MYTABLE WHERE COL1 == 25);
```

+   A ["named" query](#named), (pre-)defined in metadata (refer to metadata docs).

```java
Query<MyClass> q = pm.newNamedQuery(MyClass.class, "MyQuery1");
```

+   JDOQL : Use the [single-string]($JDOQL) form of the query

```java
Query q = pm.newQuery("SELECT FROM mydomain.MyClass WHERE field2 < threshold PARAMETERS java.util.Date threshold");
```

+   JDOQL : Use the [declarative API]($JDOQL) to define the query

```java
Query<MyClass> q = pm.newQuery(MyClass.class);
q.setFilter("field2 < threshold");
q.declareParameters("java.util.Date threshold");
```

+   JDOQL : Use the [Typed Query API](https://db.apache.org/jdo/jdoql.html#jdoql_typed) to define the query

```java
JDOQLTypedQuery<MyClass> q = pm.newJDOQLTypedQuery(MyClass.class);
QMyClass cand = QMyClass.candidate();
List<Product> results = q.filter(cand.field2.lt(q.doubleParameter("threshold"))).executeList();
```

### Closing a query

When a query is executed it will have access to the results of that query. Each time it is executed (maybe with different parameters) it will have separate results. This can consume significant resources if the query returned a lot of records.

You close a query (and all query results) like this

```java
q.close();
```

If you just wanted to close a specific query result you would call

```java
q.close(queryResult);
```

where the *queryResult* is what you were returned from executing the query.

### Named Query

With the JDO Query API you can either define a query at runtime, or define it in the MetaData/annotations for a class and refer to it at runtime using a symbolic name. This second option means that the method of invoking the query at runtime is much simplified. To demonstrate the process, lets say we have a class called *Product* (something to sell in a store). We define the JDO Meta-Data for the class in the normal way, but we also have some query that we know we will require, so we define the following in the Meta-Data.

```xml
<package name="mydomain">
    <class name="Product">
        ...
        <query name="SoldOut" language="javax.jdo.query.JDOQL"><![CDATA[
        SELECT FROM mydomain.Product WHERE status == "Sold Out"
        ]]></query>
    </class>
</package>
```

So we have a JDOQL query called "SoldOut" defined for the class *Product* that returns all Products (and subclasses) that have a *status* of "Sold Out". Out of interest, what we would then do in our application to execute this query woule be

```java
Query<Product> q = pm.newNamedQuery(mydomain.Product.class,"SoldOut");
List<Product> results = q.executeList();
```

The above example was for the JDOQL object-based query language. We can do a similar thing using SQL, so we define the following in our MetaData for our *Product* class

```xml
<jdo>
    <package name="mydomain">
        <class name="Product">
            ...
            <query name="PriceBelowValue" language="javax.jdo.query.SQL"><![CDATA[
            SELECT NAME FROM PRODUCT WHERE PRICE < ?
            ]]></query>
        </class>
    </package>
</jdo>
```

So here we have an SQL query that will return the names of all Products that have a price less than a specified value. This leaves us the flexibility to specify the value at runtime. So here we run our named query, asking for the names of all Products with price below 20 euros.

```java
Query<Product> q = pm.newNamedQuery(mydomain.Product.class, "PriceBelowValue");
q.setParameters(20.0);
List<Product> results = q.executeList();
```

All of the examples above have been specifed within the `<class>` element of the MetaData. You can, however, specify queries below `<jdo>` in which case the query is not scoped by a particular candidate class. In this case you must put your queries in any of the following MetaData files

```xml
/META-INF/package.jdo
/WEB-INF/package.jdo
/package.jdo
/META-INF/package-{mapping}.orm
/WEB-INF/package-{mapping}.orm
/package-{mapping}.orm
/META-INF/package.jdoquery
/WEB-INF/package.jdoquery
/package.jdoquery
```

#### Saving a Query as a Named Query

JDO also allows you to create a query, and then save it as a "named" query for later reuse. You do this as follows

```java
Query q = pm.newQuery("SELECT FROM mydomain.Product p WHERE ...");
q.saveAsNamedQuery("MyQuery");
```

and you can thereafter access the query via

```java
Query q = pm.newNamedQuery(Product.class, "MyQuery");
```

### Query Extensions

The JDO query API allows implementations to support "extensions" and provides a simple interface for enabling the use of such extensions on queries. An extension specifies additional information to the query mechanism about how to perform the query. Individual extensions will be explained later in this guide.

You set an extension like this

```java
q.extension("extension_name", value);
```

```java
Map exts = new HashMap();
exts.put("extension1", value1);
exts.put("extension2", value2);
q.extensions(exts);
```

The Query API also has methods *setExtensions* and *addExtension* that are from the original version of the API, but function the same as these methods quoted.

<table><tbody><tr><td class="icon"><i class="fa icon-note" title="Note"></i></td><td class="content">Refer to the documentation of your JDO provider for what extensions are supported.</td></tr></tbody></table>

### Setting query parameters

Queries can be made flexible and reusable by defining parameters as part of the query, so that we can execute the same query with different sets of parameters and minimise resources.

```java
// JDOQL Using named parameters
Query<Product> q = pm.newQuery(Product.class);
q.setFilter("this.name == :name && this.serialNo == :serial");

Map params = new HashMap();
params.put("name", "Walkman");
params.put("serial", "123021");
q.setNamedParameters(params);


// JDOQL Using numbered parameters
Query<Product> q = pm.newQuery(Product.class);
q.setFilter("this.name == ?1 && this.serialNo == ?2");

q.setParameters("Walkman", "123021");
```

Alternatively you can specify the query parameters in the *execute* method call.

### Compiling a query

An intermediate step once you have your query defined, if you want to check its validity, is to *compile* it. You do this as follows

```java
q.compile();
```

If the query is invalid, then a JDOException will be thrown.

### Executing a query

So we have set up our query. We now execute it. We have various methods to do this, depending on what result we are expecting etc

```auto
// Simple execute
Object result = q.execute();

// Execute with 1 parameter passed in
Object result = q.execute(paramVal1);

// Execute with multiple parameters passed in
Object result = q.execute(paramVal1, paramVal2);

// Execute with an array of parameters passed in (positions match the query parameter position)
Object result = q.executeWithArray(new Object[]{paramVal1, paramVal2});

// Execute with a map of parameters keyed by their name in the query
Object result = q.executeWithMap(paramMap);

// Execute knowing we want to receive a list of results
List results = q.executeList();

// Execute knowing there is 1 result row
Object result = q.executeUnique();

// Execute where we want a list of results and want each result row of a particular type
List<ResultClass> results = q.executeResultList(ResultClass.class);

// Execute where we want a single result and want the result row of a particular type
ResultClass result = q.executeResultUnique(ResultClass.class);
```

### Result Class

By default a JDO query of whatever language will return a result matching the result clause. You can override this if you wish by specifying a result class. If your query has only a single row in the results then you will get an object of your result class back, otherwise you get a List of result class objects. The *Result Class* has to meet certain requirements. These are

+   Can be one of Integer, Long, Short, Float, Double, Character, Byte, Boolean, String, java.math.BigInteger, java.math.BigDecimal, java.util.Date, java.sql.Date, java.sql.Time, java.sql.Timestamp, java.time.LocalDate, java.time.LocalTime, java.time.LocalDateTime, or Object\[\]
+   Can be a user-defined class, that has either a constructor taking arguments of the same type as those returned by the query (in the same order), or has a public put(Object, Object) method, or public setXXX() methods, or public fields.

Please look at the specific help for the query language you are using for details of a user-defined result class.

### Controlling the execution : FetchPlan

When a Query is executed it executes in the datastore, which returns a set of results. Your JDO provider could clearly read all results from this ResultSet in one go and return them all to the user, or could allow control over this fetching process. JDO provides a *fetch size* on the *Fetch Plan* to allow this control. You would set this as follows

```auto
Query q = pm.newQuery(...);
q.getFetchPlan().setFetchSize(FetchPlan.FETCH_SIZE_OPTIMAL);
```

*fetch size* has 3 possible values.

+   **FETCH\_SIZE\_OPTIMAL** - allows your JDO provider full control over the fetching. In this case your JDO provider will fetch each object when they are requested, and then when the owning transaction is committed will retrieve all remaining rows (so that the Query is still usable after the close of the transaction).
+   **FETCH\_SIZE\_GREEDY** - Your JDO provider will read all objects in at query execution. This can be efficient for queries with few results, and very inefficient for queries returning large result sets.
+   **A positive value** - Your JDO provider will read this number of objects at query execution. Thereafter it will read the objects when requested.

In addition to the number of objects fetched, you can also control which fields are fetched for each object of the candidate type. This is controlled via the [FetchPlan]($Fetch-Plan-Groups).

### ignoreCache(), setIgnoreCache()

The ignoreCache option setting specifies whether when processing the query results it should check for the retrieved objects in the cache.

```java
q.ignoreCache(true);
```

### Control over locking of fetched objects

JDO allows control over whether objects found by a query are locked during that transaction so that other transactions can’t update them in the meantime. To do this you would do

```java
Query q = pm.newQuery(...);
q.serializeRead(true);
```

In addition you can perform this on a per-transaction basis by doing

```java
tx.setSerializeRead(true);
```

<table><tbody><tr><td class="icon"><i class="fa icon-note" title="Note"></i></td><td class="content">If the datastore in use doesn’t support locking of objects then this will do nothing</td></tr></tbody></table>

### Timeout on query execution for reads

```java
q.datastoreReadTimeoutMillis(1000);
```

*Sets the timeout for this query (in milliseconds).* Will throw a JDOUnsupportedOperationException if the query implementation doesn’t support timeouts (for the current datastore).

### Timeout on query execution for writes

```java
q.datastoreWriteTimeoutMillis(1000);
```

*Sets the timeout for this query (in milliseconds) when it is a delete/update.* Will throw a JDOUnsupportedOperationException if the query implementation doesn’t support timeouts (for the current datastore).
