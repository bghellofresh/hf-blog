---
layout: post
title:  "Reading List - SLO Workshop 1"
date:   2018-11-12 12:10:00 +0100
categories:
---
Source: [https://drive.google.com/file/d/0B6YMsY__E8UpMDdvbzZtVHh6Vkk4S3JXSlRIRW02bFl6SndJ/view](https://drive.google.com/file/d/0B6YMsY__E8UpMDdvbzZtVHh6Vkk4S3JXSlRIRW02bFl6SndJ/view)

### How SLOs Help
- product perspective (what prio does reliability have)
- dev perspective (balance risk and reliability)
- ops perspective (determine level of reliability)

### The SLI Equation

![sli-equation](https://i.imgur.com/E3vKD0f.png)

- All SLIs can be expressed with this formula, which provides a consistent format for defining SLIs as falling between 0 and 100%
- consistent SLI format allows for tooling to be built for alerting, monitoring, error budget calculation
- an SLI is a formal statement of your users' expectations about *one* dimension of reliability for your service

### Availability/Reliability Chart
A helpful table for availability/reliability by 9s

![outrage-maths](https://i.imgur.com/m9HcZCf.png)

### SLI Specs

#### Availability SLI
- proportion of valid requests served successfully
- useful metrics: http status code (relies on proper use of status codes by application)
- proportion of time a system is running / reachable via SSH

#### Latency SLI
- proportion of *valid* requests served *faster* than a *threshold*
- two questions to be answered: what requests are valid and what threshold is fast enough?
- batch processing pipelines can be tracked via completions per time period (order creation for example)

#### Quality SLI
- if the system can trade lower CPU / Memory utilization for a lower quality response this can be tracked
- the proportion of *valid* requests serviced without *degrading quality*
- easier to express in terms of bad events as opposed to good events

#### Freshness SLI
- proportion of *valid* data updated *more recently* than a *threshold*
- could be measured as the time elapsed since the last successful run
- could also use a watermark to track the most recently saved record
- this can in turn be used in measuring responose quality. If the last saved record's age exceeds a threshold upon requesting data the response could be considered stale

#### Coverage SLI
- similar to availability SLI
- useful when users have expectations that data will be processed and the outputs made available to them
- proportion of *valid* data processed *successfully*
- to define the SLI the relevant data needs to be defined, as well as whether the processing of the data was *successful*
- the challenge is to find skipped data sets and record them as failed (usually requires determining the number of records outside of the data processing system itself, ie. `COUNT(*)` on data source)

#### Correctness SLI
- The proportion of *valid* data producing *correct output*
- Challenge: which of the data processed are *valid*?
- Challenge: how to determine *correctness*
- method of determining correctness must be independent of those used to generate the output data
- Strategy: have "golden" input data producing *correct* outputs when processed
