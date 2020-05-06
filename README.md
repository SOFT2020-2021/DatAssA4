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


### D) Find available routes or optimal paths between the nodes
Run the following command to find the shortest path between 2 nodes (actors/directors/movies) of your choice by replacing the names.
```sql
MATCH p=shortestPath((robert:Person {name:"Robert Zemeckis"})-[*]-(meg:Person {name:"Meg Ryan"}))
RETURN p
```
