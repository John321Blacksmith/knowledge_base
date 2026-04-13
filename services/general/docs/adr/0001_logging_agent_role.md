# Log classification work is described here

## Status
Accepted | **Proposed** | Deprecated

## Context
Here I need to clarify what a logging agnt is and
kind of problems the log classification service will solve.

## Decision
In terms of distributed services, there may've been lots of
such checks, so the fellow admin dies from exhaustion.
Why does the admin care about the logs?
Well, to see the importance of logs, let's conjure up
an example:
The therapist diagnoses his patients by tracking their state.
State of the patient is defined by a sequence of events
that take place in his body when he performs some action.
Such events represent the person's narrative description,
his feelings, an approximate time the action was done at
and a type of action the person was doing at that time.
The events may be either positive or negative, for
example, the knee pain when jumping up in the morning
etc ...
A human has lots of internal systems, such as cardio, nerve, digestion,
respiratory, muscle, mental, and every one has it's own state as well.
In order to make a conclusion about an overall person's healthstate,
the therapist has to inspect his patient's past
experience and collect that information somewhere so, it's
been processed and analyzed by him, based on his expertice,
and the analyzis result has then been assosiated with that
patient. The patient passes the cardio or blood tests, or he
may go to a medical expert, specifically oriented in some human system.
The patient is known to have some issiues or he is
healthy. After some research, the therapist sees, the person
may be prone to some chronic diseases or to have some bad potential issues.
So, if he sees a potential danger, as a result of analyzis, he makes
some steps to tackle that issue. 


When several services take part in processing
user's request, each of them has its own history
of work over it. All the processes happen during
service work are recorded as events: `logs`. The
logs contain all useful information that says
about state of the process, information about
user request, event origin, a custom message
where the nature of event is described by the dev
and a log severity that indicates type of event.
Generally, based on the OLTP standard, the log object
with its meta and body looks like:

```json
{
    "eventTimestamp": "time when the event occurred",
    "eventName": "identifies a type of the event",
    "observedTimestamp": "time when the event is observed",
    "severityText": "name of the severity",
    "severityNumber": "numerical representation of the severity",
    "body": {
        "message": "a custom message of the log the developer provides",
        "serviceName": "a name of the service where the log is instantiated",
        "serviceIP": "an IP of the service where the log is instantiated",
    },
    "traceId": "the ID of the user request that goes through an entire service",
    "spanId": "the ID of a particular UOW through which the request goes",
    "resource": "an origin where the log is instantiated"
}
```

As known, the service stores all the logs locally
and in order to see the ones, the local log storage
has to be checked by hands, so the sytem administrator
connects to the host of one of the services and checks the logs.



* ✅ 


## Consequences
Good, bad, and neutral outcomes of this choice.
