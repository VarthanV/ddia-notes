# Faults and Partial failures

- When writing a program on a signle computer , it behaves in a fairly predictable way either 
it works or doesn't

- The same operation always produces same result (deterministic). If there is a hardware problem the consequence is usally a total system failure. A individual computer with good software is either fully
functional or entirely broken but not in between.

- If an internal fault occurs we prefer a computer to crash completely rather than returning a wrong result. Because wrong results are difficult and confusing to deal with.

- When we are writing software that runs on several computers connected by a network the situation is different. In distributed systems we are no longer operation in a idealized system model. 

- In distributed system there may be some parts of system that are broken in some unpredictable way even though other parts of the system are working fine. This is known as **partial failure**.

- The partial failures are **non-deterministic** if we try to do something that involves multiple node and network. it may sometimes work and sometimes unpredictably fail.

- We may not even know whether something succeeded or not as it takes time for a message to travel across network also is nondeterministic.

