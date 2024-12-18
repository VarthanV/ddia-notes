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

