# Enterprice trades-off are described here

## Status
Accepted | **Proposed** | Deprecated

## Context
There are a variety of ready observability platforms in the world.
The tools support aggregation, monitoring, analyzis
and visualization functionality. Technically, we can buy some of them
but as some issues happen or we'd like to add our own
functionality which may not be provided by the bought
tool, we'll loose flexibility and have to seek for
another solution.

## Decision
Based on such outcomes, I decided to implement a flexible
tool which, generally, will do the same work as the commercial
tools do, but with the ability to be extended and improved as
we like. But there are already some well developed platforms


## Considered options
### Option 1 - Use the official observability platforms
- [Datadog](https://www.datadoghq.com/)
- [Splunk](https://embargo.splunk.com/)
- [Grafana Cloud](https://grafana.com/products/cloud/)
- [Dynatrace](https://www.dynatrace.com/)

##### ✅ Pros
- Minimal time for integration;
- Efficiency of such tools have been proven by hundreds of enterprice corporations;
- The tools have been covered by huge documentation and tutorials;
- There are many communities and product-oriented support worldwide;
- Stable development and big expertice;
- Some of the platforms support AI-based work;
- Telemetry is processed according to the [OTLP protocol](https://opentelemetry.io/docs/specs/otlp/');
- The platforms, such as [Datadog](https://www.datadoghq.com/) enable great data visualization;

##### ❌ Cons
- The tools are not free;
- Some tools may not go along the way our enterprice requiremets;
- As they're already shipped complete, they cannot be cusomized;


### Option 2 - Implement a custom solution
##### ✅ Pros
- The agent will be flexible, so other intregrations are possible;
- It can be configured directlty for a particular enterprice;
- The agent will use the OTLP protocol as well;
- From human perspectives, obvious personal growth by creating the analogy to the top
platforms;

##### ❌ Cons
- Lack of expertice in this field, and, as a result, huge amount of time taken for implementation;
- Difficulties with tech stack choice;
- There may be a lot of potential service work issues in the future;
- The community is not large;
- It will take some time to cover the app by documentation;
- As the solution enters the world, it'll still have zero reputation;