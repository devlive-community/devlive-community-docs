[TOC]

Cypher cannot be used in an expression— the query must exist in the `FROM` clause of a query. However, if the cypher query is placed in a subquery, it will behave as any SQL style query.


## Using Cypher with '='

When writing a cypher query that is known to return one column and one row, the '=' comparison operator may be used.


```postgresql
SELECT t.name FROM schema_name.sql_person AS t
where t.name = (
    SELECT a
    FROM cypher('graph_name', $$
    	  MATCH (v)
        RETURN v.name
    $$) as (name varchar(50))
    ORDER BY name
    LIMIT 1);
```


Results:


<table>
  <tr>
   <td><strong>name</strong>
   </td>
   <td><strong>age</strong>
   </td>
  </tr>
  <tr>
   <td>‘Andres’
   </td>
   <td>36
   </td>
  </tr>
  <tr>
   <td colspan="2" >3 row(s) returned
   </td>
  </tr>
</table>


## Working with Postgres's IN Clause

When writing a cypher query that is known to return one column, but may have multiple rows. The `IN` operator may be used.

Query:


```postgresql
SELECT t.name, t.age FROM schema_name.sql_person as t 
where t.name in (
    SELECT *
    FROM cypher('graph_name', $$
        MATCH (v:Person)
        RETURN v.name 
    $$) as (a agtype));
```


Results:


<table>
  <tr>
   <td><strong>name</strong>
   </td>
   <td><strong>age</strong>
   </td>
  </tr>
  <tr>
   <td>‘Andres’
   </td>
   <td>36
   </td>
  </tr>
  <tr>
   <td>‘Tobias’
   </td>
   <td>25
   </td>
  </tr>
  <tr>
   <td>‘Peter’
   </td>
   <td>35
   </td>
  </tr>
  <tr>
   <td colspan="2" >3 row(s) returned
   </td>
  </tr>
</table>



## Working with the Postgres EXISTS Clause

When writing a cypher query that may have more than one column and row returned. The `EXISTS` operator may be used.

Query:


```postgresql
SELECT t.name, t.age
FROM schema_name.sql_person as t
WHERE EXISTS (
    SELECT *
    FROM cypher('graph_name', $$
	  MATCH (v:Person)
        RETURN v.name, v.age
    $$) as (name agtype, age agtype)
    WHERE name = t.name AND age = t.age
);
```


Results:


<table>
  <tr>
   <td><strong>name</strong>
   </td>
   <td><strong>age</strong>
   </td>
  </tr>
  <tr>
   <td>‘Andres’
   </td>
   <td>36
   </td>
  </tr>
  <tr>
   <td>‘Tobias’
   </td>
   <td>25
   </td>
  </tr>
  <tr>
   <td colspan="2" >3 row(s) returned
   </td>
  </tr>
</table>



## Querying Multiple Graphs

There is no restriction to the number of graphs an SQL statement can query. Users may query multiple graphs simultaneously.


```postgresql
SELECT graph_1.name, graph_1.age, graph_2.license_number
FROM cypher('graph_1', $$
    MATCH (v:Person)
    RETURN v.name, v.age
$$) as graph_1(col_1 agtype, col_2 agtype, col_3 agtype)
JOIN cypher('graph_2', $$
    MATCH (v:Doctor)
    RETURN v.name, v.license_number
$$) as graph_2(name agtype, license_number agtype)
ON graph_1.name = graph_2.name
```

Results:


<table>
  <tr>
   <td><strong>name</strong>
   </td>
   <td><strong>age</strong>
   </td>
   <td><strong>license_number</strong>
   </td>
  </tr>
  <tr>
   <td>‘Andres’
   </td>
   <td>36
   </td>
   <td>1234567890
   </td>
  </tr>
  <tr>
   <td colspan="3" >3 row(s) returned
   </td>
  </tr>
</table>




