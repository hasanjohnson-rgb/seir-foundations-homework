# SEIR Foundations — Module 1, Lesson 1: EC2

## Balerica Legacy Bank Lab

This lab demonstrates how to deploy a FastAPI application backed by a GnuCOBOL banking core on Amazon EC2, test COBOL return codes, decode a fixed-width account ledger, and generate simulated SWIFT payment traffic.

## AWS Configuration

- **Region:** US East (Ohio), `us-east-2`
- **Operating System:** Amazon Linux 2023
- **Instance Type:** `t3.micro`
- **Security Group:** `seir-lesson1-sg`
- **Application Port:** TCP 8000
- **Application Directory:** `/opt/balerica-bank`

## EC2 Deployment Log

| Run | Instance ID | Public IPv4 | Public DNS | Boot Time (UTC) | Screenshot Date (Pacific) | Evidence | Termination |
|---|---|---|---|---|---|---|---|
| 1 | `i-069654b4e4b12ff2a` | `13.184.105.199` | `ec2-13-184-105-199.us-east-2.compute.amazonaws.com` | 2026-10-29 05:55:56 | 2026-10-29 00:59 PDT | `Screenshots/lab1_run1.jpg` | Terminated — verified Oct 29, 2026 |
| 2 | Pending | Pending | Pending | Pending | Pending | `Screenshots/lab1_run2.jpg` | Pending |
| 3 | Pending | Pending | Pending | Pending | Pending | `Screenshots/lab1_run3.jpg` | Pending |
| 4 | Pending | Pending | Pending | Pending | Pending | `Screenshots/lab1_run4.jpg` | Pending |
| 5 | Pending | Pending | Pending | Pending | Pending | `Screenshots/lab1_run5.jpg` | Pending |
| 6 | Pending | Pending | Pending | Pending | Pending | `Screenshots/lab1_run6.jpg` | Pending |
| 7 | Pending | Pending | Pending | Pending | Pending | `Screenshots/lab1_run7.jpg` | Pending |

**Note:** Each run uses a new EC2 instance configured manually. The screenshot date and time must be verified against the actual screenshot and recorded in Pacific time.

## COBOL Return Code Tests

| Return Code | Test | Observed Result | Screenshot |
|---|---|---|---|
| 0 | Look up account `100001` | Successful lookup; Alice Johnson, balance $5,000.00 | `Screenshots/cobol_rc0.jpg` |
| 4 | Look up nonexistent account `999999` | Account not found | `Screenshots/cobol_rc4.jpg` |
| 8 | Attempt payment exceeding available funds | Rejected: insufficient funds | `Screenshots/cobol_rc8.jpg` |
| 12 | Run payment command without required arguments | Rejected: malformed request | `Screenshots/cobol_rc12.jpg` |

## Fixed-Width Ledger

The ledger file is located at `data/accounts.dat`.

| Character Positions | Field |
|---|---|
| 1–6 | Account number |
| 7–36 | Customer name |
| 37–44 | Account status |
| 45–56 | Balance in cents |
| 57–59 | Currency |

Alice Johnson's initial account balance was **$5,000.00**, represented as `000000500000` cents.

Evidence: `Screenshots/cobol_ledger_decode.jpg`

## SWIFT Traffic Verification — Run 1

The SWIFT traffic generator sent 10 simulated MT103 payment requests through the FastAPI application to the COBOL banking core.

| Metric | Result |
|---|---|
| Requests sent | 10 |
| Approved/posted | 6 |
| Rejected | 4 |
| Failed | 0 |
| Average latency | 13 ms |
| Maximum latency | 14 ms |

The traffic generator reported **CONNECTIVITY CONFIRMED**, demonstrating communication between the API and COBOL core.

Evidence: `Screenshots/swift_traffic_run1.jpg`

## Remaining Work

- Complete and document EC2 runs 2–7.
- Record instance termination and cleanup for each run.
- Complete Git clone verification.
- Complete the required research and AI review files.
- Complete the partner spot-check.
- Add required Udemy quiz screenshots.
- Commit and push the completed assignment to GitHub.
### Run 2 — October 29, 2026

- Instance: SEIR-Lesson1-Run2
- Instance ID: i-040f35542748368b7
- Region: us-east-2 (Ohio)
- Availability Zone: us-east-2a
- Instance type: t3.micro
- Public IPv4: 52.15.54.249
- Public DNS: ec2-52-15-54-249.us-east-2.compute.amazonaws.com
- Boot time (UTC): 2026-10-29 09:33:09
- Screenshot: Screenshots/lab1_run2.jpg
- Screenshot time (PDT): [Oct 29 03:44:34 PDT 2026]
- Runbook: Steps 0–9 completed
- SWIFT traffic: 10 sent, 7 posted, 3 rejected, 0 failed
- API tests: /status, /chewbacca, /accounts/100001, /ask passed
- Git clone evidence: Screenshots/git_clone.jpg
- Termination: Terminated October 29, 2026
- Cleanup: No remaining EBS volumes or Elastic IPs
### Run 3 — October 29, 2026

- Instance: SEIR-Lesson1-Run3
- Instance ID: i-028f587f141627d58
- Region: us-east-2 (Ohio)
- Availability Zone: us-east-2a
- Instance type: t3.micro
- Public IPv4: 3.17.173.95
- Public DNS: ec2-3-17-173-95.us-east-2.compute.amazonaws.com
- Boot time (UTC): 2026-10-29 11:52:52
- Screenshot: Screenshots/lab1_run3.jpg
- Screenshot time (PDT): [Oct 29 05:14:01 PDT 2026]
- Runbook: Steps 0–9 completed
- SWIFT traffic: 10 sent, 6 posted, 4 rejected, 0 failed
- API tests: /status, /chewbacca, /accounts/100001, /ask passed
- Termination: Terminated October 29, 2026
- Cleanup: No remaining EBS volumes or Elastic IPs
  