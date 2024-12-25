# Sequence Number Ordering

- Casuality is an important theoretical concept actually keeping tracking of all casual dependencies can be impractiable, In many applications client read lots of data before writing something.  

- It is not clear whether the write is casually dependent on all or only some of those priort reads. Explicitly tracking all the data that has been written is a large overhead.

- There is a better way we can use **sequence numbers or timestamps** to order events. 

- A timestamp need not come from a time-of-day clock , it can come from instead a **logical clock**.

- It is an algorithm to generate sequence of numbers to identify operations typically using counters that are incremented for every operation.

- Such sequenece numbers or timestamps are compact and they provide total order. (i.e.) every OP has unique sequence number and we can always compare two sequence numbers to determine which is greate

- In particular we can create seq numbers in total order that is consistent with casuality.

- If operation A casually happened before B, then A occurs before B in total order.

- In case of single leader replication the leader might attach a sequence number to each log and when replicated to the follower if the follower applies the change in the casual order , then the replica is casually consisten(even if it is lagging behind the leader).

