# Two-Phase Locking (2PL)

- Two-Phase Locking makes the lock requirement much stronger

- Several transactions are allowed to concurrently read the same object as long as nobody is writing to it. 

- But as soon as anyone wants to write (modify or delete) an object exclusive access is required
    - If transaction A has read an object and transction B wants to write that object, B must wait until A commits or aborts before it can continue.

    - If transaction A has written an object and B wants to read the object , B must wait until A commits or aborts before it can continue.


## Implementation of 2PL

- The blocking of readers and writers is implemented by having a lock on each object in the database. The lock either can be in **shared mode** or **exclusive mode**.

- If a transaction wants to read an object , it must first acquire the lock in shared mode. Several txns are allowed to hold the lock in shared mode , but if another txn already has an exclusive lock on the objects these txns must wait.

- If txn wants to write an object, it must first acquire the lock in exclusive mode. No other txn may hold the lock at the same time (either in shared or exclusive mode).  So if there is any existing lock on the object the txn must wait.

- If txn first reads then writes and object , it may upgrade its shared lock to an exclusive lock, The upgrader  works as same as getting exclusive lock.

- After a txn has acquired the lock it must continue to hold the lock until the end of the txn (commit or abort). This is where the name two phase commit comes , the first phase is when the locks are acquired and second phase is when the locks are released.

- If txn A is stuck waiiting for txn B to release its lock, this situation is called **deadlock**. 

- The database automatically detects the deadlock between txns and aborts one of them so that others can make progress. The aborted txn needs to be retried by the application.


## Performance of Two phase locking

- Transaction throughput and response times of queries are significantly worse under two
phase locking under weak isolation.

-  This is partly due to overhead of acquiring and releasing all those locks, but more importantly due to
reduced concurrency. By design if two concurrent txns try to do anything that may in result in race condition
one has to wait for other to complete.

- Traditional databases dont limit the duration of a transaction, because they are designed for 
interactive application that will wait for human input.

- Although deadlocks can happen with lock based read committed isolation level, they occur much more frequently
under 2PL serializable isolation.

## Predicate locks

- A database with serializable isolation must prevent phantoms.

- Predicate Lock works similar to shared/exclusive lock but rather than belonging to a particular object 
(one row in a table) it belongs to all objects that match some condition such as

```sql
    SELECT * from bookings
    where room_id = 123 and end_time > '2024-01-01 12:00' and
    start_time < '2024-01-01 13:00';
```

- A predicate lock restricts access as follows
    - If transaction A wants to read objects matching some condition like in the SELECT query 
    it will acquirea shared mode predicate lock on the conditions of the query. If another txn B currently has an exclusive lock
    of any object matching those conditions. A must wait until B releases its lock before its allowed to make its 
    query

    - If txn a wants to CRUD any object. it must first check whether the old or the new value matches any existing
    predicate lock. If there is a matching predicate lock held by transaction B , then A must ewait until B has 
    committed or aborted before it can continue.


- The key idea here is that a predicate lock applies even to object that do not yet exist in the datbase, 
but which might be added in future(phantoms). If two-phase locking includes predicate locks , the database prevents
all the forms of write-skew and other race conditions and so its isolation becomes serializable.

## Index range locks

- Unfortunately predicate locks do not peform well , if there are many locks by active txns , checking for matching 
locks becomes times consuming.

- The reason most database with 2PL actually implement index-range-locking which is simplified approximation
of predicate locking.

- Its safe to simplify a predicate by making it match a greater set of objects.

- In room bookings database you would probably have an index on the room_id , column and indexes on 
start_time and end_time (otherwise the preceding query would be very slow on large DB)

- Say your index is on ``room_id`` and database uses this index to find existing bookings for room 123. 
Now that DB can simply attatch a shared lock to this index entry. indication that a txn has be searched for 
bookings for room 123.

- Alternatively if the database uses a time based index to 
find existing bookings it can attach a shared lockedto a range of values in that index. 
indicating that the txn has already searched for bookings that overlap with 
the time period of noon to 1pm on jan 2024.

- Either way an approximation of the search condition is attached to one of the indexes. 
Now if the another txn  want to insert , updated or delete a booking for the same room or overlapping
time period , it will have to update the same index range . so it will encounter the shared lock and it will
be forced to wait until the lock is released.

- This provides effective protection against phantoms and write skew, Index range locks are not a precise
as predicate locks would be (they lock a bigger range of objects to maintain serializabliyy).

- If there is no suitable index to lock the database falls back to shared lock on entire table.It is not good for
performance but safe fallback position.

