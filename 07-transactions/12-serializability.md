# Serializability

- Serializable isolation is usually regarded as the strongest isolation level.

- It guarantees even though transactions may execute in parallel the end result in the same as if they had executed one at a time serially without any concurrency.

- Thus if database guarantees that if the transaction behave correctly wen run individually they continue to be correct when run concurrently.

- Database prevents all race conditions.

- Below are the ways to implement Serialzability
    - Executing transactions in a serial order
    - Two phase locking
    - Optimistic concurrency contol (Serializable Snapshot Isolation)