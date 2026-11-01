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

| Run | Date | Time zone | Instance ID | Boot time (UTC) | Public IPv4 DNS | Screenshot | Terminated? |
|---|---|---|---|---|---|---|---|
| 1 | 2026-10-29 | America/Los_Angeles | `i-069654b4e4b12ff2a` | 2026-10-29 05:55:56 | `ec2-13-184-105-199.us-east-2.compute.amazonaws.com` | `Screenshots/lab1_run1.jpg` | Yes |
| 2 | 2026-10-29 | America/Los_Angeles | `i-040f35542748368b7` | 2026-10-29 09:33:09 | `ec2-52-15-54-249.us-east-2.compute.amazonaws.com` | `Screenshots/lab1_run2.jpg` | Yes |
| 3 | 2026-10-29 | America/Los_Angeles | `i-028f587f141627d58` | 2026-10-29 11:52:52 | `ec2-3-17-173-95.us-east-2.compute.amazonaws.com` | `Screenshots/lab1_run3.jpg` | Yes |
| 4 | 2026-10-30 | America/Los_Angeles | `i-07c2b0944a9d1eac9` | 2026-10-30 21:58:10 | `ec2-13-59-173-40.us-east-2.compute.amazonaws.com` | `Screenshots/lab1_run4.jpg` | Yes |
| 5 | 2026-10-31 | America/Los_Angeles | `i-0d2038e61975bb463` | 2026-11-01 00:05:48 | `ec2-18-223-206-240.us-east-2.compute.amazonaws.com` | `Screenshots/lab1_run5.jpg` | Yes |
| 6 | 2026-10-31 | America/Los_Angeles | `i-0174dbb9daa11a42d` | 2026-11-01 01:23:08 | `ec2-3-14-248-3.us-east-2.compute.amazonaws.com` | `Screenshots/lab1_run6.jpg` | Yes |
| 7 | 2026-10-31 | America/Los_Angeles | `i-0e044b9bfa972626e` | 2026-11-01 01:56:57 | `ec2-18-217-203-210.us-east-2.compute.amazonaws.com` | `Screenshots/lab1_run7.jpg` | Yes |


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

- [ ] Complete and document EC2 runs 5–7.
- [ ] Verify all seven screenshots against instance IDs and boot times.
- [ ] Complete `lab1_notes.md`, including the seven run summaries and COBOL practice documentation.
- [ ] Verify COBOL return-code evidence and journal entries.
- [ ] Complete and cross-check `spotter_THasanJohnson.txt`.
- [ ] Verify the Git clone evidence and required AI review and study files.
- [ ] Verify the Maarek Section 21, 23, and 25 quiz screenshots.
- [ ] Commit and push the completed assignment to GitHub.

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

  ### Run 4 — October 30, 2026

- Instance: SEIR-Lesson1-Run4
- Instance ID: i-07c2b0944a9d1eac9
- Region: us-east-2 (Ohio)
- Availability Zone: us-east-2a
- Instance type: t3.micro
- Public IPv4: 13.59.173.40
- Public DNS: ec2-13-59-173-40.us-east-2.compute.amazonaws.com
- Boot time (UTC): 2026-10-30 21:58:10
- Screenshot: Screenshots/lab1_run4.jpg
- Screenshot time (PDT): October 30, 2026, 3:21:45 PM
- SWIFT traffic: 10 sent, 4 posted, 6 rejected, 0 failed
- Average latency: 22 ms
- Maximum latency: 62 ms
- SWIFT evidence: Screenshots/swift_traffic_run4.jpg
- Application: FastAPI running successfully on port 8000
- Termination: Terminated October 30, 2026
- Cleanup: No remaining EBS volumes or Elastic IPs

### Run 5 — October 31, 2026

- Instance: SEIR-Lesson1-Run5
- Instance ID: `i-0d2038e61975bb463`
- Region: `us-east-2` (Ohio)
- Instance type: `t3.micro`
- Public IPv4: `18.223.206.240`
- Public DNS: `ec2-18-223-206-240.us-east-2.compute.amazonaws.com`
- Boot time (UTC): `2026-11-01 00:05:48`
- Screenshot time (PDT): October 31, 2026, 5:43:46 PM
- Uvicorn PID: `35047`
- Application: FastAPI running successfully on port 8000
- SWIFT traffic: 10 sent, 7 posted, 3 rejected, 0 failed
- Average latency: 29 ms
- Maximum latency: 48 ms
- API tests: `/status` and `/chewbacca` passed
- Screenshot: `Screenshots/lab1_run5.jpg`
- SWIFT evidence: `Screenshots/swift_traffic_run5.jpg`
- Termination: Terminated October 31, 2026
- Cleanup: No remaining EBS volumes or Elastic IPs

### Run 6 — October 31, 2026

- Instance: SEIR-Lesson1-Run6
- Instance ID: `i-0174dbb9daa11a42d`
- Region: `us-east-2` (Ohio)
- Instance type: `t3.micro`
- Public IPv4: `3.14.248.3`
- Public DNS: `ec2-3-14-248-3.us-east-2.compute.amazonaws.com`
- Boot time (UTC): `2026-11-01 01:23:08`
- Screenshot time (PDT): October 31, 2026, 6:40:05 PM
- Uvicorn PID: `34380`
- Application: FastAPI running successfully on port 8000
- SWIFT traffic: 10 sent, 8 posted, 2 rejected, 0 failed
- Average latency: 43 ms
- Maximum latency: 83 ms
- API tests: `/status` and `/chewbacca` passed
- Screenshot: `Screenshots/lab1_run6.jpg`
- SWIFT evidence: `Screenshots/swift_traffic_run6.jpg`
- Termination: Terminated October 31, 2026
- Cleanup: No remaining EBS volumes or Elastic IPs

### Run 7 — October 31, 2026

- Instance: SEIR-Lesson1-Run7
- Instance ID: `i-0e044b9bfa972626e`
- Region: `us-east-2` (Ohio)
- Instance type: `t3.micro`
- Public IPv4: `18.217.203.210`
- Public DNS: `ec2-18-217-203-210.us-east-2.compute.amazonaws.com`
- Boot time (UTC): `2026-11-01 01:56:57`
- Screenshot time (PDT): October 31, 2026, 7:08:25 PM
- Uvicorn PID: `34145`
- Application: FastAPI running successfully on port 8000
- SWIFT traffic: 10 sent, 6 posted, 4 rejected, 0 failed
- Average latency: 13 ms
- Maximum latency: 14 ms
- API tests: `/status` and `/chewbacca` passed
- Screenshot: `Screenshots/lab1_run7.jpg`
- SWIFT evidence: `Screenshots/swift_traffic_run7.jpg`
- Termination: Terminated October 31, 2026
- Cleanup: No remaining EBS volumes or Elastic IPs
