# Linarizability

- Database gives a illusion that there is only one replica .So that every client would have the same view of the data and don't need to worry about replication lag. This is the idea behind **linearizability**, **atomic consistency**.

- In linearizalbe system , if one client finishes the write all other clients in the cluster must be able to read the data that was writeen.

- Maintaining an illusion of single copy of data means guaranteeing the value read is the most recent upto date value and doesn't come from stale cache or replica.

## What makes system Linearizable?

![alt text](../assets/read-req-with-concurrent-write.png)

- In this example the register has two types of operation

**read(x)** = > v means the client requested to read the value of register x and database returned the 
value v

**write(x,v)**  => r means the client requested to set the register x to value v and the database returned response r


The value of x is initially 0 and client C performs a write request to set it to 1 . While this is happening clients A and B are repeatedly polling the database to read the lates value. What are the possible
responses that A and B