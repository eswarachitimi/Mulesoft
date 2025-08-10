# Pipes and Filters
How can we perform complex processing on a message while maintaining independence and flexibility?

<img width="529" height="90" alt="image" src="https://github.com/user-attachments/assets/a67aca00-023d-4c8f-9163-13ba453555a6" />

Use the Pipes and Filters architectural style to divide a larger processing task into a sequence of smaller, independent processing steps (Filters) that are connected by channels (Pipes).

# Message Router
How can you decouple individual processing steps so that messages can be passed to different filters depending on a set of conditions?

<img width="494" height="144" alt="image" src="https://github.com/user-attachments/assets/af5c6fab-b9bd-46aa-b6be-cc1c2e9a1fe0" />

Insert a special filter, a Message Router, which consumes a Message from one Message Channel and republishes it to a different Message Channel channel depending on a set of conditions.

# Content-Based Router
How do we handle a situation where the implementation of a single logical function (e.g., inventory check) is spread across multiple physical systems?

<img width="490" height="118" alt="image" src="https://github.com/user-attachments/assets/5e139d90-bffd-4dc6-afda-ee9ef797b868" />

Use a Content-Based Router to route each message to the correct recipient based on message content.

# Message Filter
How can a component avoid receiving uninteresting messages?

<img width="576" height="107" alt="image" src="https://github.com/user-attachments/assets/208e477b-66ce-43b8-be56-25b6bfd162ca" />

Use a special kind of Message Router, a Message Filter, to eliminate undesired messages from a channel based on a set of criteria.

# Dynamic Router
How can you avoid the dependency of the router on all possible destinations while maintaining its efficiency?

<img width="494" height="243" alt="image" src="https://github.com/user-attachments/assets/43dc1c56-61a7-4980-8779-7a8fc213175f" />

Use a Dynamic Router, a Router that can self-configure based on special configuration messages from participating destinations.

# Recipient List
How do we route a message to a list of dynamically specified recipients?

<img width="462" height="197" alt="image" src="https://github.com/user-attachments/assets/25698797-94a7-42c1-b155-fcc57b3fe9e7" />

Define a channel for each recipient. Then use a Recipient List to inspect an incoming message, determine the list of desired recipients, and forward the message to all channels associated with the recipients in the list.

# Splitter
How can we process a message if it contains multiple elements, each of which may have to be processed in a different way?

<img width="477" height="126" alt="image" src="https://github.com/user-attachments/assets/62c12455-aa67-4304-b0f6-e64d21e8f018" />

Use a Splitter to break out the composite message into a series of individual messages, each containing data related to one item.

# Aggregator

How do we combine the results of individual, but related messages so that they can be processed as a whole?

<img width="450" height="134" alt="image" src="https://github.com/user-attachments/assets/9b0beaa1-a5d3-42d7-abf6-478b0f475499" />

Use a stateful filter, an Aggregator, to collect and store individual messages until a complete set of related messages has been received. Then, the Aggregator publishes a single message distilled from the individual messages.

# Resequencer

How can we get a stream of related but out-of-sequence messages back into the correct order?

<img width="403" height="106" alt="image" src="https://github.com/user-attachments/assets/77992c98-445f-4ae2-a3fe-972bd3b616b0" />

Use a stateful filter, a Resequencer, to collect and re-order messages so that they can be published to the output channel in a specified order.

# Composed Message Processor

How can you maintain the overall message flow when processing a message consisting of multiple elements, each of which may require different processing?

<img width="606" height="220" alt="image" src="https://github.com/user-attachments/assets/8fe05d0c-2d73-48cf-b754-2d8dfdd8ee10" />

Use Composed Message Processor to process a composite message. The Composed Message Processor splits the message up, routes the sub-messages to the appropriate destinations and re-aggregates the responses back into a single message.

# Scatter-Gather

How do you maintain the overall message flow when a message needs to be sent to multiple recipients, each of which may send a reply?

<img width="377" height="226" alt="image" src="https://github.com/user-attachments/assets/3d34b1b8-a7ab-4d55-a1c2-c4102005d9a7" />

Use a Scatter-Gather that broadcasts a message to multiple recipients and re-aggregates the responses back into a single message

# Routing Slip

How do we route a message consecutively through a series of processing steps when the sequence of steps is not known at design-time and may vary for each message?

<img width="429" height="197" alt="image" src="https://github.com/user-attachments/assets/05382894-7056-4b2a-ad77-903b9f75ca46" />

Attach a Routing Slip to each message, specifying the sequence of processing steps. Wrap each component with a special message router that reads the Routing Slip and routes the message to the next component in the list.

# Process Manager

How do we route a message through multiple processing steps when the required steps may not be known at design-time and may not be sequential?

<img width="315" height="157" alt="image" src="https://github.com/user-attachments/assets/5d96f9fc-df66-42a8-bc3b-30b255516d85" />

Use a central processing unit, a Process Manager, to maintain the state of the sequence and determine the next processing step based on intermediate results.

# Message Broker

How can you decouple the destination of a message from the sender and maintain central control over the flow of messages?

<img width="350" height="204" alt="image" src="https://github.com/user-attachments/assets/2214a7b1-a27b-44d7-ad86-9f927b4e4d51" />

Use a central Message Broker that can receive messages from multiple destinations, determine the correct destination and route the message to the correct channel. Implement the internals of the Message Broker using the design patterns presented in this chapter.

