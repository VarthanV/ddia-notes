# Introduction

## Services (Online systems)

- A service waits for a request or instruction from a client to arrive.

- When one is received the service tires to handle it quickly as possible and send a resposne.

- Response time is usually the primary measure of performance for a service and availability is often important.


## Batch processing systems (Offline systems)

- A batch processing system takes a large amount of input data runs a job to process it and produces some output data .

- Jobs often take a while so normally user doesn't wait for a job to finish.

- Instead batch jobs are often scheduled to run periodically.

- The primary performance of a batch job is usually **throughput** (time it takes to crunch through an input dataset of certain size).


## Stream Processing Systems

- Stream processing is somewhere between online and offline/batch processing is sometime called near-realtime or realtime processing.

- Like batch processing system a stream processor consumes inputs and produces outputs.

- However a stream job operates on events shortly after they happen whereas batch job operates on fixed set of input data. 

