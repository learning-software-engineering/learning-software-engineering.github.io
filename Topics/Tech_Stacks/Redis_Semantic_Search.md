# Using Redis for Semantic Search
This page explains the implementation of semantic search using Redis. First, an introduction is provided on semantic search and related concepts. In addition, Redis is introduced as a vector database that provides support for semantic search. Lastly, an example is provided to show how to implement semantic search using Redis.

## Introduction
### What is Redis?
Redis is an in-memory database that stores data using key-value pairs (like a Python dictionary). Redis can store data structures like strings, hashes, lists, sets, etc. 
- [Official Redis Website](https://redis.io/)

### What is Semantic Search?
Semantic search is a type of search algorithm that searches for results based on the meaning behind the query instead of pattern-matching the query. For example, given a query "coca-cola", a keyword search only yields anything in the database that contains the word, whereas a semantic search may yield other results such as "Pepsi", due to the conceptual similarity between the two terms.

### How is Semantic Search Implemented?
To implement semantic search, there must be a reliable way to understand the meaning of a query (or any string in the database). This is usually done by creating embeddings. Embeddings are high-dimensional vectors produced on a target string, they entail the high-level meaning of its target in the sense that the embeddings of two closely related concepts will be near each other (i.e. the Euclidean distance between the two vectors is close to zero). 
Here are the steps for semantic search:
- preprocessing:
  1. For each item in the database, create an embedding
- Search:
  1.  Embed the query
  2.  Find the k-nearest neighbor between the query embedding and the database embeddings

### How to create embeddings?
Embeddings are usually created by a deep learning model that takes a string as its input and produces a vector (an array of float point vectors) as its output. The simplest way to create embedding is to call openAI's api for embedding models.
- [OpenAI Embeddings](https://platform.openai.com/docs/guides/embeddings/)






