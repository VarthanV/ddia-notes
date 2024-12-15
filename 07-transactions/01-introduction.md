# Transactions

## Introduction

- In reality of data systems, many things can go wrong  
    - The database software or hardware may fail at any time (including in middle of a write operation)

    - The application may crash at any time (including halfway through a series of operations)

    - Interruptions in the network can unexpectedly cut off the application from the database or one database node from another.

    - Serveral clients may write to database overwriting each other's changes.

    - A client may read data that doesn't make sense because it has only partially been updated.

    - Race condition can unpredicted bugs


- For to build a reliable system we need to deal with this faults and ensure that they dont cause any caastrophic failure of the entire system. 

- A transaction is  a way for an application to group several reads and writes executed into one logical unit.

- Conceptually all reads and writes operation in a transaction are executed as one operation , either the entire transaction success (commit) or it fails (abort, rollback).

- If it fails application can safely retry,  with txns error handling becomes much simpler for an application because it doesn't worry about partial failure (some operation succeed and some dont).

- By using transactions the application is free to ignore certain potential error scenarios and concurrency issues because the database takes care of them (safety guarantees).
