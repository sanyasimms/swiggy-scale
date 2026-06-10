# AWS COST ESTIMATION

## Baseline Cost (Normal Traffic)

### EC2

t3.medium × 4

$0.0416 × 4 × 720

= $119.81/month

### PostgreSQL Primary

db.r6g.large

$0.182 × 720

= $131.04/month

### Read Replicas

2 × db.r6g.large

= $262.08/month

### Redis

cache.r6g.large × 3

= $358.56/month

### Application Load Balancer

≈ $56/month

### CloudFront

10TB transfer

≈ $85/month

### SQS

1M/day

≈ $12/month

---

## Total Baseline

≈ $1024/month

---

## Peak Event Scaling

Extra EC2:

≈ $27

Temporary DB Upgrade:

≈ $4

CloudFront Surge:

≈ $425

---

## Peak Event Total

≈ $455

---

## Business Justification

Revenue loss:

₹4.2 crore/minute

45 minute outage:

₹189 crore

Infrastructure cost is significantly lower than outage losses, making scaling economically justified.
