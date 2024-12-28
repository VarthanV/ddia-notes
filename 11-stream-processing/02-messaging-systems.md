# Messaging Systems

-  A common approach for notifiying consumers about new events is to use **messaging system**.

- A producer sends a message containing the event which is then pushed to consumers.

- A direct communication channel like a  Unix pipe or TCP connection between producer and consumer is a simplest way for implementing message systems.

- Most systems expand on the basic model, UNIX pipe and TCP connect excatly one sender with one recipient where as messaging system allows multiple producer nodes to send messages to same topic and 

## Direct messaging from producer to consumers

- UDP multicast is widely used in the financial industry for streams such as stock market feeds ,where low latency is important. UDP itself is unreliable but application level protocols can recover lost packets.

- Brokerless messaging lib such as ZeroMQ and nanomsg take a similar approach by implementing pub/sub over TCP or IP multicast.


- Direct messaging requires to consumer to be having high availability and it is active processor , there is potential loss of message during retries and we are dependent on single node and losing the message beacuse of external cause.


