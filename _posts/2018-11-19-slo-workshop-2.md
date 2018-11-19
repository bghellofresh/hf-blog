---
layout: post
title:  "Reading List - SLO Workshop 2"
date:   2018-11-19 11:10:00 +0100
categories:
---

### Measuring SLIs

5 Ways to measure SLIs
1. Server-Side Logging
2. Application Server Metrics
3. Frontend Infra Metrics
4. Synthetic Clients or Data
5. Client Instrumentation

#### Server-Side Logging

**Pros**
- Can backfill SLI Metrics via logs
- SLI implementation can be turned into simple "good events" and "bad events" counters

**Cons**
- Missing logs for requests that did not reach server
- Processing latency makes SLI unsuitable for triggering operational response

#### Application Server Metrics
**Pros**
- fast and cheap to add new metrics
**Cons**
- servers cant see requests that do not reach them
- stateless application servers make it difficult to measure overall user journeys

#### Frontend Infra Metrics

**Pros**
- probably already implemented (low engineering effort)
- closest to user

**Cons**
- not viable for data processing for any SLI
- only approximate

#### Synthetic Clients or Data

**Pros**
- request comes from outside of infrastructure, therefore captures more of overall request path
- can measure all steps of complex user journey

**Cons**
- covering corner cases is hard
- high reliability targets must be probed very frequently

#### Client Instrumentation

**Pros**
- most accurate measure of user experience
- quantifies reliability of 3rd party services (CDN, payments providers, etc)

**Cons**
- processing latency makes it difficult to trigger operational response
- measurements contain factors out of SLI scope


### Developing SLOs and SLIs

For each *critical user journey*, ranked by *business impact*

1. choose an sli spec
2. sli spec -> implementation
3. look for coverage gaps in user journey
4. set SLOs based on past performance or business needs

#### An example SLO Worksheet
![slo-worksheet](https://i.imgur.com/uG7izMh.png)