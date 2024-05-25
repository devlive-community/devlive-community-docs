[TOC]

As we have described earlier, JDO allows access to many query languages to give the user full flexibility over what they utilise. To demonstrate how you would utilise a different query language with JDO, take the example that you are using an RDBMS (i.e your JDO provider supports RDBMS) it is sometimes desirable to query using **SQL**.

> Please be aware that the SQL query that you invoke has to be valid for your RDBMS, and that the SQL syntax differs across almost all RDBMS.

To utilise **SQL** syntax in queries, you create a Query as follows

```sql
Query q = pm.newQuery("javax.jdo.query.SQL", the_sql_query);
```

You have several forms of SQL queries, depending on what form of output you require.

+   **No candidate class and no result class** - the result will be a List of Objects (when there is a single column in the query), or a List of Object\[\]s (when there are multiple columns in the query)
+   **Candidate class specified, no result class** - the result will be a List of candidate class objects, or will be a single candidate class object (when you have specified "unique"). The columns of the querys result set are matched up to the fields of the candidate class by name. You need to select a minimum of the PK columns in the SQL statement.
+   **No candidate class, result class specified** - the result will be a List of result class objects, or will be a single result class object (when you have specified "unique"). Your result class has to abide by the rules of JDO result classes (see [Result Class specification]($Query-API)) - this typically means either providing public fields matching the columns of the result, or providing setters/getters for the columns of the result.
+   **Candidate class and result class specified** - the result will be a List of result class objects, or will be a single result class object (when you have specified "unique"). The result class has to abide by the rules of JDO result classes (see [Result Class specification]($Query-API)).

### Setting candidate class

If you want to return instances of persistable types, then you can set the candidate class.

```java
Query query = pm.newQuery("javax.jdo.query.SQL", "SELECT MY_ID, MY_NAME FROM MYTABLE");
query.setClass(MyClass.class);
List<MyClass> results = query.executeList();
```

### Unique results

If you know that there will only be a single row returned from the SQL query then you can set the query as *unique*. Note that the query will return null if the SQL has no results.

Sometimes you know that the query can only every return 0 or 1 objects. In this case you can simplify your job by adding

```java
// Using traditional JDO Query API
Query query = pm.newQuery("javax.jdo.query.SQL", "SELECT MY_ID, MY_NAME FROM MYTABLE");
query.setClass(MyClass.class);
query.setUnique(true);
MyClass obj = (MyClass) query.execute();

// Using JDO3.2 Query API
Query query = pm.newQuery("javax.jdo.query.SQL", "SELECT MY_ID, MY_NAME FROM MYTABLE");
query.setClass(MyClass.class);
MyClass obj = query.executeUnique();
```

### Defining a result type

If you want to dump each row of the SQL query results into an object of a particular type then you can set the result class.

```java
// Using traditional JDO Query API
Query query = pm.newQuery("javax.jdo.query.SQL", "SELECT MY_ID, MY_NAME FROM MYTABLE");
query.setResultClass(MyResultClass.class);
List<MyResultClass> results = (List<MyResultClass>) query.execute();


// Using JDO3.2 Query API
Query query = pm.newQuery("javax.jdo.query.SQL", "SELECT MY_ID, MY_NAME FROM MYTABLE");
List<MyResultClass> results = query.executeResultList(MyResultClass.class);
```

The *Result Class* has to meet certain requirements. These are

+   Can be one of Integer, Long, Short, Float, Double, Character, Byte, Boolean, String, java.math.BigInteger, java.math.BigDecimal, java.util.Date, java.sql.Date, java.sql.Time, java.sql.Timestamp, or Object\[\]
+   Can be a user defined class, that has either a constructor taking arguments of the same type as those returned by the query (in the same order), or has a public put(Object, Object) method, or public setXXX() methods, or public fields.

For example, if we are returning two columns like above, an *int* and a *String* then we define our result class like this

```java
public class MyResultClass
{
    protected int id = 0;
    protected String name = null;

    public MyResultClass(int id, String name)
    {
        this.id = id;
        this.name = name;
    }

    ...
}
```

So here we have a result class using the constructor arguments. We could equally have provided a class with public fields instead, or provided *setXXX* methods, or just provide a *put* method. They all work in the same way.

### Parameters

In JDO SQL queries can have parameters but must be *positional*. This means that you do as follows

```java
Query q = pm.newQuery("javax.jdo.query.SQL", "SELECT col1, col2 FROM MYTABLE WHERE col3 = ? AND col4 = ? and col5 = ?");
List results = q.setParameters(val1, val2, val3).executeList();
```

So we used traditional JDBC form of parametrisation, using "?".
