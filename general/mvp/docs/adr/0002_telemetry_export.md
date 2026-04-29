# Basic functionality of the logging agent

## 📌 Date and identifier
* ADR-0002
* Created at: 2026-04-29

## Status
Accepted | **Proposed** | Deprecated

## Context
Here is an explanation on how the telemetry export is done

## Quick note
Given a particular service from the distributed system,
the logs and traces in this service are emitted, they're
transported to the MQ and taken by a Collector.

## Tech choices
* Telemetry processing and transport - **Opentelemetry**
* Programming language - Any

## Other notes