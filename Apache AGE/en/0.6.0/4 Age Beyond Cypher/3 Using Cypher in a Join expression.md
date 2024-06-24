[TOC]

A Cypher query can be part of a `JOIN` clause.


```
Developers Note
Cypher queries using the CREATE, SET, REMOVE clauses cannot be used in sql queries with JOINs, as they affect the Postgres transaction system. One possible solution is to protect the query with CTEs. See the subsection Using CTEs with CREATE, REMOVE, and SET for more details.
```


Query:


```postgresql
SELECT id, 
    graph_query.name = t.name as names_match,
    graph_query.age = t.age as ages_match
FROM schema_name.sql_person AS t
JOIN cypher('graph_name', $$
        MATCH (n:Person)
        RETURN n.name, n.age, id(n)
$$) as graph_query(name agtype, age agtype, id agtype)
ON t.person_id = graph_query.id
```


Results:


<table>
  <tr>
   <td><strong>id</strong>
   </td>
   <td><strong>names_match</strong>
   </td>
   <td><strong>ages_match</strong>
   </td>
  </tr>
  <tr>
   <td>1
   </td>
   <td>True
   </td>
   <td>True
   </td>
  </tr>
  <tr>
   <td>2
   </td>
   <td>False
   </td>
   <td>True
   </td>
  </tr>
  <tr>
   <td>3
   </td>
   <td>True
   </td>
   <td>False
   </td>
  </tr>
  <tr>
   <td colspan="3" >3 row(s) returned
   </td>
  </tr>
</table>
