# Architecting a System to Handle 100k+ Requests

## Motivation
When we build a project, we are often concerned with the product; what features does the user want? After we've identified the features to build, we come up with a specification and implement our solution accordingly. We test our code to ensure correctness before then finally shipping. 

But what happens after this? If we have have tens or hundreds of thousands of users each making lots of requests, how do we know that our system can handle the load? This page aims to provide a high level framework for designing such a system and provides additional resources for interested readers. 

We consider an app with three components: a client, an API, and a database. The database stores persistent information, our APIs serve requests for data from the database, and the client renders data for the user to interact with in some capacity. 


## Vertical and Horizontal Scaling
Suppose we have an influx of thousands of users, there are two ways we can think about scaling the system: vertically and horizontally. **Vertical scaling** refers to the resource capacity of our APIs; we can increase their capacity by increasing the amount of memory (RAM) and compute power (CPUs) available to our server. However, we can see that this approach will not scale beyond a certain limit simply from a physical and cost perspective. So we also consider **horizontal scaling** which refers to increasing the number of servers we have hosting our APIs. We can have virtually infinite servers running to distribute the workload of all the requests we're receiving from the client. Naturally, we will need a way to direct traffic according to some logic so that the load is balanced amongst our servers. 

## Load Balancing
A **load balancer** is responsible for routing requests from our clients to the 


## Database Scaling


## Caching

## CDN 

## Stateless Architecture 

## Sources 

This page is based on [Alex Pareto's blog post "Scaling to 100k Users"](https://alexpareto.com/scalability/systems/2020/02/03/scaling-100k.html), [High Scalability's Guide to Scaling to 11 Million+ Users on AWS](https://highscalability.com/a-beginners-guide-to-scaling-to-11-million-users-on-amazons/), [Linh Truong's page on Building & Scaling to 100 Million Users](https://scholar.harvard.edu/linh/system-design), [Anh T. Dang's Medium post on Designing a System to Scale to 100 Million Users](https://levelup.gitconnected.com/how-to-design-a-system-to-scale-to-your-first-100-million-users-4450a2f9703d), and [Daniel Adetunji's Explainer on Stateful vs Stateless Architecture](https://www.freecodecamp.org/news/stateful-vs-stateless-architectures-explained/#:~:text=In%20a%20stateless%20architecture%2C%20HTTP,needed%2C%20without%20impacting%20state%20data.)

