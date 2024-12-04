# Multi Leader Replication

- Leader based replication has one major flaw, All writes go through a single leader, if the leader node goes down writes are blocked.

- Extension of this model is to allow more than one leader to accept writes.

- Replication still happens the same way each node that processes a write must forward the data change to all other nodes. 

- This is known as **multi-leader,master/master or active/active** replication

- Each leader simultaneoulsy acts as follower to other leaders.

