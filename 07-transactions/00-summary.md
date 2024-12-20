# Summary

## Dirty reads

One client reads another clients writes before they have been commited. The read committed isolation level and stronger levels prevent dirty reads.

## Dirty Writes
One client overwrites data that another client has written but not yet committed. Almost all txn implementations prevent dirty writes.

## Read Skew
- A client sees different part of database at different point in time. 

- Some cases of read skew is also known as **nonrepetable reads**.

- The issue is prevented with snapshot isolation which allows a txn to read from a consistent snapshot corresponding to one particular point in time. It is usually implemented with Multiversion concurrency control (MVCC).

## Lost updates 
- Two clients concurrently perform a read-modify-write cycle. One overwrites others change without incorprating its changes so data is lost.

- Some implementation of snapshot isolation prevent this automatically while others require manual lock (``SELECT FOR UPDATE``)

## Write Skew
- A txn reads something and makes decision based on the value it saw and writes the decision to database. However by the time write is made the premise of decision is no longer true. Only serializable isolation fixs this

## Phantom reads

- A txn reads objects that match some search condition.

- Another client makes a write that affects the results of search.

- Snapshot isolation prevents straightforward phantom reads but phantoms in context of write skew required special technique like **index range lock**.

Weak isolation levels protect against some of these anomalies but leave the application developer to handle others manually using explicit locking . only serializable isolation protects against these issues.

## Literally executing transactions in a serial order

- If we can make each txn very fast to execute and the transaction throughput 
is low enough to process on a single CPU core that is a simple and effective option.

## Two phase locking

- Avoid using for performance charecterisicts


## Serializable Snapshot Isolation(SSI)

- It uses an optimisitc approach allowing txns to proceed without blocking. When a txn wants to commit , it is checked and it is aborted if the execution is not serializable


