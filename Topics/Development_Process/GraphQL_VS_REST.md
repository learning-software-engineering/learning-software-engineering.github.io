# GraphQL and REST APIs

## Table of Contents
1. [Overview & Motivation](#overview--motivation)
    - [What is an API?](#what-is-an-api)
    - [Why do we need APIs?](#why-do-we-need-apis)
    - [Designing APIs](#designing-apis)
2. [REST Overview](#rest-overview)
3. [GraphQL Overview](#graphql-overview)
4. [When does REST make sense to use?](#when-does-rest-make-sense-to-use)
5. [When does GraphQL make sense to use?](#when-does-graphql-make-sense-to-use)
6. [Quick Reference](#quick-reference-for-common-uses)
7. [Summary](#summary)
8. [Additional Readings](#additional-reading)

## Overview & Motivation
### What is an API?
An API is an **application programming interface**, or in simpler words, a way for two pieces of software to communicate with one another. For example, every time you interact with Google's website, an API is being called in the background to get your search result data.

On this page, we will refer to things called `endpoints`. These are basically access ways for our API - you use these endpoints to communicate with the software. For example, when you search something on Google, their `/search` API endpoint is used to access the actual search API.

### Why do we need APIs?
Without APIs, there would be no way for software to communicate between one another. In fact, even within the same project, different components may have APIs between them to facilitate communication. Without APIs, software would never be able to interact with anything. Even something as simple as loading Google's webpage deals with many dozens of APIs without you knowing! 

### Designing APIs
In this article, we will specifically discuss APIs that deal with sending requests over the internet, which is a very special case of APIs. We will cover two special commonly used types of APIs:
1. REST
2. GraphQL 

On this page, you will learn about the differences between the two, and hopefully be able to make a confident decision on which one you need to use, based on your project requirements. 

## REST Overview
A REST API is any API that follows the REST architecture. The implementation of it can be handled in many pre-existing libraries, so this page will focus on the important details:
1. In REST, you have to specify the `type` of the request you are sending when you call an API endpoint.
    + Some common examples include `GET`, `POST`, `PUT`, and `DELETE`. Others exist, but these are the ones used most often.
2. REST is not specific; when you call an endpoint, you will get *all* of the data that endpoint can give, whether you like it or not.
    + For example, if you are trying to get the first name of a User, through REST you would send a GET request to a `/users` endpoint, which would give you the entire User object (i.e, more data than usual) and you would be required to parse the response and get the First Name.
    + This can be ideal when you require a lot of data, but can also lead to larger than necessary load on your system if you have to call many API endpoints in quick succession.
3. Every difference type of request in REST has to be called to a different endpoint. For instance, if you want to `GET` all `Users` and `Cars` at the same time, with a typical REST API, you would need to send two seprate `GET` requests to a `/users` and `/cars` endpoint.


## GraphQL Overview
GraphQL is difference from REST in the sense that it is not actually an API architecture. In fact, it is actually a `query language`, hence the QL in its name. This leads to a number of distinct characteristics that we will discuss:
1. In GraphQL there are only two types of requests: `Queries`, and `Mutations`. A query is used to get data, i.e, "query" some data. Everything else would be a mutation; creating, updating, or deleting data all mutate, and thus they are mutations.
    + To follow proper GraphQL standards, any endpoint that only sends back data would fall under `query`. Any endpoint that changes data in any way would fall under `mutation`.
2. GraphQL is very specific; when you call an endpoint, you can request *exactly* what data you want, and you can send different structures of data, based on customizable `types`.
3. GraphQL only requires one endpoint. Usually, this is found at the `/graphql` URL on a webapp. Since GraphQL is a query language, whenever call the endpoint, you use the request body to specify your query. From this, you can define mutations and queries, and can in fact, get multiple pieces on data through one request. Using the same example from REST, you would only need to send one `/graphql` request, and just write both queries for data in the same request. This allows you to get the same amount of data using one request instead of two separate ones.


## When does REST make sense to use?
REST makes the most sense if you deal with simple data, and you do not need to only get specific pieces of data; getting all of what you need is okay. In other words, if you're getting a User's data, for instance, you are okay with getting all of their data, instead of just their username for instance.

## When does GraphQL make sense to use?
GraphQL makes sense if you are dealing with quite complicated data, especially if it is large swaths of data where you might only need a specific chunk of it. It also makes sense if you need to get numerous different pieces of data at the same time, and want to do so efficiently. GraphQL is much faster than REST in terms of actual efficiency of getting data, but has a trade-off of a complex set up compared to REST.


## Quick reference for common uses
In JavaScript, you can implement REST APIs through ExpressJS. Here is an example request, where you would call an already existing API request using fetch(). 
```javascript
const response = await fetch("http://example.com/movies.json", {
  method: "POST",
  body: JSON.stringify({
    name: "Barbie",
    director: "Greta Gerwig",
    stars: [
        "Margot Robbie"
    ]
  })
});
```

You can implement GraphQL in JavaScript with the GraphQL library. Here is an example GraphQL query, where you would get the director of the Barbie movie, similarly to the above request.
```graphql
query {
  getMovie(params: {
    name: "Barbie"
  }) 
  { director }
}
```

For more information on setting up and creating your own API through REST or GraphQL, you can visit their respective documentation here:
- https://graphql.org/graphql-js/
- https://expressjs.com/en/starter/hello-world.html

## Summary
In summary, there are many similar uses for GraphQL and REST. They can both accomplish the same things, but depending on your data structure, one would be better in terms of efficiency and complexity of development. GraphQL requires a lot more boilerplate code, and needs types and queries set up, while REST's setup just requires a few lines defining some simple endpoints.


## Additional Reading
1. https://www.mulesoft.com/resources/api/what-is-an-api
2. https://www.redhat.com/en/topics/api/what-is-a-rest-api
3. https://www.ibm.com/topics/rest-apis
4. https://www.apollographql.com/blog/graphql/basics/what-is-graphql-introduction/
5. https://aws.amazon.com/compare/the-difference-between-graphql-and-rest/
