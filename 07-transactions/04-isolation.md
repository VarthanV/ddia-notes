# Isolation

-  When two or more threads modify the same database records we can run into race conditions

- Isolation means that concurrently executing transactions are isolated from each other. they cannot step on each other toes.

- We formalize isolation as **serializablity** which means that each txn pretends that it is the only txn running on the entire database. The database ensures that when txn has commited , the result is same as they if have run serially even though they may have run concurrently.