# Retries in web services

Especially relevant for webserver applications, but useful for others, retries are really tricky to get right. 
Retries and throttling are both terms used to talk about the _flow_ of traffic into a service. Often the 
operators/developers of that service want to make guarantees about the rate of that flow, or otherwise direct 
traffic.

## Why retry at all?

Intermittent failure can happen at any level. This can be within a single host if its on-host disk, memory, or 
CPU fails, or often in the communication between two hosts over a network. Networks, especially over the public 
internet using TCP/IP, are known to have periodic failures due to high load/congestion or network infrastructure 
hardware failure.

Retries are a really simple, easy answer to these intermittent failures. If the error only happens rarely, then 
trying a task again is a really effective way to ensure that the message goes through. This often manifests 
itself as retrying API calls.

Some services have built up language around these retries to control them. For example, calling AWS APIs returns
metadata about the request itself. For example, there is a `$retryable` field in most of the AWS SDKv2's APIs, 
the most common client used to make AWS API calls. If this field is set `true`, the server is hinting that the 
failure was intermittent and that the client should retry. If the field is set to `false`, the server is hinting 
to the client that the failure is likely going to happen again.

## What are the problems with retries?

Since retries are so simple to implement and elegant, they are usually the first tool that developers reach for 
when a dependency of theirs has intermittent failures, but how can this go wrong?

Consider a case where 4 distinct software teams each build products that depend on one another, in a chain like:
```
A -> B -> C -> D
```

That is, service A is calling service B's APIs, and so on. Since B's APIs are known to fail occasionally, A has 
configured an automatic retry count of 3. Underneath the hood, B depends on C. Service A may or may not know this 
about B. But since C has a flaky API too, B also has a retry count of 3. And the same for C. 

This works fine, and will usually work. If all services are sufficiently scaled up to handle the load they are 
given, there are no problems.

However, imagine a case where service D is down. Though it is at the end of the chain of dependencies, in theory, 
the services should be able to stay up despite their dependencies being down. This type of engineering is called 
fault-tolerance.

The next time that Service A takes a request, it forwards it to B, which forwards it to C, which tries to call D's 
API, which fails. C then, tries again 3 times before reporting a failure back to B, which also triggers a retry. 
That means C tries _another 3 times_.

Retries deep into services grow multiplicatively, and a single API call to A has caused
```
A: 3
B: 9
C: 27
```
different API calls to fail. C is handling 27x more load than it is used to, and might start failing itself, further 
exacerbating the problem. 

That is, D has become a single point of failure for all other services, and even if they don't outright fail, the 
load on B, C, and D, are highly needlessly increased.

## What can we do about retries?

Clients calling services will nearly always have retries configured. However, internal services should rarely 
implement retries while calling other internal services, for precisely this reason.

Another technique to get around excessive retries is to utilize more caching. If service C had cached the responses 
from service D, it's possible that service D going down would have affected the top-level services at all, and 
everything would have worked as normal. The downside to this approach is that caches are often trick to get right, 
and sometimes introduce modal behavior in services [1], usually a bad thing.

## So should I retry?

As always in software engineering, it depends. A good rule of thumb is the external/internal, where external 
dependencies are wrapped in retries, but internal dependencies aren't. It's much easier to control the behavior of 
internal dependencies, either by directly contributing to their product, or speaking to the owners of that product 
itself. Retries are a rough bandaid, and more precise solutions are better. Fixing the root-cause of intermittent 
failures avoids the problems with retries in the first place, and produces a more stable product.

Retries are also more acceptable when they aren't in the _critical path_ of a service. For an `AddTwoNumbers` 
service, having retries on dependencies within the main `AddTwoNumbers` API call might not be a good idea. However,
for backup jobs, batch processing, or other non-performance-critical work, retries are often a simple, 
engineering-efficient way to ensure reliability.

## References
1. https://brooker.co.za/blog/2021/05/24/metastable.html