---
layout: post
title:  "Reading List Part 1 - SLO Chapter Google"
date:   2018-11-12 10:53:49 +0100
categories:
---

## SLO at HelloFresh

And the reading begins with google's definition of SLO (Service Level Objectives) [^1].

- define and deliver a level of service to users

### Indicators
- SLO = Service Level Objective
- SLI = Service Level Indicator
- SLA = Service Level Agreement
- SLI, SLA, SLO all inform which metrics are important to track for a given application.
- request latency, error rate (as a percentage of all requests), and system throughput (requests per second) are usually key SLIs
- availability (fraction of time service is usable), usually defined as successful request percentage, ie. yield.
- durability (likelihood of persistence - important for data storage systems)

**Availability** is usually expressed as decimal points after 99% in terms of "nines", ie. 99.99% is "2 nines".


### Objectives
- target value or range of values measured by an SLI (eg. `SLI < target` or `lower bound < SLI < upper bound`)
- speed matters, ie low latency is good. but it is difficult to set a hard threshold for acceptible speed.
- publishing SLOs to users set expectations about service performance.
- helps ground a discussion around complaints like "the service is slow" with data

### Agreements
- a contract with users that includes consequences of meeting/not meeting SLOs
- closely tied to business so defined consquences are often financial
- SREs (site reliability engineers) are usually not involved in defining SLAs
- to avoid disagreements, there has to be an objective way of measuring SLOs in an SLA

### Indicators in Practice
- How can you define appropriate metrics for a given service?
- don't choose too many metrics

**Categories**
- *User-facing serving system* - availability, latency, throughput
- *Storage Systems* - latency, availability, durability
- *Big Data* - throughput, end-to-end latency
- *ALL* - correctness/integrity (right answer returned, right data retrieved, correct analysis performed)

### Collecting Indicators
- prometheus
- borgmon
- log analysis
- frontend site-speed, first paint metrics

### Aggregation
- eg. requests, should this metric be collected every second or over a longer period of time?
- using an average for requests / time can obscure varied latency, a better approach is to use percentages as indicators, ie. what percentage of the requests were handled within defined req/sec thresholds? example: 70% of the time we handle 100 reqs/sec. the SLO in this case would then be that X percent of the time we handle y requests in a defined time period.

### Standardize Indicators
- recommended to standardize common definitions for SLIs through a template

**Examples**
- Aggregation intervals
- Aggregation regions
- Frequency of measurement
- What requests are included
- Acquisition method
- data access latency

### Objectives in Practice
- what do your users care about?
- work from objectives backwards to indicators

### Defining Objectives
- SLOs should define how they are measured, and the conditions under which they are valid
- it is unrealistic to expect SLOs to be met 100% of the time, an error budget should be allowed


### Choosing Targets
- dont base decisions on current performance
- keep it simple
- be flexible
- have as few SLOs as possible (if you can't win an argument on the basis of an SLO, it's not worth having)
- start with a loose target and gradually tighten it as more data is collected

### Control Measures
- SLIs should be measured and monitored
- Compare SLIs to SLOs to decide what, if any, action is necessary
- Keep realistic expectations by having a safety margin (tighter internal SLO as external), not exceeding SLOs (planned outages, throttline requests)


**Note** People often confuse SLA with SLO. If they speak about an SLA violation they are usually talking about an SLO


### Questions:
- What is a service, and what is its level?
- How do we agree on indicators with business folks?
- Didn't understand this line. Typo?
```
An easy way to tell the difference between an SLO and an SLA is to ask "what happens if the SLOs aren’t met?": if there is no explicit consequence, then you are almost certainly looking at an SLO.16"
```
- 

[^1]: [https://landing.google.com/sre/sre-book/chapters/service-level-objectives/](https://landing.google.com/sre/sre-book/chapters/service-level-objectives/)
