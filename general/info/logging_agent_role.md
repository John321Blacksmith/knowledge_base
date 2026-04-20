# Log classification role is described here

## Status
Accepted | **Proposed** | Deprecated

## Context
Here I need to clarify what kind of problems the log classification service will solve.
Our distributed system has lots of services to be inspected for some issues. Every service
produce logs and they are published to the stream. Then these logs are consumed by the log
collector and stored in a dedicated database. As the logs are gathered from different services
in a centralized place, they're still uncertain since they do not say which potential problems may
occur in a particular service or if one of the services is inclined to have some kind of issues.
Having a centralized database of well-refined logs is already useful for system administrators
but they still have to query data from the storage in order to analyze it by hands. The admins
need to do a log research and remember which service to what problem is related. They also
need to look several steps forward and predict a future behaviour of the systems. These steps
require some time and efforts.

## Decision
Instead of administrators, the logs may be queried by a log classification agent and then
analyzed automatically. The analyzed data is then stored in a dedicated database and presented
to the clients. The result data already contains analyzis result for each service.

## Problems the log agent solves

* ✅ **Time efficiency**: The logs are queried from storage, processed and analyzed automatically;
* ✅ **Persistent results**: Analyzis work is structured in the storage and available to clients;
* ✅ **More accurate predictions**: Big amounts of logs are analyzed by algorithms capable of learning;
* ✅ **More flexibility, less noise**: If a new service is added, no need to worry about its domain, just logs;