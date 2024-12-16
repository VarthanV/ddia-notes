# Consistency

- The idea of ACID consistency is that we have certain statements about our data (**invariants**) that must always be true, For example in an accounting system , credits and debits across all accounts must be balanced.

- If a txn starts with a database that is valid according to these invariants and writes during the txn
preserves the validity then we can ensure that the invariants are always satisfied.


- However the idea of consistency depends on the applications notion of invariants and its applications responsibility to define its txns correctly so they preserve consistency.

- Some consistency constraints can be checked by db like foreign key or uniquness constraints.

- Consistency in a DB can be achieved through Atomicity and Isolation