# GraphQL With Apollo

## Table of contents
### [Introduction](#introduction)
### [GraphQL Explained](#graphql-explained)
### [Apollo Explained](#apollo-explained)
### [Tutorial With Basic Setup](#tutorial-with-basic-setup)

## Introduction
GraphQL simply put is a query language used to build APIs. It is a framework that is very different from the traditional approach of API design. It allows clients to request exactly what they need, nothing more and nothing less, making it an incredibly efficient tool for data retrieval and manipulation. Used across various applications, from small-scale projects to large enterprise-level systems, GraphQL provides a flexible and efficient way to interact with data. It stands out due to its compatibility with a wide array of technologies, including but not limited to JavaScript frameworks like React, Vue.js, and Angular. Unlike SQL, which is a query language specifically for interacting with relational databases, GraphQL is not tied to any specific database or storage engine. Its agnostic nature allows it to work seamlessly with both relational databases like MySQL and PostgreSQL, as well as non-relational databases like MongoDB. At its core, GraphQL operates by defining a schema that describes all possible data points and relationships in the system, enabling clients to query precisely what they need, leading to optimized data loading and reduced network usage.

## GraphQL Explained
Under the hood, GraphQL works in fashion such that a client sends a query to a GraphQL server, it typically includes specific fields on the types it requests. This query is a string that follows the GraphQL query language syntax. The server parses the incoming query, ensuring it is a valid one and uses the correct syntax. Once the query is validated, ensures that the query matches the GraphQL schema defined on the server. The schema defines all possible types, queries, mutations, and the relationships between these types. If the query asks for fields that don’t exist or are not allowed due to schema constraints, the validation step will fail. resolving each field that the query requests. Resolvers are functions defined on the server for each field in the schema. When a field is requested, its corresponding resolver is called. The resolver function fetches the data for that field, which can involve retrieving data from databases or other data sources. After all resolvers have returned their data, GraphQL assembles this data into a response object that mirrors the structure of the query. The server sends this response object back to the client, typically in JSON format.

Though this process is similar to relational query languages (SQL), the key differences are:
- Query Flexibility: GraphQL allows clients to define the structure of the response data, requesting exactly what they need in a single query. This flexibility reduces over-fetching or under-fetching of data. While SQL requires more rigid, predefined queries, specifying exact tables and columns to retrieve. Thus GraphQL offers more efficient data retrieval tailored to client needs, reducing bandwidth and improving performance.
- Data Retrieval Endpoint: GraphQL uses a single endpoint to handle a variety of queries, with the query itself defining the data requirements. In contrast, SQL typically involves separate queries to different tables or views in a database. Therefore, GraphQL simplifies API structure and maintenance with a single, unified interface for diverse data requests.
- Schema and Data Relationships: GraphQL employs a schema to define data types and their relationships, guiding query validation and execution. SQL, on the other hand, focuses on data storage structure (tables, columns) without inherently defining relationships for data retrieval. This makes GraphQL more effective in enhancing client-side querying capabilities by clearly defining data relationships and available operations.
- Data Source Integration: Capable of integrating with multiple data sources within the same query, GraphQL can handle different databases, APIs, and static files, unlike SQL, which is specific to a single database and its structure. This versatility makes GraphQL a unified layer to access varied data sources, making it versatile for complex applications.
- Execution Process: GraphQL utilizes resolver functions to retrieve data for each field in a query, allowing for custom logic and integration with various data sources. SQL, however, directly executes queries against the database for data retrieval. The flexibility offered by GraphQL in how data is fetched and processed accommodates complex and varied data retrieval needs.

## Apollo Explained
Apollo is a comprehensive suite of tools designed to work with GraphQL, making it easier and more efficient to build, manage, and query GraphQL APIs. Apollo consists of two tools. Firstly, the Apollo Client, is a state management library for JavaScript applications that facilitates efficient data fetching, caching, and state management in applications using GraphQL. On the server-side, Apollo Server provides a quick and straightforward way to set up a robust GraphQL server that can interface with various data sources, including SQL and NoSQL databases.

## Tutorial (With Setup)
To get started with a GraphQL project with Apollo first run: 
```
mkdir apollo-graphql-server
cd apollo-graphql-server
```

Then initialize and install all dependencies:
```
npm init -y
npm install apollo-server graphql
```

Now ```cd``` to the project folder and in the root create an ```index.js``` file for the server, schema, and resolver code. 

Then add the following schema, resolver and server side code: 
```
const { ApolloServer, gql } = require('apollo-server');

// Define your schema here.
const typeDefs = gql`
  type Query {
    hello: String
  }
`;

// Define your resolvers here.
const resolvers = {
  Query: {
    hello: () => 'Hello, world!',
  },
};

// Create the Apollo Server instance.
const server = new ApolloServer({ typeDefs, resolvers });

// Start the server.
server.listen().then(({ url }) => {
  console.log(`Server running at ${url}`);
});
```

Now, start the server by running ```node index.js``` and open up localhost to access the client playground. Test the code by running: 
```
query {
  hello
}
```
You should get the following as a response: 
```{"data": {"hello": "Hello, world!"}}```

Expand your GraphQL API by adding more types, queries, and mutations! Start integrating with a database like MongoDB or PostgreSQL to fetch and manipulate real data!