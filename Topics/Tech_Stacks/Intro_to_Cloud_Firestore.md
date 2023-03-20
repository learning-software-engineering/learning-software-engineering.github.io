# Using Firebase's Cloud Firestore

## Introduction

When choosing to use a NoSQL database, Firebase provides two options. One is the Firebase Realtime Database and another is the Cloud Firestore. 

Cloud Firestore is Firebase's newest database for mobile app development. It builds on the successes of the Realtime Database with a new, more intuitive data model. Cloud Firestore also features richer, faster queries and scales further than the Realtime Database.

Realtime Database is Firebase's original database. It's an efficient, low-latency solution for mobile apps that require synced states across clients in realtime.

## Comparing the Options

While both are NoSQL databases, Realtime Database stores data as one large JSON tree, whereas Cloud Firestore stores data as collections of documents. This makes complex, hierarchical data harder to organize at scale in Realtime Database. In Cloud Firestore, organizing data is easier at scale using subcollections within documents. 

In addition, Realtime Database is limited in its sorting and filtering functionality. For example, queries can sort or filter on a property, but not both. These queries are also deep by default because they always return the entire subtree. In Cloud Firestore, you can chain filters and combine properties in a single query. Queries are also shallow because they only return documents in a particular collection or collection group and do not return subcollection data.

There are many other factors to consider aside from the data models and querying, including writes and transactions, reliability and performance, scalability, security, etc. For more information, consult the [official documentation](https://firebase.google.com/docs/database/rtdb-vs-firestore).

## Getting Started

Once you decide to move forward with Cloud Firestore (or use it in conjunction with the Realtime Database), you can follow this [tutorial](https://firebase.google.com/docs/firestore/quickstart) to start. Further readings (e.g. how to add/manage data, make queries) can be found [here](https://firebase.google.com/docs/firestore).