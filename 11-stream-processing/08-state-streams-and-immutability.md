# State, Streams and Immutability

- The key idea is mutable state and append only log of immutability events do not contradict each other.

- The log of all the changes **changelog** represents the evolution of state over time.

## Deriving several views from the same event log

- By seperating mutable log from immutable event log we can derive several read oriented representations from the same log of events.

- Having explicit translation step from an event log to database makes it easier to evolve application over time , if we want to introduce a new feature that presents existing data in some new way can use event log to build a seperate read optimised view for new feature and run in alongside the existing systems without having to modify them.

- Running old and new systems side by side is often easier than performing a complicated schema migration in an existing system. 

## Uses of Stream Processing

- It can be used form monitoring purposed where org wants to get alerted when certain things happen
    - Fraud detection system needs to determine if usage pattern of credit card has unexpectedly changed and block the card if it was likely to be stolen.

    - Trading system needs to examine the price changes in a financial market and execute trades according to specified rules.

    - Manufacturing systems need to monitor the status of machines in afacotry and quickly identify problem before malfunction.

    - Military system for any anomalies


## Complex Event Processing

- Complex Event Processing is an approach to analyze event streams especially geared towards application tha requires searching for certain event patterns. 

- CEP allows us to search for certain patterns in an event similar to regex.

## Stream Analytics

- Analytics is more oriented towards aggregation and statistic metrics over a large number of events than event sequences
    - Measuring the rate of some type of event
    
    - Calculating the rolling average of a value over some time period.

    - Comparing current statistics to previous time intervals.

- Eg: Knowing number avg number of queries per second to a service over the last 5minutes and P99 during their time.

- The time interval which we aggregate is known as **window**, 


## Maintaining Materliazed Views

- Deriving an alternative view onto some dataset so that we can query efficiently and updating the view whenver underlying data changes.


