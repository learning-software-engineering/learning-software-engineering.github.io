# Learning DynamoDB

## Table of contents

### [Introduction](#introduction)

### [Why would I want to use it?](#why-would-i-want-to-use-it-1)

### [Why would I not want to use it?](#why-would-i-not-want-to-use-it-1)

### [How do I use it effectively?](#how-do-i-use-it-effectively-1)

### [Additional resources](#additional-resources-1)

## Introduction

This is a very brief overview of DynamoDB, what it is, why you might want to use
it, why you might not want to use it, and how to go about using it effectively.

## What is it?

DynamoDB is a [NoSQL database](https://en.wikipedia.org/wiki/NoSQL) that is
designed to be fast at any scale. It is developed by Amazon and is available
through Amazon Web Services.

## Why would I want to use it?

DynamoDB has a couple of main selling points:

1. Scalability: your database will automatically adjust to the scale required of
   it.
1. Speed: due to how the database is implemented, queries will always be fast -
   as long as your data is modelled appropriately for your access patterns!
1. Fully managed by AWS: it's pretty easy to quickly spin up a database that
   will just work, with all the great benefits that come with AWS.

## Why would I not want to use it?

There are a few major details of DynamoDB that may make it the wrong choice for
your application.

1. Inflexibility: DynamoDB is not designed to be flexible. You need to have a
   pretty good idea of what your core access patterns will be at the time of
   making your initial data model. If your application is changing frequently
   DynamoDB might cause you more headaches than it's worth!
1. Incompatibility with certain access patterns: if your application has certain
   collections of complex access patterns, DynamoDB will either take up a lot of
   extra storage space or be very slow.

## How do I use it effectively?

If you've decided DynamoDB might be a good fit for your application, then you
should try designing a single-table data model! There are a couple of key
concepts to DynamoDB that you'll need to understand to start creating a data
model (not an exhaustive list):

1. Partition keys & sort keys
1. Attributes
1. Global secondary indexes

Together, an **item**'s partition key and sort key must uniquely identify it.
They should be pretty generic, since lots of different types of items may need
to be stored. Attributes are the real data you want to store. DynamoDB is
schemaless so you can store whatever attributes you want on an item, but as a
result, you must also keep your data model straight in your application code
when you're reading and writing to the database.

Global secondary indexes can be defined on your table to account for usecases
where querying on your partition key + sort key will not be efficient. When you
define a GSI, all of the data will be replicated and stored (effectively in
another table) with your GSI as the partition key. For example, if an access
pattern we wanted to account for was to find all users with the first name
"Spencer", but it wouldn't make sense to define our partition key to be first
name, we could say that first name is a GSI on our table. This would allow us to
make an efficient query to find users with the first name "Spencer", but would
cost us some space to store the replicated data. This is a trade-off; if we had
very many situations where we needed to query on attributes, then we would
probably want to re-evaluate whether DynamoDB is the best choice for us.

## Additional resources

- [AWS Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)

A lot of my learning on DynamoDB has been from Alex DeBrie - he has done a bunch
of practical talks on DynamoDB and has even written "The DynamoDB Book". I'd
recommend looking into his stuff if you're interested in learning more about
DynamoDB and how to best use it.

- [The DynamoDB Book](https://www.dynamodbbook.com/)
- [Data modelling talk at AWS re:Invent 2020](https://www.youtube.com/watch?v=fiP2e-g-r4g)
- [Alex DeBrie's website](https://www.alexdebrie.com/)
