# Basic functionality of the logging agent

## 📌 Date and identifier
* ADR-0001
* Created at: 2026-04-20

## Status
Accepted | **Proposed** | Deprecated

## Context
Based on the research over different alternatives,
a main picture was drawn.


#### Basic Descriptive Layers
1) Application ----- ObservingSystem
2) Application ----- ObservingSystem[Exporter --- Aggregation]
3) Application ----- Exporter ----- Aggregation[Collector --- Refinery --- AnalysisEngine --- DataRecording --- Presenter]
4) Application ----- Exporter ----- Collector ----- Refinery[Cleanser --- Transformer] ----- AnalysisEngine ----- DataRecording[StorageManager --- Repository] ----- Presenter
5) Application ----- Exporter ----- Collector ----- Cleanser ----- Transformer ----- AnalysisEngine ----- StorageManager ----- Repository ----- Presenter


## The essence of the app
#### Non Verbose
1. `ObservingSystem` *receives* the **forwarded logs** from `Application`
2. `ObservingSystem` *aggregates* the **logs**
3. `ObservingSystem` *presents* the **results** to `Client`

#### Verbose

1. A service from the `Application` *emits* the **log**

2. The **log** is *exported* to the MQ by a dedicated `Exporter`

3. `Collector` *gathers* and *forwards* the **exported logs** to the `Cleanser`

4. `Cleanser` *removes* noice and inconsistency from **forwarded logs** and *sends* to the `Transformer`

5. `Transformer` *formats* the **clean logs** to **analyzable format** and *sends* to the `AnalysisEngine`

6. `AnalysisEngine` *evaluates* the **analyzable logs** and *makes* **reports**

7. `AnalysisEngine` *sends* the **reports** to the `StorageManager`

8. `StorageManager` *stores* the **reports** in a persistent database

9. The **saved records** are *presented* by the `Presenter` to an external client

## Usecases
Here are the basic user stories
1) User queries a list of all reports within a specified time;
2) User queries a list of reports about a particular service;
3) User queries a list of all services with critical reports;
