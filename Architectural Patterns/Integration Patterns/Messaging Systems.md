An enterprise has two separate applications that are communicating via Messaging, using a Message Channel that connects them.

# Message

How can two applications connected by a message channel exchange a piece of information?

<img width="282" height="96" alt="image" src="https://github.com/user-attachments/assets/bd2f5b54-14dc-46b0-ac86-eb3c351fb75b" />

Package the information into a Message, a data record that the messaging system can transmit through a message channel.

Thus any data that is to be transmitted via a messaging system must be converted into one or more messages that can be sent through messaging channels.

A message consists of two basic parts:

`Header –` Information used by the messaging system that describes the data being transmitted, its origin, its destination, and so on.

`Body –` The data being transmitted; generally ignored by the messaging system and simply transmitted as-is.
