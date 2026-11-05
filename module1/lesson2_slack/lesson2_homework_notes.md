# SEIR Foundations — Module 1, Lesson 2
## Slack Monitoring Homework Notes

**Student:** T. Hasan Johnson  
**Date:** November 5, 2026  
**Assignment:** Seven Alerts, Seven Wins

### Homework 1 — Hello Slack

I personalized the Python script with my name and successfully sent an INFO notification to the `#balerica-alerts` Slack channel.

**Incident ID:** HW-001

**What I learned:** Python can send automated messages from an AWS EC2 instance to Slack using a webhook.

### Homework 2 — Severity Tour

I tested four alert severity levels: INFO, WARNING, ERROR, and CRITICAL.

With the threshold set to INFO, all four alerts were delivered.

With the threshold set to ERROR, only ERROR and CRITICAL alerts were delivered.

**Question: Which severities arrived, and why?**

The severity threshold determines which notifications are delivered. Alerts below the configured threshold are filtered out, while alerts at or above it are delivered. This helps engineers prioritize important problems and avoid unnecessary notifications.

### Homework 3 — Server Time

**Incident ID:** HW-003

I used Python to retrieve the server's current UTC time and send it to Slack.

**Question: How many hours apart are server time and my local clock?**

My local time in California was eight hours behind UTC because California observes Pacific Standard Time (UTC−8) in November.

### Homework 4 — Disk Watch

**Incident ID:** HW-004

My initial disk usage was 25.7%, producing an INFO alert because it was below the 75% WARNING threshold.

**Question: Why is a quiet INFO alert good design rather than a failure?**

A healthy server should not constantly generate urgent warnings. INFO notifications document normal operation without overwhelming engineers. WARNING and ERROR notifications are reserved for conditions requiring greater attention.

### Homework 5 — CPU Load Check

**Incident ID:** HW-005

My actual results were:

- One-minute load: 0.00
- Five-minute load: 0.00
- Fifteen-minute load: 0.00
- Available CPUs: 2
- Severity: INFO

**Question: What would make the CPU load spike at Balerica Bank?**

Large numbers of simultaneous banking transactions, demanding database operations, inefficient programs, and heavy processing workloads could increase server load. Processes waiting for disk operations could also contribute to Linux load averages.

### Homework 6 — Incident Drill

I ran the simulated incident generator three times.

**Run 1:** DRILL-4504 — WARNING  
COBOL batch job BATCH-EOD running 12 minutes longer than usual.

**Run 2:** DRILL-5220 — ERROR  
FastAPI `/payments` endpoint responded 500 twice in one minute.

**Run 3:** DRILL-8995 — ERROR  
FastAPI `/payments` endpoint responded 500 twice in one minute.

All three incidents were confirmed in Slack.

**Question: Which incidents deserve to wake a human at 3 AM?**

A CRITICAL incident involving an unreachable ledger file deserves immediate attention because it could interrupt essential banking operations. Persistent payment-processing failures may also require overnight escalation depending on their severity and customer impact. A completed backup or a minor batch-processing delay would not ordinarily require waking an engineer.

### Homework 7 — Morning Report

**Incident ID:** HW-007

I generated a combined server monitoring report containing the current UTC time, hostname, operating system, Python version, disk usage, and CPU load.

My final verified report included:

- UTC time: November 5, 2026, 08:06:21
- Operating system: Linux x86_64
- Python version: 3.9.25
- Disk usage: 25.6%
- One-minute load average: 0.00
- Severity: INFO
- Delivery: Successful

The report was confirmed in Slack.

### Experiment 1 — CRITICAL-Only Alerts

**Prediction:** Only one of the four severity levels would be delivered.

I changed `SLACK_ALERT_SEVERITY` to `CRITICAL` and reran Homework 2.

**Actual results:**

- INFO: Skipped
- WARNING: Skipped
- ERROR: Skipped
- CRITICAL: Delivered

The prediction was correct. Only CRITICAL notifications passed the configured severity filter. I verified the alert in Slack.

### Experiment 2 — Slack Kill Switch

I changed `SLACK_ALERTS_ENABLED` to `false` and ran Homework 1.

The script reported that its notification was skipped. At the time, the severity threshold was also set to CRITICAL, so this run alone did not isolate the effect of the kill switch.

**Why is a kill switch useful?**

A kill switch allows engineers to temporarily suppress notifications during maintenance, testing, or troubleshooting without deleting monitoring code.

### Experiment 3 — Disk Warning Threshold

I temporarily changed the WARNING threshold in `hw4_disk_watch.py` from 75% to 20%, keeping the ERROR threshold at 90%.

**Actual disk usage:** 25.6%  
**Result:** WARNING delivered to Slack.

This demonstrated that changing monitoring thresholds changes how Python classifies server conditions.

Afterward, I restored the original WARNING threshold of 75% and verified that the ERROR threshold remained 90%.

### Final Configuration

I restored the Slack configuration to:

- `SLACK_ALERTS_ENABLED=true`
- `SLACK_ALERT_SEVERITY=INFO`

All seven homework scripts were executed, all three configuration experiments were performed, and the required monitoring evidence was collected.

### Evidence

Screenshots are stored in the `Screenshots` folder within `module1/lesson2_slack`, including the final Morning Report with the EC2 identification line and Slack alert screenshots.