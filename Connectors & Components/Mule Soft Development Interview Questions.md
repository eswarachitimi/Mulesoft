### How will you achieve optimal performance in your Mule Application?
 
There are some tuning recommendations that you can apply at the application level to make better performance of the Mule Applications.

1. Repeatable/Non-Repeatable strategy:
Non-Repeatable Strategy:
 Even though this strategy has advantages like memory efficiency, performance, simplified data handling, and reducing the risk of out-of-memory error, the main disadvantage is that it reads the payload only once, also reprocessing the data is not possible.
Repeatable Strategy:
Useful in scenarios where the same data needs to be processed or accessed by multiple components within the flow. Payload can be read more than once.
 1.     File-store streaming
 2.     In-memory streaming
File-Store Repeatable Stream
 To handle large data streams by storing them in a temporary file on disk, allowing the stream to be read multiple times without consuming a large amount of memory.
 In-memory repeatable stream
 To handle data streams by storing them in memory (heap memory), allowing the stream to be read multiple times.
Both repeatable strategy has some properties to be set.

2. Back pressure and Max concurrency:
 Whenever all threads are busy and the flow concurrency is exceeded, it logs the message “Flow 'flowName' is unable to accept new events at this time”.
This message is called back pressure. MaxConcurrency is used to handle the back pressure.
Max Concurrency:
 There is no limit for the Max Concurrency values for Flow and Async, but the Max concurrency for Batch is double the available cores of your system CPU. Eg: If your system has 10 cores, the max concurrency’s maximum value is 20.
Max concurrency Components:
·       Flow scope --> limits the number of messages processing in the Flow
·       Scatter-Gather router --> limits how many routes should processed concurrently
·       Async scope --> limits the no of messages processing in the Async Scope
·       Batch Job scope --> limits the no of records to be processed in the Batch step concurrently
·       Parallel For Each scope  --> limits the no of records or elements to be processed concurrently
Guys to be continued in the Next Post.


### How will you manage sticky session in Mule HTTP request?

Sticky Session --> A sticky session, also known as session persistence, is a method used in load balancing to ensure that a user's session is always handled by the same server.
In some cases the server’s load-balancing technique may have Round-robin DNS, we have to set the property to maintain the Sticky Session to ensure User Experience. 

In order to do this, we can set the property [ mule.http.disableRoundRobin=serverhostname.com ] 
This will disable the Round-Robin DNS technique in the Server.

Main Advantage:
 This can be important for applications that store session data locally on the server, such as user authentication information, shopping cart contents, or other stateful data.

Summary: 
 Sticky sessions (session persistence) ensure that a user's session is consistently handled by the same server, which can be crucial for stateful applications.

### Difference between for-each, parallel for-each, batch process?

For-each Scope:
·       Splits the payload into elements and iterate one by one 
·       After for-each Payload remains the same as before the for-each, i.e whatever payload updated inside for-each doesn’t come outside the flow
·       Note: Processed payload inside for-each can be retrieved using the Set variable inside the for-each and storing the payload as Variable. This variable can called outside the for-each to access the payload that updated or changed inside the for-each.
·       Error-Handling--> If one of the elements in the payload collection throws an error, the scope stops the process.

Parallel for-each Scope:
·       Split the collection and simultaneously process in separate routes. 
·       After finishing the process, the payload is arranged in the same order as before they split.
·       Each element is processed in parallel using separate threads.
·       It reduces processing time and improves the overall efficiency and scalability of your MuleSoft applications.
·       Error Handling --> As the process is parallel if any error occurs, it won't stop the entire process. After the process is completed, the error handler will handle the error MULE: COMPOSITE_ROUTING.

Batch
 One of the most used and important core components is the Batch process.
·       To handle large data sets in an Asynchronous process.
·       Three components of the Batch process --> Batch Job, Batch, Step, Batch Aggregator.
·       Batch Job--> splits data and stores it in the persistent queue, it has Load and dispatch, process, and On Complete phases.
·       Batch step--> process the individual records from the persistent queue. It is the processing unit within the batch job, allowing you to apply transformations, validations, or interact with external systems for each record. To filter records, the Batch Step component supports one acceptExpression and one acceptPolicy.
·       Batch Aggregator --> useful for sending multiple records within an array to an external server. Using Batch Aggregator, we can add an operation, such as a bulk upsert, insert, or update operation, to load multiple records to a server with a single execution of an operation, instead of running an operation separately on each record.
·       Error-Handling: However there are dataweave functions to handle the errors like #[Batch::isFailedRecord()], we have to configure the Accept policy as ONLY_FAILURES. 


### Which type of rate-limiting policy can be applied to the System API? 

 Answers: Based on the requirement we can apply any type of rate-limiting Policy. The type of rate-limiting policies are Rate limiting Policy, Rate limiting Policy SLA based, and Spike Control Policy.

Rate Limiting Policy:
 After applying this policy, the API Gateway enables you to control incoming traffic to an API by limiting the number of requests. If the limit is reached it rejects the upcoming requests and returns 429 Too Many Request Status. This policy is mainly applied to avoid the overloading of the Backend API.
For example: Assume that You are applying the parameters Number of Requests = 10 and Time Period = Second. Now n number of requests comes to the server, it only allows 10 requests based on the applied parameters. If the 11th request is reached, the server returns 429 Too Many Requests. 

Rate Limiting Policy SLA-based:
 SLA--> Service Level Agreement, a contract between the API provider and API consumer.
This Policy is the same as the rate-limiting policy, the only difference is that the request with the Client ID, an optional client secret is only allowed to the server by API Gateway. The request must be within the SLA limit. This policy can calculate rate limits based on either overall requests or requests from a particular user/client ID.
For example: Assume that there are 15 requests to the server, only requests with Client ID and an optional client secret are allowed to be requested. When a number of requests or requests from a particular Client ID reaches the limit, it returns 429 Too Many Requests.

Spike Control Policy:
 The spike control policy is very useful where the request can be queued for a particular time. You can set the number of requests to be queued and the time to be stored. The queued request retries for the second time based on the policy.
 There are some parameters to be given while applying the policy. To ensure maximum performance, configure these parameters to the lowest possible value. The Spike Control policy uses a Sliding Window Algorithm which reduces spikes in traffic and protects the gateway instance. 
For example: You can set the request limit as 100 per second and the queue limit can be 20. If 101 requests arrive, it will be stored in the queue. When 121 requests reach, it returns 429 Too Many Requests.

### Can you explain the difference between Cache and Object store? 

Cache --> Store the frequently called data for a particular time.
Cache scope in the Mule core component can be used to store the frequent data to reduce the processing load. The next time the Cache scope receives the same kind of message payload, the scope can offer a cached response rather than invoking a potentially time-consuming process again. With this, the processing speed is well maintained.

For example: We can give the request component inside the Cache scope to reduce the processing load for the second time, or we can give a select database component in the cache to avoid the database connection for the second time. But if you need a particular ID to be retrieved, use the filter function in the transformation message to filter the ID data.

Configure the cache size, expiration time, and maximum allowed entries using the caching strategy object-store.

Object store: 
 The object store is mainly used for storing and retrieving key-value pairs, often to maintain state, cache data, or store transient information that needs to be shared across different components and flows. You can configure a Mule app to use the Object Store REST API to store and retrieve values from an object store in another Mule app.
Object Store Connector is a Mule component that allows for simple key-value storage. We can use object store connector components to store and retrieve the data in Key Value Pairs.

### What happens when enabling the cookies in the Request configuration?

 Cookies --> Actually, Cookies store the data on the client side that was reached from the request.
Cookies in the HTTP request config help us pass the data to the HTTP listener in key-value pairs. The data passed from the request to the listener can be retrieved using attributes.header by set variable or in Transform message
The main use of Cookies:
* Session Management --> To maintain the state of a user.
* Authentication and Authorization --> To store authentication tokens.
* Load Balancing and Sticky Sessions --> To ensure that subsequent requests from the same client are routed to the same server instance in a clustered environment.
* User Preferences and Personalization --> To store user preferences and settings.
* Caching and Performance Optimization --> To reduce the need for repeated data retrieval.

### What do you know about Round-Robin?

 Round Robin in the Mule core component can contain n number of processing routes to process the mule event. Each time it selects the next to the previously selected router to execute the event. It never selects the same consecutive router.
For example: Assume that you have 4 routers in a round-robin router, if you trigger the flow for the first time, the first router is selected to execute the event. If you trigger a second time, the round-robin automatically selects the second router.
Note: Round-Robin router never depends on the method(get, post, put, delete)  you give. Even if you change the method and trigger the flow for a second time, it will route the second router automatically. 

Round-Robin Strategy in Load Balancing:
 The most commonly used load-balancing strategy is the Round-Robin strategy, where incoming requests are distributed evenly across a pool of available servers or instances. This method ensures that each server gets an equal share of the load, providing a simple and effective way to balance traffic. Even though the Round-Robin strategy has many advantages, it also has some disadvantages like it doesn’t suit for Stateful applications, it doesn't account for the capacity of each server. To overcome these disadvantages, Round-Robin has variations like Weighted Round-Robin and Dynamic Round-Robin.

### What is the purpose of enabling Persistent connection in Request Configuration, what happens when it is disabled?
Answer: If false, each connection will be closed after the first request is completed (Answer in MuleSoft document). 
Assume that the connection (created by the request) between a server and a client has a default timeout of 30000. If persistent is enabled, the connection is opened until the 30000 of default timeout. Here n number of requests can happen within this timeout. However if persistent is disabled, the connection between the server and client will be closed when the first request is completed. So, whenever a new request is triggered it creates a new connection between the client and server. This could be understood. But To understand practically, create a simple flow with a request component and get attributes in Postman. In that, we will have a remote address. If persistent is enabled, you can see the Unchanged remote address until 30000 of timeout for the next specific triggers. If persistent is disabled, you will get a new remote address each time when you trigger the flow.

### Why the post-method non-idempotent?
Answer: Idempotent --> Idempotence is a property of performing an operation multiple times that have the same effect or result. So, we know that the data will be created newly each time when we are triggering the request with the Post method. So, the post method is non-idempotent. get, put, and delete are idempotent as they will give the same result. By default, the patch is non-idempotent, but we can design the patch as idempotent by giving condition headers like If-Match.

