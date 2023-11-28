# Introduction to Graph Databases with Neo4j

## Overview of Graph Databases
Graph databases are a type of NoSQL database, which designed to treat relationships between data as equally important to the data itself. Unlike traditional relational databases, graph databases use graph theory to store, map, and query relationships. It is a collection of nodes and edges, where each node represents an entity and each edge represents a relationship between two nodes. They provide a flexible structure fpr handling highly interconnected data with many-to-many relationships and deep hirarchies. They are ideal for applications that require complex queries with high performance and flexibility. Graph databases are often used for social networks, recommendation engines and fraud detection. It is easy for visualizing and analyzing the data.

### Key Concepts
- **Node**: Represents entities with labels and properties. For example, each node has a label. We can have many nodes with the same label. We are able to define the label by ourselves. (e.g. person, movie, car). Node can also have any number of properties, which are key-value pairs. For example, a person node can have properties like name, age, address, etc.
- **Relationship**: Directed, named connections between nodes, source node and destination node, which may also contain properties. For example, we can have Person A and Person B nodes, and a relationship from Person A to Person B called "KNOWS", which denotes that Person A knows Person B. The relationship can also have properties, such as "since" (e.g. Person A knows Person B since 2010).

_Note: Relationships can have the same source node and destination node, which would be a relationship pointing to the node itself._

## Neo4j - A Popular Graph Database
Neo4j is an open-source, native graph database known for its high performance and flexibility, and ease of use in handling complex and connected data. It implements the graph model down to the storage level, allowing for efficient traversal and a flexible schema. It is written in Java and Scala and uses Cypher Query Language for data querying. It is available in both Community and Enterprise editions.

### Features of Neo4j
- **Cypher Query Language**: An SQL-like, graph-optimized query language, which allows for expressive and efficient data querying.
- **ACID Transactions**: Reliable transaction processing with cluster support and failover capabilities.
- **Scalability**: Capable of handling billions of nodes on moderate hardware, supporting constant time traversals for large graphs.
- **Flexibility**: The property graph schema is adaptable and flexible, allowing you to evolve your graph and add new relationships over time.
- **Language Drivers**: Neo4j provides drivers for a variety of popular programming languages, such as Java, JavaScript, .NET, and Python, facilitating integration with different technology stacks.

## Working with Neo4j

### Installing Neo4j
You can download Neo4j Desktop from the [official website](https://neo4j.com/download/). Choose the edition that suits your requirements (Community Edition is free).

### Basic Cypher Queries
Cypher is Neo4j's query language. Here's a simple example to create a node:

```cypher
CREATE (n:Person {name: 'John Doe', age: 29})
```

This creates a `Person` node with `name` and `age` properties. `Person` is the label of this node. The `CREATE` clause creates the node, and the `RETURN` clause returns the node.

### Relationship Queries
To create a relationship between two nodes:

```cypher
MATCH (a:Person {name: 'John Doe'}), (b:Person {name: 'Jane Doe'})
CREATE (a)-[r:LOVES]->(b)
RETURN r
```

This query creates a relationship of type `LOVES` between the two `Person` nodes. These two nodes must exist. Otherwise, `MATCH` will not be able to find them. The relationship is directed. The source node is `Person` node with name John Doe and the destination node is `Person` node with name Jane Doe. The relationship means that John Doe `LOVES` Jane Doe. 

The two nodes are matched using the `MATCH` clause, and the relationship is created using the `CREATE` clause. The `RETURN` clause returns the relationship.

### Example of a Graph

Below is an example with a combination of queries that creates a graph of people and movies, and their relationships. It creates a `Person` node for each actor and director, and a `Movie` node for each movie. It also creates `KNOWS` relationships between people who know each other, and `ACTED_IN` relationships between actors and movies. The query also creates a `KNOWS` relationship between Kathryn Bigelow and Jessica Chastain, and `ACTED_IN` relationships between Keanu Reeves and The Matrix, and Carrie Anne Moss and The Matrix.

```cypher
CREATE
  (keanu:Person {name:'Keanu Reeves', age:58, nationality:'Canadian'}),
  (carrie:Person {name:'Carrie Anne Moss', age:55, nationality:'American'}),
  (liam:Person {name:'Liam Neeson', age:70, nationality:'Northern Irish'}),
  (guy:Person {name:'Guy Pearce', age:55, nationality:'Australian'}),
  (kathryn:Person {name:'Kathryn Bigelow', age:71, nationality:'American'}),
  (jessica:Person {name:'Jessica Chastain', age:45, address:''}),
  (theMatrix:Movie {title:'The Matrix'}),
  (keanu)-[:KNOWS]->(carrie),
  (keanu)-[:KNOWS]->(liam),
  (keanu)-[:KNOWS]->(kathryn),
  (kathryn)-[:KNOWS]->(jessica),
  (carrie)-[:KNOWS]->(guy),
  (liam)-[:KNOWS]->(guy),
  (keanu)-[:ACTED_IN]->(theMatrix),
  (carrie)-[:ACTED_IN]->(theMatrix)
```

![Neo4j Node Example](https://neo4j.com/docs/cypher-manual/current/_images/graph_predicate_functions.svg "Example of a Neo4j Node")

Example is from the [Cyphern Manual Documentation](https://neo4j.com/docs/cypher-manual/current/functions/predicate/).

You can refer to the [official documentation](https://neo4j.com/docs/cypher-manual/current/clauses/create/) for more information on Cypher queries.


## Use Cases of Neo4j
- **Social Networks**: Managing complex and dynamic relationships between users.
- **Recommendation Engines**: Providing personalized recommendations based on user connections.
- **Fraud Detection**: Identifying patterns that indicate fraudulent activity.

## Conclusion
Neo4j offers a powerful and flexible way to handle complex data relationships. Its intuitive graph-based model makes it a go-to choice for applications where relationships are key.

## References
- [Neo4j Official Documentation](https://neo4j.com/docs/)
- [Getting Started with Neo4j](https://neo4j.com/docs/getting-started/get-started-with-neo4j/graph-database/)
