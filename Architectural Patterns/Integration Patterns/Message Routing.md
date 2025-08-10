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
