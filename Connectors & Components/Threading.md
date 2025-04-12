# Threading

Starting in Mule 4.3, Mule contains one unique thread pool, called the UBER pool. This thread pool is managed by Mule and shared across all apps in the same Mule instance. At startup, Mule introspects the available resources (such as memory and CPU cores) in the system and tunes automatically for the environment where Mule is running. This algorithm was established through performance testing and found optimal values for most scenarios.

This single thread pool allows Mule to be efficient, requiring significantly fewer threads (and their inherent memory footprint) to process a given workload when compared to Mule 3.

The `proactor design pattern` is used, so the different operations of a Mule flow are classified in categories and executed with threads of I/O, CPU_LIGHT, or CPU_INTENSIVE depending on the task. Some thread switches are omitted — for example, if a CPU_INTENSIVE is followed by a CPU_LIGHT operation, that task will remain in the CPU_INTENSIVE thread.

## Thread pool responsibilities

The source of the flow and each event processor must execute in a thread that is taken from one of the three centralized thread pools (with the exception of the selector threads needed by HTTP Listener and Requester). The task accomplished by an event processor is either 100% nonblocking, partially blocking, or mostly blocking.

![image](https://github.com/user-attachments/assets/eca702eb-a6d2-4276-86bd-e2417ce53dde)

The CPU_LITE pool is for tasks that are 100% non-blocking and typically take less than 10ms to complete. The CPU_INTENSIVE pool is for tasks that typically take more than 10ms and are potentially blocking less than 20% of the clock time. The BLOCKING_IO pool is for tasks that are blocked most of the time.

## CPU Light

These schedulers should be used for asynchronous tasks that complete really quickly without significant CPU consumption. They can also be used for tasks that perform non-locking I/O. 

Examples include simple validations, light calculations, or any kind of logic that doesn’t perform I/O and takes around 10 ms to complete.

For quick operations (around 10 ms), or nonblocking I/O, for example, a Logger `(logger)` or HTTP Request operation `(http:request)`. These tasks should not perform any blocking I/O activities. The applicable strings in the logs are `CPU_LIGHT` and `CPU_LIGHT_ASYNC`.

## CPU Intensive

For CPU-bound computations, usually taking more than 10 ms to execute. These tasks should not perform any I/O activities. One example is the Transform Message component `(ee:transform)`. The applicable string in the logs is `CPU_INTENSIVE`

Examples include encryption, heavy transformations, expensive validations, and any other kind of logic that doesn’t perform I/O and makes heavy use of the CPU for more than 20 ms.

## IO Scheduler ( Blocking I/O )

For I/O that blocks the calling thread, for example, a Database Select operation `(db:select)` or a SFTP read `(sftp:read)`. Applicable strings in the logs are `BLOCKING` and `IO`.

## HTTP thread pools

The Mule 4 HTTP module uses Grizzly under the covers. Grizzly needs selector thread pools configured. Java NIO has the concept of selector threads. These check the state of NIO channels and create and dispatch events when they arrive. The HTTP Listener selectors poll for request events only. The HTTP Requester selectors poll for response events only.

There is a special thread pool for the HTTP Listener. This is configured at the Mule runtime level and shared by all applications deployed to that runtime. There is also a special thread pool for the HTTP Requester. This is dedicated to the application that uses an HTTP Requester. So 2 applications on the one runtime both using an HTTP Requester will have one selector pool each for that HTTP Requester. If they both use an HTTP Listener they will share the one pool for the HTTP Listener.

![image](https://github.com/user-attachments/assets/4c83284c-2aab-405c-9516-809e63c6755c)

### Treadpool Sizing

![image](https://github.com/user-attachments/assets/592cda33-5c8f-488d-9480-f1aa1f6b7ca8)

![image](https://github.com/user-attachments/assets/6c8f49ad-d1c8-44b2-9a9d-4e8089676144)

![image](https://github.com/user-attachments/assets/50041472-027e-49da-ae0d-5a64cb6e5abd)

![image](https://github.com/user-attachments/assets/65d88a99-74d4-4078-a1b1-7e4b86ef5511)


`C:\AnypointStudio-7.21.0\AnypointStudio\plugins\org.mule.tooling.server.4.9.ee_7.21.0.202502030106\mule\conf`

- scheduler-pools.conf
  
```
#The strategy to be used for managing the thread pools that back the 3 types of schedulers in the Mule Runtime
#(cpu_light, cpu_intensive and I/O).
#Possible values are:
#- UBER: All three scheduler types will be backed by one uber thread pool (default since 4.3.0)
#- DEDICATED: Each scheduler type is backed by its own Thread pool (legacy mode to Mule 4.1.x and 4.2.x)
org.mule.runtime.scheduler.SchedulerPoolStrategy=UBER
```

- wrapper.conf

### Typical thread switching scenario

![image](https://github.com/user-attachments/assets/89953737-d377-4b56-b34c-340d02f005d9)

#### Try scope with Transaction

![image](https://github.com/user-attachments/assets/19bee320-9808-4ff9-95cf-86f87f983a3b)

#### JMS Transactional

![image](https://github.com/user-attachments/assets/2cc51f07-9f47-40d3-809e-01270b063894)

#### JMS transactional with Async scope

![image](https://github.com/user-attachments/assets/06d6ebbe-c3ef-4612-af17-bec1814bb0ff)

## Observer Pattern

![image](https://github.com/user-attachments/assets/ac2985c2-dd92-40af-959b-085cfc12ff6f)

## Flowback Pressure

Back pressure can occur when, under heavy load, Mule does not have resources available to process a specific event. This issue might occur because all threads are busy and cannot perform the handoff of the newly arrived event, or because the current flow’s maxConcurrency value has been exceeded already.

If Mule cannot handle an event, it logs the condition with the message `Flow 'flowName' is unable to accept new events at this time`. Mule also notifies the flow source, to perform any required actions.

The actions that Mule performs as a result of back-pressure are specific to each connector’s source. For example -
 - `http:listener` might return a `503 error code`
 - while a message-broker listener might provide the option to either wait for resources to be available or drop the message.
 - In some cases, a source might disconnect from a remote system to avoid getting more data than it can process and then reconnect after the server state is normalized.
   
![image](https://github.com/user-attachments/assets/80c1c01e-2678-4a79-8eda-3cfc6179e58c)

## Takeaways from performance testing

- The performance of Mule 4.3 and ability to withstand stress tests outperformed my expectations. It can handle more than 500 API calls per second in a small worker of 500 MB, and the CPU is still below 80%.
- The overhead of DataWeave is not excessive. Although the API has used operations such as now(), upper(), substringAfterLast(), the response time was not affected.
- The invocation of other APIs using HTTP Request is very fast, as it only adds five milliseconds to the response time. Keep in mind that Client ID enforcement policies are executed in every request of the API, but they are not adding significant overhead.
- The number of threads of the worker was able to scale from the initial set of 83 threads to 118, which is an increase of 35 threads
