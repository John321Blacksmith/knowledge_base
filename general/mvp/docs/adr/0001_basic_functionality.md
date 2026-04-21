# Basic functionality of the logging agent

## 📌 Date and identifier
* ADR-0001
* Created at: 2026-04-20

## Status
Accepted | **Proposed** | Deprecated

## Context
Based on the research over different alternatives,
a main picture was drawn.

## The essence of the app
#### Verbose
1. `Exporter` *sends* **logs** to `Collector`                         [data migration]

2. `Collector` *gathers* the **logs**                                 [data migration]

3. `Collector` *structures* the **logs**                              [data modification]

4. `Collector` *sends* the **structured logs** to `Analyzer`          [data migration]

5. `Classifier` *performs* cleansing of the **structured logs**       [data modification]

6. `Classifier` *evaluates* the **analyzable data** to **results**    [data modification]

7. `Classifier` *formats* the **results** to **reports**              [data modification]

8. `Classifier` *associates* the **reports** with the services        [data modification]

9. `Classifier` *stores* the **results** in the database              [data migration]

#### Basic Descriptive Layers
1) Application ----- Observer
2) Application ----- Observer[Exporter ----- LoggingService]
3) Application ----- Exporter ----- LoggingService[Collector ----- Analyzer ----- Presenter]
4) Application ----- Exporter ----- Collector ----- Analyzer ----- Presenter[Repo ----- Server ----- API Interface]
5) Application ----- Exporter ----- Collector ----- Analyzer ----- Repo ----- Server ----- API Interface ----- Client Dashboard

#### 