1. Clarify both functional and non-functional requirements before designing.
2. Assume everything can and will fail. Make it fault tolerant.
3. Don't add functionality until it's necessary. Avoid over-engineering.
4. There is no perfect solution. It’s all about tradeoffs.
5. Prefer horizontal scaling over vertical scaling for scalability.
6. Use load balancers to distribute traffic and ensure high availability.
7. Consider using SQL databases for structured data and ACID transactions.
8. Opt for NoSQL databases when dealing with unstructured data.
9. Use database sharding to scale SQL databases horizontally.
10. Use database indexing to optimize read queries.
11. Use rate limiting to prevent system overload and DOS attacks.
12. Use websockets for real-time communication.
13. Employ heartbeats / health checks for failure detection.
14. Consider using a message queue for asynchronous communication.
15. Implement data partitioning and sharding for large datasets.
16. Consider denormalizing databases for read-heavy workloads.
17. Consider using event-driven architecture for decoupled systems.
18. Use CDNs to reduce latency for a global user base.
19. Use write-through cache for write-heavy applications.
20. Use read-through cache for read-heavy applications.
21. Use blob storage to store media files like files, images, videos etc..
22. Implement data replication and redundancy to avoid single point of failures.
23. Implement autoscaling to handle traffic spikes smoothly.
24. Use asynchronous processing to run non-urgent/background tasks.
25. Make operations idempotent where possible to simplify retry logic and error handling.
26. Prefer microservices architecture over monoliths for scalability, modularity, and maintainability.
27. Consider using an API gateway when you have multiple microservices.
28. Use the circuit breaker pattern to prevent cascading failures
29. Design clear and consistent APIs and incorporate security.
30. Consider using a data lake or data warehouse for analytics and reporting.
