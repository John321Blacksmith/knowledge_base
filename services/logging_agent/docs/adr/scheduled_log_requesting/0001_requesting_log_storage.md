# Requesting of the logs from the log storage

## 📌 Date and identifier
* ADR-0001
* Created at: 2026-01-30

## Status
Accepted | **Proposed** | Deprecated

## Context
Within the specified time window, **logging agent** requests a list of logs from the logs storage.
The storage contains existing logs saved by the logging service. Now, this storage is Firebird DB.
The problem is how to send a request to the data source safely and not to overload their database.

## Considered options

### Option 1 - Direct access to the logs storage
* ✅ Pros
- Flexible querying, so the consumer can send requests with custom DML and get whatever required.
- No agents needed to facilitate data delivery from storage to consumer.
* ❌ Cons
- Direct access to the database can lead to overload. The more connections, the more machine resourses
  are taken, so the system may be exhausted. In terms of big data, it can lead to disastrous consiquences.
- If, for some reason, the database has crushed on the side of the logging service, the
  dependant consuming mechanism will not know where to fetch fresh data from,
  so the external client won't have seen the relevant analysis reports.

### Option 2 - Read the logs from the message queue
It's known, their logging service has its messaging stream powered by the NATS server.
The publishing services push their logs as messages into the stream, on topics, based on the service name.
Then, their logging service consumes the messages and saves ones to the log storage.
The consumer of the logging agent may do the same: it can fetch data from the NATS stream directly and group the messages by
the message topics referred as service names, having subscribed to topics.
* ✅ Pros
- Consumer fetches the freshiest data, almost from the publishing services.
- There is no need to send multiple requests to fetch the logs of a particular service,
  since the logs live as messages on different topics, according to the service name.
- The service name is always available, since each message in the stream has it's topic name.
* ❌ Cons
- Consumer will have to do part of the logging service work itself.
- The NATS stream doesn't guarantee persistence of data.

### Option 3 - Let the agent-helper send logs to the consumer
On the side of the logging service, implement a scheduled agent which will send the logs to the logging agent
* ✅ Pros
- Offload log fetching job from the logging agent consumer to the helper-agent(log sender) which itself sends logs to the consumer.
* ❌  Cons
- Additional engineering.
- There should be an agreement between an owner of logging service and owner of the logging agent
  to have a helper-agent on the side of the logging service.
- Despite of ability of a helper-agent to send logs to the logger agent consumer, there should be some kind of
  messaging layer, from which the consumer will pick the messages up for further processing. So it may add more
  dependencies, more engineering.

### Option 4 - Use API of the logging service
Their **logging service** has already an API by which the client can fetch
a paginated list of logs within a specified time window.
* ✅ Pros
- No need to either access persistent log storage or a messaging stream. Just use their optimized API.
- Access to log storage is controlled by the backend of the logging service.
- The API andpoint already has parameters of time and pagination.
- Even if the NATS server may be replaced by another solution in the future, the API is always present.
* ❌  Cons
- The client can only fetch the logs with a limited set of fields.
- Currently, the logs which API provides, do not have a field of the service name. Instead, there's just service ID,
  so the grouping log entites by services process will take more steps.
  
## 💡 Decision
Based on the analysis, the option 4 was taken.
### Reasons
- The most straightforward implementation.
- Reliability of data, serialized and presented by the **logging service**.
- Several queries for corresponding services are harmless to their DB.
- Opportunity to improve the consumer of the **logging agent**
  if one of the other options has been reconsidered later.

## ⚠️ Consequences
- The consumer will be adopted for sending requests to the **logging service**.
- At specified time window, the consumer will iterate over the list of service
  IDs and send requests to get the corresponding logs.
- Since there there may have been different mapping of services and their IDs on
  two databases, log storage and reports, the **logging agent** will have a map
  of services and their IDs, synchronized with database of **logging service**.