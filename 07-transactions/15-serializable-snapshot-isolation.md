# Serializable Snapshot Isolation (SSI)

- It provides full serializability but has only a small performance penalty compared to snapshot isolation.

## Pessimistic Vs optimistic concurrency-control

- Two-phase locking is also called **pessimistic concurrency** control mechanism, it is based on the principle of anything might go wrong , It is better to wait until the situation is safe again before doing
anything. It is like **mutual exclusion** which is used to protect DS in multi-threaded programming.

