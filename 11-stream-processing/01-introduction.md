# Introduction

- In general a stream refers to data that is incrementally made available ovwer time. 

## Transmitting event streams

- In context of stream processing a record is more commonly known  as **event** 

- Event is a small self contained immutable object containing the details of something that happened in some point in time . A event usually contains timestamp indicating when it happened according to time of day clock.
    Eg: A user viewed which page, measurement of temperature sensor

- A event may be encoded as text,string or JSON. 

- This encoding allows us to store an event by appending it to a file , inserting into a relational table or writing it to a document database. It also allows us to send the event over network to another node in order to process it.

- A event is generate once by a **producer** and then potentially processed by **consumers**.

- Related events are usually grouped together into a **topic or stream**.

- Constantly polling database for events is expensive , so specialized tech like messaging systems is used.



