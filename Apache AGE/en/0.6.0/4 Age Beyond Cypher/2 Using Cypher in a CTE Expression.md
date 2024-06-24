[TOC]

There are no restrictions to using Cypher with CTEs ([Common Table Expressions](https://www.postgresql.org/docs/current/queries-with.html)).

Query:


```postgresql
WITH graph_query as (
    SELECT *
        FROM cypher('graph_name', $$
        MATCH (n)
        RETURN n.name, n.age
    $$) as (name agtype, age agtype)
)
SELECT * FROM graph_query;
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

