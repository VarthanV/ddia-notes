# Ordering Guarantees

- If system obeys the ordering imposed by casualty. we say the system is casually consistent ,snapshot isolation provides casual consistency , when we read from database and see some pieces of data , then we must be able to see any data that causally preceeds it(assuming it is not deleted in meantime)

## Casual order is not total order

- A **total order** allows any two elements to be compared ,so if we have two elements we can say which one is greater and which one is smaller 

**Lineraizability**

- In a linearizable system we have a total order of operations, if the system behaves as if there is only a single copy of the data and every operation is atomic, this means that for any two of operations we can see which happened fast.

**Casuality**

- We said two operations are concurrent if neither happened before the other, but they are incomparable if they are concurrent. This means casualty defines a partial order not a total order. some ops are ordered with respect to each other but some other are incomparable.


# Casual dependencies

In **distributed systems**, a **causal dependency** refers to the relationship between events or actions where one event causally influences another. This means that the occurrence of the second event depends on or is influenced by the occurrence of the first event. Such dependencies are critical for maintaining **causal consistency** and understanding the behavior of distributed systems.

### Key Concepts in Causal Dependency in Distributed Systems

1. **Happens-Before Relation (\( \to \))**:
   - Defined by Leslie Lamport, the **happens-before relation** captures causal dependencies between events in a distributed system. 
   - If event \( A \) happens before event \( B \) (\( A \to B \)), it implies:
     - \( A \) occurs on the same process before \( B \), or
     - \( A \) sends a message to another process, and \( B \) is the receipt of that message.
   - \( A \to B \) is **transitive**, meaning if \( A \to B \) and \( B \to C \), then \( A \to C \).

2. **Message Passing**:
   - Causal dependency arises naturally in message-passing systems. If a message is sent by one process and received by another, any event that occurs after receiving the message is causally dependent on the sending event.

3. **Causal Consistency**:
   - A distributed system is **causally consistent** if it ensures that operations are observed in an order that respects causal dependencies.
   - For example:
     - Process \( A \) writes \( x = 1 \).
     - Process \( B \) reads \( x = 1 \) and writes \( y = 2 \).
     - Process \( C \) should not read \( y = 2 \) before observing \( x = 1 \).

4. **Vector Clocks**:
   - Vector clocks are often used to track causal dependencies in distributed systems.
   - Each process maintains a vector of counters, and these counters are incremented or updated based on events and communication between processes.
   - By comparing vector timestamps, a system can determine if one event causally depends on another.

5. **Eventual Consistency vs. Causal Consistency**:
   - In **eventual consistency**, updates propagate to all replicas, but the order may not respect causal dependencies.
   - In **causal consistency**, updates propagate in a manner that respects causal order, ensuring users observe related events in the correct sequence.

### Example
Consider three processes (\( P1, P2, P3 \)) in a distributed system:

1. \( P1 \) performs \( A: \) write(x=1).
2. \( P2 \) observes \( A \) and performs \( B: \) write(y=2).
3. \( P3 \) reads \( y=2 \). To ensure causal consistency, \( P3 \) must also see \( x=1 \).

If \( P3 \) reads \( y=2 \) but \( x \neq 1 \), the causal dependency between \( A \) and \( B \) is violated.

### Importance
Causal dependencies are crucial for:
- **Data consistency**: Ensuring operations in distributed databases or systems are applied in the correct order.
- **Debugging**: Identifying the cause of faults or unexpected behaviors.
- **Concurrency control**: Maintaining correctness in concurrent executions.

