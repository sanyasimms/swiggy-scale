# REDESIGNED MULTI-TIER ARCHITECTURE

## 1. Current Architecture

10M Users

↓

Single Node.js Server

↓

Single PostgreSQL Database

Weaknesses:

* Single point of failure
* No cache
* No load balancing
* Payment blocks DB
* Static assets overload API

---

## 2. Redesigned Architecture

Users

↓

CloudFront CDN

↓

Application Load Balancer

↓

Node.js Instances (4–20)

↓

Redis Cluster

↓

PgBouncer

↓

PostgreSQL Primary

↓

Read Replicas

↓

SQS Queue

↓

Payment Worker

---

## 3. Component Justification

| Component      | Failure Prevented       | How                       |
| -------------- | ----------------------- | ------------------------- |
| CloudFront     | Static asset saturation | Images served from edge   |
| ALB            | Single server failure   | Health checks and routing |
| Node Cluster   | Event loop saturation   | Horizontal scaling        |
| Redis          | DB exhaustion           | Cache responses           |
| PgBouncer      | Connection exhaustion   | Reuse DB connections      |
| Read Replicas  | Read contention         | Separate reads            |
| SQS            | Payment blocking        | Async processing          |
| Worker Service | Payment bottleneck      | Background execution      |

---

## Architecture Flow

User Request

↓

CDN Cache

↓

ALB

↓

Node

↓

Redis

↓

Postgres

↓

Queue

↓

Payment

↓

Response
