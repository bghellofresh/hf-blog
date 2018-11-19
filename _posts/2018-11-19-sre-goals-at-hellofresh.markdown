---
layout: post
title: "Implementing Site Reliability Engineering at HelloFresh"
date: 2018-11-19 09:31:49 +0100
categories:
---

**Source**: Slack post from Squad Lead

This is the plan to what we need to do, to start doing Site Reliability Engineering at HelloFresh


*Implementing Service Level Objectives (SLOs)*

Service level objectives (SLOs) specify a target level for the reliability of a service.

Because SLOs are key to making data-driven decisions about reliability, they’re at the core of SRE practices, in many ways, this is the most important SRE concept.

SLOs are a tool to help determine what engineering work to prioritize, let's take API-v2 as a example, it will drive decisions in regards to what needs to be made more reliable (increasing cost and slowing development) or less reliable (allowing greater velocity of development).

API-V2 will requires agreement from the Product Managers, Product Developers, Team Responsible, CTO and even the CEO, they will commit to a availability target for the service.

That being said, let's not set availability targets if we don’t intend to commit to it to being that reliable, let's iterate on this until we get the target in which fits our reality.

*More Monitoring*

- Define availability targets for infrastructure core components such as:
   - Kubernetes
   - RabbitMQ
   - Janus
   - Entry
   - Monoliths Databases

- Define availability targets for HelloFresh overall services:
   - Core Services
   - CRM Services
   - Monoliths (API-V2)
   - etc...

*Prometheus Retention Period*

The current Prometheus retention period is 10 days. We need to scale our prometheus to at least a month so we can start applying Error Budgets policies.

It's a bit challenging given we are waiting for an upstream feature to be merged to leverage a higher retention period from Prometheus

We have opened a issue to prometheus-operator repo https://github.com/coreos/prometheus-operator/issues/1965

*Establishing an Error Budget Policy*

Once we have an SLO, we can use it to derive an error budget. In order to use this error budget, we need a policy outlining what to do when a service runs out of budget.

`TBD`

*Alerting on SLOs*

1. Target Error Rate ≥ SLO Threshold
2. Increased Alert Window
3. Alert on Burn Rate
