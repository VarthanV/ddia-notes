# Total Order Broadcast

- If program runs on a single CPU core it is easy to define a total ordering of operations, it is simply the order which was executed by CPU. 

- However dist system getting all nodes to agree on same total ordering OP is tricky. 

- The challenge is how to scale the system if the throughput is greater than a single leader can handler and how to handle failover if the leader fails in distributed systems , this problem is known as **total order broadcast** or **atomic broadcast**.

- Total order broadcast is usually described as protocol for exchanging messages between nodes, It needs two safety property to be satisfied.

**Reliable Delivery**: No messages are lost , if message is delivered to one node it is delivered to all nodes.

**Totally ordered delivery**: Messages are delived to every node in same order

- A correct algorithm for total order broadcast must ensure the reliability and ordering properties are always satisifed, even if a node or the network is faulty , Messages will not be delivered while the network is interrupted but an algorithm can keep trying so that the messages get through when the network is eventually repaired


## Using total order broadcast

- Consensus services such as Zookeper and etc implement total order broadcast . 

- Total Order broadcast is what we excatly need for database replication , if every message represents a write to the db and every replica processes the same writes in the same order , then the replicas will remain consistent with each other (aside from any replication log). This principle is know as **state nachine replication**.

- They can also be used to implement serializable transactions , if every message represents a deterministic txn to be executed as stored procedure and if every node process those messages in same order , thn partitions and replicas are kept consistent with each other.

- Important aspect of total order broadcast is order is fixed at the time messages are delivered, a node is not allowed to insert a message into earlier position in the order if subsequent messages have already been deloverd.

- Another way of total order broadcasting is creating a **log** , delivering a message is like appending to the log. Since all nodes must deliver the same messages in the same order all nodes can read the log and see the sequence of message.

- It is also useful for implementing a lock service that provides fencing tokens. 

- Every request to acquire the lock is appended as message to the log and all messages are sequentially number ied in the order they appear in the log. 

- The seq number is monotonically increasing so it acts a fencing token. In zookeeper it is called as **zkid**

