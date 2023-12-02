# Using Redis for Semantic Search

## What is Redis

Redis is an in-memory database that stores data using key-value pairs (like a Python dictionary). Redis can store data structures like strings, hashes, lists, sets etcs.
- [Official Redis Website](https://redis.io/)

## What is Semantic Search

Semantic search is a type of search algorithm that searches for results based on the meaning behind the query instead of pattern-matching the query. For example, given a query "coca-cola", a keyword search only yields anything in the database that contains the word, where as semantic search may yield resutls such as "Pepsi", due to the conceptual similarity between the two terms.

## How is Semantic Search Implemented?

To implement semantic search, there must be a reliable way to understand the meaning of a query. For example, one can give the query (such as "what is the weather")
Semantic search is done by creating embeddings for items in the database, as well as the query, and then calculating the distance between the query embedding and the item embeddings. Embeddings are high-dimensional vectors produced by a deep-learning model, it entails the high level meaning of its in the sense that 

