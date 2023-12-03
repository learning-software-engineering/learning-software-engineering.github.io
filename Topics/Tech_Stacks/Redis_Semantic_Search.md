# Using Redis for Semantic Search
This page explains the implementation of semantic search using Redis. First, an introduction is provided on semantic search and related concepts. In addition, Redis is introduced as a vector database that provides support for semantic search. Lastly, an example is provided to show how to implement semantic search using Redis.

## Introduction
### What is Redis?
Redis is an in-memory database that stores data using key-value pairs (like a Python dictionary). Redis can store data structures like strings, hashes, lists, sets, etc. 
- [Official Redis Website](https://redis.io/)

### What is Semantic Search?
Semantic search is a type of search algorithm that searches for results based on the meaning behind the query instead of pattern-matching the query. For example, given a query "coca-cola", a keyword search only yields anything in the database that contains the word, whereas a semantic search may yield other results such as "Pepsi", due to the conceptual similarity between the two terms.

### Why do we want semantic search?
Semantic search often produces more accurate results, consider a database consisting of Wikipedia articles on food companies, a simple keyword search for 'Carbonated Drinks' only yields pages that contain the keyword in full or in part, but semantic search can produce results such as Pepsi or Coca-Cola, even if the content of these pages doesn't contain any substring of the keyword.

### How is Semantic Search Implemented?
To implement semantic search, there must be a reliable way to understand the meaning of a query (or any string in the database). This is usually done by creating embeddings. Embeddings are high-dimensional vectors produced on a target string, they entail the high-level meaning of its target in the sense that the embeddings of two closely related concepts will be near each other (i.e. the Euclidean distance between the two vectors is close to zero). 
Here are the steps for semantic search:
- preprocessing:
  1. For each item in the database, create an embedding
- Search:
  1.  Embed the query
  2.  Find the k-nearest neighbor between the query embedding and the database embeddings

### How to create embeddings?
Embeddings are usually created by a deep learning model that takes a string as its input and produces a vector (an array of float point vectors) as its output. The simplest way to create embedding is to call openAI's API for embedding models.
- [OpenAI Embeddings](https://platform.openai.com/docs/guides/embeddings/)


## Example
For the following example, I will show the Python implementation of a Redis database design for articles and a function that returns the most relevant search results from a string query.

### 1. Installations
To use Redis, one must either create a Redis database locally or use Redis Cloud. Redis Cloud is free for use (max 30MB storage) and an account can be easily created with the following link: https://redis.com/try-free/

Then, for intuitive database manipulation through GUI, download Redis Insight V2 with the following link: https://redis.io/docs/connect/insight/

### 2. Setup
First, create a new python file:

```
touch example.py
```

Import relevant modules:
```python
import openai
import pandas as pd
import redis
```

Connect to database:
```python
r = redis.Redis(host='your host ip',
                port=your port here,
                password='your hey here',
                decode_responses=True)
# You can get the above parameters from your Redis Cloud console
# decode_responses=True is used to receive decoded strings

```

Before writing our query, we must specify a schema, this will be used later for searching through our database:
```python
schema = (
            TextField("$.text", no_stem=True, as_name="text"),
            VectorField(
                "$.embedding",
                "FLAT",
                {
                    "TYPE": "FLOAT32",
                    "DIM": self.model_dimension,
                    "DISTANCE_METRIC": "COSINE",
                },
                as_name="vector",
            ),
        )
definition = IndexDefinition(prefix=["article:"],
                             index_type=IndexType.JSON)
r.ft(INDEX_NAME).create_index(fields=schema, definition=definition)

```

First, we must create embeddings for our texts:
```python
def create_embeddings(self, texts: [str]) -> pd.DataFrame:
  """ Create an embedding for a array of texts.
  """
  embeddings = []
  for text in texts:
    # Call OpenAI's API for embedding
    response = openai.Embedding.create(model="text-embedding-ada-002", input=text)
    embeddings.append(response["data"]["embedding"])
  
    df = pd.DataFrame({"text": texts, "embedding": embeddings})
    return df

```

Next, we can fill the database with data:
```python
pipeline = r.pipeline()

# iterate through all rows in the data frame produced by the above code
for index, row in df.iterrows():
  # redis is a key-value store, we store data by given each piece of data a key
  key = f"article:{index}"
  value = {"text": row["text"],
           "embedding": row["embedding"]
          }
  pipeline.json().set(key, "$", value)
pipeline.execute()
```

Lastly, we will write a function that performs a query:
```python
def get_article_sections(self, query: str):
    # create an embedding for our query
    query_embedding = self.embedder.create_embedding(query)

    # write our query, we are getting the top 5 related articles
    redis_query = (
        Query(f'(*)=>[KNN {5} @vector $query_vector AS vector_score]')
        .sort_by('vector_score')
        .return_fields('vector_score', 'text')
        .dialect(2)
    )

    # Get query results
    result_docs = r.ft(INDEX_NAME).search(redis_query,
                                          {
                                            'query_vector': np.array(query_embedding,
                                             dtype=np.float32).tobytes()
                                          }).docs
    
    rt = []
    for doc in result_docs:
        item = {"text": doc["text"],
                "vector_score": doc["vector_score"]}
        rt.append(item)
    return rt
```


