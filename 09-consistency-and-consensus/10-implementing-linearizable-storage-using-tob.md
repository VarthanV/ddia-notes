# Implementing Linearizable storage using total order broadcast

- Total order broadcast is asynchornous; messages are guaranteed to be delivered reliably in fixed order, but no guarantee about when a message will be delivered

- In case of the uniq username problem we can assume that each username has a linearizable register with atomic compare and set operation.

- Every register initially has the value null indicating the username is not taken. 

- When user wants to take a username we execute a compare and set op on the register for that username, setting it to user account ID , under the cond previous register value is nul..

- If multiple user tries to grab the username concurrently one of compare and set op succeed because the other will see value other than null (due to linearizability).

- We can implement such compare and set op as follows
    - Append a message to the log , tenatively indicating the username to be claimed.

    - Read the log and wait for the message appended to be delivered back.

    - Check for any message claiming the username we want . if the first message is the own message then we are succesful. we can commit the username claim (appending another message to log) and acknowledge it to client if the first message is from another user, the OP is aborted.

- Because the log entries are delivered to all nodes in same order , if there are concurrent writes all nodes will agree on which one is came first. 

- It guarantees linearziable writes , but not read , if we read from store that is async updated from the log , it may be stale.

- To make reads linearizable here are few options
    - Sequence reads through the log by appending a message, reading the log 
    and performing the actual read when message is delivered back. The messages position the log thus defines the point in time which the read happens.

    - If the log allows to fetch the position of the latest log message in linearizable way can query the position wait for all entries up to that position deliver and perform the read.

    - Read from replica which updated on writes 

