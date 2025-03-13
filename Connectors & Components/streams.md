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

