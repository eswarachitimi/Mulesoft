### What is Streaming in Mule Apps?

Streaming supports efficient processing of large data objects such as files, documents, and records by streaming the data through Mule rather than reading the whole thing into memory.

**_Streaming provides the following advantages:_**

- Allows flows to consume very large messages in an efficient way
- Message payloads are not read into memory
- Simple routing rules based on message metadata are still possible
- You can combine streaming and non-streaming endpoints.

![image](https://github.com/user-attachments/assets/78f6be57-86ee-4fa4-9aad-db952b258ea9)

![image](https://github.com/user-attachments/assets/a07fcf78-b784-4d04-8658-354c61eb8217)

![image](https://github.com/user-attachments/assets/a4450332-8732-420c-b857-ed8823423d75)


There are three types of streaming strategies available in MuleSoft:

1. Repeatable file store stream (by default, this strategy is selected).
2. Non repeatable stream.
3. Repeatable in-memory stream.

Following is the snippet for the same:

![image](https://github.com/user-attachments/assets/8033dd8c-3c24-46eb-8bfc-45daaa89ee46)

![image](https://github.com/user-attachments/assets/40434bd7-c9b7-40d9-9b7e-cc232f46ad6b)

### Repeatable File Store Stream

![image](https://github.com/user-attachments/assets/21f365b9-f4ff-47f9-b2a4-95b87bb429d6)

Before proceeding, let us consider a simple scenario like we have 0.1vCore (512MB memory) and our application is deployed, what will happen if you pass 1 GB of payload. Will it throw some exception or will execute successfully?

If you think, it will execute successfully then you are right, because by default 'Repeatable file store stream' strategy is selected. 

**_How Does It Work?_**

In reality, for 0.1 vCore there is 8GB of memory available, what MuleSoft provides to us is 512 MB as Heap memory. After 512 MB is full, data will be stored in the disk storage which is the remaining memory (8GB - 512MB (some installations let us assume 1.5 GB)).

**_Following are some of the advantages:_**

- As it stores data in the memory and disk, so you can pass input payload of more size than heap size.
- As the name suggests repeatable, once you read the data, and you want to read the same data somewhere else you can read that as data is backed up in disk storage.

### Non Repeatable Stream
In this streaming strategy, when the very first time you are reading the input payload, the memory assignment and everything work as Repeatable File Stream strategy but once read, the payload data will be cleared from the memory and disk space, and you cannot read it again.

### Repeatable In-Memory Stream
This streaming strategy is a bit different from others. In this, the data will be stored in memory (heap memory), it will not be stored in disk space. So if you pass payload more than heap size, it will throw memory out of bound exception.

![image](https://github.com/user-attachments/assets/86792938-b928-4b60-a0c5-ff6e255c1432)

![image](https://github.com/user-attachments/assets/d1bc1950-0a10-4056-a637-612596d7a74e)


# Streaming in Mule 4: Processing Large Data Sets

<img width="800" height="533" alt="image" src="https://github.com/user-attachments/assets/9dff6cd7-39ad-41fa-9764-ce6f20f7841d" />

🔹 What is Streaming in Mule 4?
In Mule 4, streaming is a way of processing large payloads (files, database results, HTTP responses, etc.) without loading the entire content into memory at once.
 Instead, Mule reads and processes the data piece by piece (streamed) — which prevents memory issues for very large datasets.
👉 In simple words:
Without streaming: Mule loads the whole file or query result in memory → OutOfMemory risk for large data.
With streaming: Mule processes chunks of data sequentially → Memory efficient & faster.
Types of Streaming Strategies in Mule 4

Mule provides Three main streaming strategies:
1.Repeatable In-Memory Stream
Stores payload in memory.
Works well for small/medium payloads.
Fast, but limited by available heap memory.

2.Repeatable File Store Stream
Stores payload in temporary files instead of memory.
Works well for large payloads (GBs of data).
Slightly slower (disk I/O), but avoids memory issues.

3.Non-repeatable Stream: 
 Cannot be read more than once
 Cannot be consumed simultaneously
 Very performant but needs careful treatment
 No additional memory buffers
 No I/O operations (disk-based buffers)
 Suitable for processing large streams

🔹 When to Use Streaming Process?
You should go for streaming in scenarios like:
When processing large files (CSV, Excel, XML, JSON).
When fetching large result sets from Database or APIs.
When integrating with real-time data feeds (logs, IoT, Kafka, messaging).
When payload needs to be read multiple times (e.g., logging + transformation).
When you need memory efficiency in high-throughput systems.
👉 If payload is small → In-Memory is fine.
 👉 If payload is huge → File Store streaming is recommended.

Real-Time Use Cases of Streaming in Mule 4
Large File Processing (CSV/XML/JSON)
Example: A logistics company uploads a 1 GB shipment CSV file daily.
Mule reads the file using file store streaming → processes line by line → stores into DB.
No Out Of Memory issues.
Database Large Result Set
Example: An e-commerce company extracts 10M order records for reporting.
Mule fetches results from DB using streaming → writes chunk by chunk to a flat file / another DB.
Real-time IoT Sensor Data
Example: Thousands of IoT devices send continuous temperature logs.
Mule streams data in chunks → applies rules → sends anomalies to alert system (Kafka/Queue).
API Integration (Download Large Files)
Example: Mule downloads a large PDF/ZIP from an external API.
Instead of loading the whole file in memory, Mule streams it → stores it in S3/cloud.
✅ Key Benefit: Streaming = Scalable, Memory Efficient, and High Performance
Repeatable In-Memory Stream: Stores data in memory (not ideal for large payloads).
Repeatable File Store Stream: Stores data temporarily on disk.
Non-repeatable Stream: Data is consumed once and not cached.
