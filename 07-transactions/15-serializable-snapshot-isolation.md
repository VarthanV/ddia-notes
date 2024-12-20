# Serializable Snapshot Isolation (SSI)

- It provides full serializability but has only a small performance penalty compared to snapshot isolation.

## Pessimistic Vs optimistic concurrency-control

- Two-phase locking is also called **pessimistic concurrency** control mechanism, it is based on the principle of anything might go wrong , It is better to wait until the situation is safe again before doing
anything. It is like **mutual exclusion** which is used to protect DS in multi-threaded programming.

- Serial exeuction in a sense pessimistic to extreme, it is essentially equivalent each txn having an exclusive lock on the entire database for one partition for duartion of each txn.

- It is compensated by making each txn fast to execute so only lock is holded for short time.

-  Serializable Snapshot isolation(SSI) is an **optimistic concurrency control** technique. 

- Instead of blocking something ptoentially dangerous happens txn's continue anwyay. 

- When txn wants to commit the database checks if anything bad happened (isolation violated) if so the txn action is aborted and retried. Only the txn that executed serially is allowed to commit.

- It performs badly if there is high contention as this leads to a higher propotion of txn needing to abort . If the system is already close to maximum throughput the addition txn load can make performance worse.

- However if there is enough spare capacity and if contention is not too high , optimistic concurrency techniques tend to perform better than pessimistic ones. Contention can be reduced with commutative atomic operations.

- On top of snapshot isolation SSI adds an algorithm for detecting serialization conflicts among writes and which txns to abort.

