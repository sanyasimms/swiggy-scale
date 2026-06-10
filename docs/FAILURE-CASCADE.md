# FAILURE CASCADE ANALYSIS

## 1. Traffic Simulation Math

### Event Scenario

Total users receiving notification:

180,000,000

Estimated click-through rate:

8%

Users opening app:

180,000,000 × 0.08

= 14,400,000 users

Assume active spike:

10,000,000 users

Each user performs:

* GET /restaurants
* GET /restaurant/:id
* POST /orders

Total API calls:

10,000,000 × 3

= 30,000,000 calls

Peak RPS:

30,000,000 ÷ 60

= 500,000 RPS

---

## 2. Component Capacity Numbers

### PostgreSQL

max_connections = 100

### Node.js

Approx capacity:

12,000–15,000 RPS

### Payment

Average hold:

800ms

### DB Exhaustion Formula

Connections held:

(0.7 × RPS × 0.02)

*

(0.3 × RPS × 0.8)

Pool limit:

100

0.014R + 0.24R = 100

R ≈ 394

Pool exhausted at approximately 394 RPS.

---

## 3. Failure Cascade

### Failure 1 — PostgreSQL Pool Exhaustion

Severity:
CRITICAL

Trigger:
394 RPS

Impact:
New DB requests rejected.

Result:
Node queues requests.

---

### Failure 2 — Node Event Loop Saturation

Severity:
CRITICAL

Trigger:
12,000 RPS

Impact:
Timeouts and OOM.

---

### Failure 3 — Payment Amplification

Severity:
HIGH

Trigger:
Slow gateway response.

Impact:
Connections held too long.

---

### Failure 4 — Promo Race Condition

Severity:
HIGH

Trigger:
Concurrent promo validation.

Impact:
Oversold discounts.

---

### Failure 5 — Static Asset Saturation

Severity:
CRITICAL

Trigger:
Images served from Node.

Impact:
NIC overload.

---

## 4. Incident Timeline

T+0 Push sent

T+3 DB exhausted

T+5 Event loop backup

T+10 Payment timeout

T+15 Network saturation

T+18 Node crash

T+45 Root cause identified

T+2h System restored
