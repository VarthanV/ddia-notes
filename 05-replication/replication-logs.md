# Implementation of replication logs

## Statement based replication log

- In the simplest case , the leader logs every write statement it executes and sends the statement log to its followers.

- In relational DB this means every INSERT, UPDATE or DELETE statement is forwarded to the followers.

- Each follower parses and executes the SQL statement as if it had been received from a client.

- But there are several ways this might go wrong

- Any statement that calls a non-deterministic function like ``RAND()``, ``NOW()`` is likely to generate a different value on each replica.

- If stmts use autoincrementing column or they depend on existing data in the DB they must be executed in same order on each replica or else they have different effect.

- Statements can have side effects (triggers,stored-procedures,user-defined) fns these may have different side effects on each replica unless they are determinsitc.

## Write ahead Log (WAL) shipping

- Log is append only sequence of bytes containing all writes to database , we can use the same log to build a replica on another node.

- Beside writing the log to disk , the leader can also send it across network to its followers.

- When follower processes the log it builds a copy of the exact same data-structure found on the leader.  This method of replication is used in PostgreSQL and Oracle 

## Disadvantage

- The log describes the data on very low level like which bytes changed in which disk blocks.

- This makes replication very closely coupled to storage engine. For example DB engine 1 has page size of 4KB where as DB engine 2 has page size of 8KB.

- If the db changes it storage format from one version to another it is not possible to run all the version of software on leaders and followers.

- Usually a down time is required to update the software.

## Logical (row-based) log replication

- It is wise to use different formats for replication and storage engine.

- This allows replication log to be decoupled from the storage engine. 

- This log is called **logical log**

- A logical log is usually a sequence of records describing the writes to a database table at the granularity of a row.

## What does log contain? 

- For an inserted row , the log contains the new value of all columns

- For an deleted row , the log contains unique value of the row that is deleted usually it is a primary key , if no primary key is there the old values of the columns need to be logged.

- For an updated row , the log contain enough information to uniquely identify the update row and the new values of all columns that has changed.


- A txn that modifies several rows generates several much logs followed by a record indicating the xn was commited. 

- Since the log is decoupled from the storage engine internals , it can be easily kept backwards compatible ,allowing the leader and follower to run different version or db storage engine.

- A logical format is also easier for external applications to parse.

- This is useful when we want to send the content of database to a external system such as wareshouse for offline analysis or for building custom indexes and caches , this technique is called **change data capture**