# DatAssA4

This project is based on the movie dataset example, found in the neo4j localhost browser. We have added the file to create the database.

### A) Identify the most important nodes, based on their relationships
If the project is loaded in, use the following command to find the most important nodes. We have limited it to 5, and done it descending, giving you the most common node as the first.
```sql
MATCH (nodes)-[relations]-() RETURN nodes, COUNT(*) as relations ORDER BY COUNT(*) DESC LIMIT 5
```

### B) Detect the close connected communities of nodes
```sql
MATCH (u:Person)
WITH u
ORDER BY u.louvain
WITH  u.louvain AS community, collect(u.name) AS people
RETURN community, people[..10]
ORDER BY size(people) DESC
```

### C) Discover similarities between nodes, based on their properties or behaviour

In order to find similarities between the different nodes i have tried to take one movie title as an observation and use the different aggregating functions to find the different data distribution between the nodes.

First
```sql
MATCH (m: Movie {title: "A Few Good Men"}) WITH m MATCH (m) <- [:ACTED_IN] - (p:Person) RETURN min(m.released - p.born), avg(m.released - p.born), max(m.released - p.born)
````

`min(m.released)	avg(m.released)	max(m.released)
1975	1998.2894736842106	2012`

```sql
MATCH (m: Movie {title: "A Few Good Men"}) WITH m MATCH (m) <- [:ACTED_IN] - (p:Person) RETURN min(m.released - p.born), avg(m.released - p.born), max(m.released - p.born)
```

Afterwards we try to take the difference in the age between the actors who also acted in the movie, and use the aggregating function on those values. 
Using these functions, we can see the similarites in between the nodes. 




### D) Find available routes or optimal paths between the nodes
Run the following command to find the shortest path between 2 nodes (actors/directors/movies) of your choice by replacing the names.
```sql
MATCH p=shortestPath((robert:Person {name:"Robert Zemeckis"})-[*]-(meg:Person {name:"Meg Ryan"}))
RETURN p
```
