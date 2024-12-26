# Membership and Coordination Services

- Projects like Zookeeper or etcd are often described as distributed key value stores or coordination and configuration services.

## Features

- **Linearizable Atomic operation**: Using an atomic compare-and-set op, can implement a lock , if several nodes concurrently try to perform the same operation only one of them will succeed. The consensus protocol guarantees that the OP will be atomic and linerizalbe  even if a node fails or network is interrupted at any point. A distributed lock is implemented as **lease** which has expiry time so that it is eventually released if client fails.

- **Total ordering of operations**:  When some resource is protected by a lock or lease we need a **fencing token** to prevent clients from conflicting with each other in case of process pause. The fencing token is a number that monotonically increases when a lock is acquired. 

- **Failure Detection**: Clients maintain a long lived session on zookeeper servers and client and the server periodically exchange heartbeats to checj that other node is still avlie. Even if the connection is temporarily interrupted or a zookeeper. Even if the connection is temporarily interrupted or a zookeeper node fails the session remains active. If heartbeats cease for a duration that is longer than session timeout. Zookeeper declares the session to be dead. Any locks configured  by the zookeeper can be automatically released when the session tiesmout.

- **Change notification**: Not only can one client read locks and values that were created by another client but it can also work for changes. Thus a client can find out when another client joins the cluster or if another client fails. By subscribing to notifications a client avoids having to frequently poll about changes.

---

A **fencing token** is a mechanism used in distributed systems and concurrency control to enforce a strict sequence of access or operations, particularly in leader-based setups or situations involving resource contention. It is often employed to ensure safety and consistency in scenarios where multiple nodes or clients might compete for access to a shared resource.



### Key Features of a Fencing Token:
1. **Strictly Increasing Value**:  
   The token is typically a monotonically increasing number (e.g., a timestamp, sequence number, or logical clock). Each time a new token is issued, it has a value strictly greater than the previous one.

2. **Issued by a Central Authority**:  
   Usually, a central entity (like a leader or a distributed lock manager) generates and issues fencing tokens to ensure their uniqueness and order.

3. **Validity Check**:  
   Before a client is allowed to operate on a resource, the resource manager verifies the token. Only operations with the latest or highest token are allowed.

---

### **Example Scenario:**
Imagine a distributed system where multiple clients acquire a lock to write to a shared database. To prevent stale or failed clients from writing invalid data:
1. The lock service (e.g., using ZooKeeper or Consul) issues a fencing token each time a client acquires the lock.
2. The client must present this token when accessing the resource.
3. The resource (database) validates the token. If a client presents an outdated token (lower number), its request is rejected.

---

### **Why Is This Needed?**
Fencing tokens prevent **split-brain scenarios** or **stale lease problems**, where a client might incorrectly assume it still has access to a resource after its lock has expired or been taken over by another client.

For instance:
- A client might crash and later revive, unaware that its lock has been reassigned.
- Without fencing, the revived client might overwrite newer data or interfere with the operations of the legitimate lock holder.

---

### **Real-world Use Cases:**
1. **Distributed Locking**: To enforce proper ordering of lock acquisition.
2. **Leader Election**: Ensuring the old leader cannot interfere after losing leadership.
3. **Cloud-native Systems**: Services like etcd, ZooKeeper, and Consul often employ fencing tokens.
4. **Database Systems**: Used in clustered databases to ensure consistent writes.

---


