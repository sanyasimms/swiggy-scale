# INCIDENT RUNBOOK

## STEP 1 — DETECT

### Alerts

* ALB 5xx > 5%
* DB Connections > 80%
* CPU > 80%
* Redis Memory > 75%
* Queue > 10,000
* P99 > 2 seconds

---

## STEP 2 — TRIAGE

Check in order:

1. Database Connections
   → If red → DB issue

2. CPU Utilization
   → If red → compute issue

3. Cache Misses
   → If red → Redis issue

4. Queue Depth
   → If red → payment issue

---

## STEP 3 — RESPOND

### DB Exhaustion

Scale DB

Restart pool

### Compute Saturation

Scale instances

### Queue Backup

Restart workers

### Cache Failure

Warm cache

---

## STEP 4 — ROLLBACK

Conditions:

* 5xx > 20%
* Issue persists > 5 mins

Command:

aws ecs update-service

Never rollback DB schema.

---

## STEP 5 — POSTMORTEM

Timeline

Root Cause

Impact

Recovery

Action Items
