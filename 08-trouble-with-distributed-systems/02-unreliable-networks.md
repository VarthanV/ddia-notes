# Unreliable Networks

- Distributed systems are basically **shared-nothing systems** 

- Bunch of machines connected by a network , the network is the only way that those machines can communicate.

- It is assumed that each machine has its own memory and disk.and one machine cannot access another machines memory or disk (except by naking requests to other service over network).

- Shared nothing is comparitively cheap and can make use of cloud services more.

- Data redundancy can be acheived by replicating the data across geographically distrivuted datacenters.

- The internet and most network in the data centers are **asynchornous packet networks**.

- This kind of network one node can send message to another node but the network gives no guarantees as to when it will arrive or whether it will arrive at all.


## Request Response cycle problems

- Request may be have been lost (someone unplugged a network cable)

- Request may be waiting in a queue and will be delivered later (network of the recipient is overloaded).

- The remote node may have been failed (crashed or power down).

- The remote node may have temporarily stopped responding (gc process pauses).

- The remote node processed the request but the response has been lost on network.

- The remote node has processed network but response is delayed and delivered later.



- The usual way of handling the issue is **timeout** after sometime we give up waiting and assume that response is going to arrive , when a timeout occurs we dont know whether the remote node got the request or not. 