# Basic functionality of the app observer

## 📌 Date and identifier
* ADR-0001
* Created at: 2026-04-30

## Status
Accepted | **Proposed** | Deprecated

## Context
Based on the research over different alternatives,
a main picture was drawn.


## The essence of the app

1. `ObservingSystem` *receives* the **forwarded logs** from `Application`
2. `ObservingSystem` *aggregates* the **logs**
3. `ObservingSystem` *presents* the **results** to `Client`
