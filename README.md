# Swiggy Scale Simulation & Incident Architecture

## Project Overview

This project analyses how a Swiggy-like food delivery platform behaves during an extreme traffic event and redesigns the architecture to survive the load.

Scenario:

* India vs Pakistan World Cup Final
* 50% promo campaign
* 180M notifications
* ~10M users opening simultaneously
* Single Node.js server
* Single PostgreSQL database

---

## Repository Documents

| Document           | Purpose                             |
| ------------------ | ----------------------------------- |
| FAILURE-CASCADE.md | Traffic simulation and outage chain |
| ARCHITECTURE.md    | Redesigned scalable architecture    |
| COST-ESTIMATE.md   | AWS infrastructure cost             |
| RUNBOOK.md         | Incident handling guide             |

---

## Key Findings

* Database pool exhausts at ~394 RPS
* Node.js saturates around 12K RPS
* CDN removes static asset bottleneck
* Async payment flow reduces DB lock time
* Redis dramatically lowers DB load

---

## Architecture Summary

The redesign introduces:

* CloudFront CDN
* Application Load Balancer
* Node.js horizontal scaling
* Redis caching
* PgBouncer
* PostgreSQL read replicas
* SQS payment queue

---

## Technologies

* Node.js
* PostgreSQL
* Redis
* AWS
* CloudFront
* SQS
* PgBouncer

---

## Outcome

The redesigned architecture costs significantly less than the projected outage losses and provides reliability during traffic spikes.
