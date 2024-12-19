# Preventing lost updates

- The read committed and snapshot isolation levels have primarily been about guarantees of what a read only transaction can see in the presence of concurrent writes. 

- There are several other conflicts that can occur between concurrently writing transactions. The best known is the **lost update problem**.

- The lost update problem occurs if an application reads some value from the database , modifies it and writes back the modified value (read-modify-write cycle).

- If two txn do this concurrently one of the modifications can be lost because the second write doesn't include the first modification . This pattern occurs in different scenarios

## Scenarios for Lost update

- Incrementing a counter or updating the account balance (requires reading current value, calculating new value and writing back the updated value)

- Making a local change to complex value (eg adding an element to a list within a JSON document,requires parsing the document and making changes).

- Two users editing a wiki page at the same time , where each user saves their changes by sending the entire page contents to the server ,overwriting whatever is currently in the database.

## Solutions for Lost updates
---

## Atomic Write Operations

- Many databases provide atomic update operations which remove the need to implement read-modify-update write cycles in application code. They are the best solution if code can be expressed in terms of those operations.Below instruction is concurrency safe

```sql
    UPDATE counters SET value = value+1 where key = 'foo';
```

- Similarly document db like mongodb provided atomic OP for making local modification for part of JSON and Redis provides atomic op for modifying data structures such as priority queue.

- Not all writes can be expressed in terms of atomic OP , for example the updates to a wiki page involve arbitary text editing. but where atomic OP can be used it is best choice.

- Atomic OP can be implemented by taking an exclusive lock on the object whene it is read so no other txn can read it until the update has been applied.

- The technique is known as **cursor stability**. Another option is to simply force all atomic operations to be executed on single thread.

## Explicit Locking

-  If the databases built in atomic operation doesnt provide the necessary functionality , is for the application to explicitly lock the objects that are going to be updated.

- Thus the application can perform a read-modify-write cycle and if any other txn tries to concurrently read the same object it is forced to wait until the first read-modify-write cycle has been completed.

- Consider a multiplayer game in which several players can move the same figure concurrently, in this case an atomic OP may not be sufficient , because the app needs to ensure that a players move abides by the rule of the game which involves some logic we cannot implement in db query.

- Instead we can lock to prevent two players from concurrently moving the same peace

```sql
BEGIN 

SELECT * from figures where name = 'robot'
and game_id = 222
FOR UPDATE;

UPDATE figures set postion='c4' where id=1234;
COMMIT;
```

- The ``FOR UPDATE`` clause indicates that the database should take a lock on all rows returned by this query.

- This works but to get it right we should be careful when taking locks so we dont introcduce a race condition

## Automatically detecting lost updates

- Atomic operations and locks are way of preventing lost updates by forcing the read-modify-write-cycles to happen sequentially. 

- An alternative is to allow them to execute in parallel and if the txn manager detects a lost update , abort the txn and forceit to retry the cycle.

- Databases can perform this check efficiently in conjuction with snapshot isolation 

- Loss update happens automatically and less error prone so the application dont need to worry about locking ,race conditions etc


## Compare and set

- In databases that dont provide txn we find an **atomic compare and set operation**.

- The purpoe of this operation is to avoid lost updates by allowing an updated to happen only if the value has not changed since the last read.

- If the current value doesnt match with the previous value the update has no effect and we need to do read-modify-write cycle again.

- For example n a wiki page we may do like this

```sql
    UPDATE wiki_pages SET content = 'new content'
    where id=1234 and content='old content'
```

- If the content changed no longer matches the old content this will have no effect. So we need to retry if necessary depending on the rows affected value.

- However we need to check the isolation level since if we are reading from an old snapshot this update may occur and lost updates it not detected.


 


