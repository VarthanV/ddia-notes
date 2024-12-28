# Event Sourcing

- Event sourcing involves storing all changes to application state as log of change events.

- The application logic is explicitly built on basis of immutable events that are written to an event log . In this case the event store is append only and updates and deletes are discouraged/ prohibited. 

- Events are designed to check what happened in the application level rather than low-level state changes.

- It is a great design pattern to record the users actions as immutable events rather than recording those on a mutable database.

- Event sourcing helps to evolve applications over time , helps with debugging by making it easier to debug and providing inituiton on why something happened and guards against application bugs.

## Deriving current state from the event log

- Application using event-sourcing must take log of events and transform it into application state that is suitable for showing it to  user (the way in which data is read from the system). 

- This transformation can use arbitary logic , but it should be determinstic so that we can run it and derive the same application state from the event log

- Log compaction is not possible in event logs mechanism since we need the whole set of logs to make sense on the final state.

- Event sourcing typically have some mechanism for storing snapshot of current state that is derived from log of events so they dont need to repeatedly process the full log.

## Commands and events

- When a request arrives initially from a user it is command , at this point it still may fail because of some integrity condition is violated

- If any integrity condition is violated the app must first validate it and execute the command.If the validation is succesful and command is accepted it becomes an event which is durable and immutable.

- When event is generate it becames an **fact**.

- A consumer of event store is not allowed to reject any event,by the time consumer sees an event it is part of the immutable log and it may have been seen by other consumers. Thus any validation must happen synchornously before it became an event.

