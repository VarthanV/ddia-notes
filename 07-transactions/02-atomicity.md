# Atomicity

-  In general atomic refers to something that cannot be broken down into smaller parts.

- Atomicity describes what happens if a client wants to make several writes but a fault occurs after some of the writes have been processed. For example a process crashes , network interruption ,disk becomes full or integrity constraint is violated. 

- If the writes are grouped together in atomic txn and the txn cannot be commited. due to fault then the transaction is aborted and the database must discard or undo any writes it has been made so far in the txn.

- Without atomicity it is difficult to track multiple changes made and which effects have taken place and which haven't and difficult to rollback. 

- Atomicity ensures that if a txn is aborted nothing has been changed from the original state and it didn't change anything.

- The ability to abort a txn on error and have all writes from that transaction discarded is defining the feature of ACID atomicity. 
