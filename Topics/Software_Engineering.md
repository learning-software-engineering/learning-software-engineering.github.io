## Resources for Software Engineering

Potential topics--

1. Methodologies & Frameworks

    1. Agile
        1. Scrum
        2. Kanban
        3. XP
    2. Waterfall

2. Software Design Patterns

    1. Scalable Architecture - Approaches to building scalable software architectures
       Scalable sofware architecture is critical in modern software engineering, as it allows for systems to handle increasing amounts of load, users, and data. Scalability refers to the ability of a system to handle growth while maintaining performance, reliability, and availability.

        Scalable software architectures are based on the two main principles: vertical scaling and horizontal scaling.

        - Increasing the capacity of a single system by adding more processing power, memory, or storage resources is referred to as vertical scaling, also known as scaling up. This strategy can be cost-effective for small-scale applications and is reasonably straightforward to execute. However, vertical scaling has a limit, as the application expands, it gets more challenging and expensive to keep upgrading hardware resources.

        - Increasing the number of machines to disperse the workload and resources across them is known as horizontal scaling, often referred to as scaling out. This method can be scaled infinitely because new machines can be added to the system as needed. Applications that need high availability, fault tolerance, and performance are good candidates for horizontal scalability. To ensure that the distributed systems work together and without interruption, this technique calls for more complicated design and implementation.

        There are different approaches to building scalable software architectures that are dependent on the specific requirements of the system.

        - One such approach is a microservices architecture. Due to their loose coupling (subsystems are not strongly connected), these services can be independently deployed and scaled. By employing this method, programmers may be able to locate and eliminate system bottlenecks as well as improve the scaling of specific components.

        - Another approach that uses the scalability and flexibility of cloud computing is the cloud-based architecture. Cloud-based systems provide fault tolerance and disaster recovery capabilities for maintaining high availability. In addition, you can increase processing power and throughput by adding more computing resources, using load balancers, distributed databases, and caching.


