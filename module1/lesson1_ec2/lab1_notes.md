# SEIR Foundations — Module 1, Lesson 1
## Balerica Legacy Bank — Personal Lab Notes

**AWS Region:** us-east-2 (Ohio)
**Operating System:** Amazon Linux 2023
**Application:** FastAPI with GnuCOBOL banking core

## Seven Manual EC2 Lab Runs

### Run 1 — October 29, 2026
**Instance ID:** i-069654b4e4b12ff2a

During Run 1, I manually deployed the Balerica Legacy Bank application on a new Amazon EC2 instance using Amazon Linux 2023. I installed the application dependencies, started the FastAPI server using Uvicorn on port 8000, and verified that the application could communicate with the GnuCOBOL banking core. I also ran the SWIFT traffic generator, which sent 10 simulated payment requests: 6 were posted, 4 were rejected, and none failed. This helped me understand how an EC2-hosted API communicates with a legacy COBOL banking system and how business rejections differ from technical failures.

**Run 1 evidence:** `Screenshots/lab1_run1.jpg` and `Screenshots/swift_traffic_run1.jpg`

**Exact output line:** `INFO:     Started server process [37565]

### Run 2 — October 29, 2026
**Instance ID:** i-040f35542748368b7

During Run 2, I launched a new EC2 instance (`i-040f35542748368b7`) and manually installed the Balerica Legacy Bank application. I encountered several installation problems, beginning with `No match for argument: gnucobol`, which required installing the other dependencies and compiling GnuCOBOL 3.2 from source. During compilation, the configuration process failed because the Berkeley DB development header (`db.h`) was missing; I resolved this by installing `libdb-devel` and rerunning the configuration. When testing the compiled COBOL program, I encountered a missing `libcob.so.4` shared-library error, which I resolved by registering `/usr/local/lib` with the Linux dynamic linker and running `ldconfig`.

After resolving these issues, I successfully started Uvicorn on port 8000 and verified the `/status`, `/chewbacca`, `/accounts/100001`, and `/ask` API endpoints. The SWIFT traffic generator processed 10 simulated payments: 7 posted, 3 rejected, and 0 technical failures. This run taught me the difference between installing a package, compiling software from source, and configuring Linux to locate shared libraries at runtime.

**Evidence:** `Screenshots/lab1_run2.jpg`

**Exact output line:** `INFO:     Started server process [38503]`

### Run 3 — October 29, 2026
**Instance ID:** i-028f587f141627d58

During Run 3, I manually launched another EC2 instance (`i-028f587f141627d58`) and repeated the Balerica Legacy Bank deployment process. I successfully started the FastAPI application using Uvicorn on port 8000 and verified the `/status`, `/chewbacca`, `/accounts/100001`, and `/ask` endpoints. The SWIFT traffic generator processed 10 simulated payment requests, with 6 posted, 4 rejected, and no technical failures. Unlike Run 2, I have not documented a specific installation error for this run. Repeating the deployment helped me become more familiar with the Linux commands, application installation sequence, and verification procedures needed to operate the banking system independently.

**Evidence:** `Screenshots/lab1_run3.jpg`

**Exact output line:** `INFO:     Started server process [34469]`

### Run 4 — October 30, 2026
**Instance ID:** i-07c2b0944a9d1eac9

During Run 4, I manually launched a new EC2 instance (`i-07c2b0944a9d1eac9`) and successfully installed the Balerica Legacy Bank application. I started Uvicorn on port 8000 and verified that the banking application displayed **FastAPI: ONLINE** in my Chrome browser. The SWIFT traffic generator processed 10 simulated payments, with 4 posted, 6 rejected, and no technical failures.

I encountered two minor terminal mistakes. First, I entered Linux commands into the terminal already running Uvicorn, not realizing that the server process was occupying that terminal. I corrected this by opening a second EC2 Instance Connect terminal for additional commands. Second, I accidentally copied the Linux shell prompt along with a command, which caused a command-entry error. These experiences helped me understand the difference between a running foreground process and an available command prompt, as well as why I should copy only the command itself.

I also practiced locating the COBOL source files and learned how the EC2 instance's public IP address, port 8000, and FastAPI's `/docs` path combine to create the interactive banking API URL. After completing the run, I terminated the instance and verified that no EBS volumes or Elastic IP addresses remained in the Ohio region.

**Evidence:** `Screenshots/lab1_run4.jpg` and `Screenshots/swift_traffic_run4.jpg`

**Exact output line:** `INFO:     Started server process [34661]`


### Run 5 — October 31, 2026
**Instance ID:** `i-0d2038e61975bb463`

During Run 5, I launched a fresh Amazon EC2 instance using my approved basic launch template, `mybank`, and manually installed the Balerica Legacy Bank application. The template provided the basic EC2 configuration but did not contain a preinstalled application or automated installation script. I installed Git, cloned the SEIR Foundations repository, executed the installation script, activated the Python virtual environment, and started Uvicorn on port 8000.

I verified the `/status` and `/chewbacca` endpoints and successfully generated 10 simulated SWIFT payments: 7 posted, 3 rejected, and 0 technical failures. I also encountered a minor command-entry issue while upgrading pip because I copied an incorrectly quoted command. After correcting the command, I completed the upgrade and continued testing. This run reinforced the importance of checking command syntax and distinguishing between a reusable EC2 configuration and a fully configured application.

**Evidence:** `Screenshots/lab1_run5.jpg` and `Screenshots/swift_traffic_run5.jpg`

**Exact output line:** `INFO:     Started server process [35047]`

**Result:** Instance terminated; no remaining EBS volumes or Elastic IPs.

### Run 6 — October 31, 2026
**Instance ID:** `i-0174dbb9daa11a42d`

During Run 6, I launched another fresh EC2 instance using the approved basic launch template and manually repeated the banking application deployment. I installed Git, cloned the source repository, ran the application installer, activated the virtual environment, and started the FastAPI server with Uvicorn. I recorded the instance identification information and Pacific time immediately before starting the server.

I successfully verified the `/status` and `/chewbacca` API endpoints. The SWIFT traffic generator processed 10 simulated payment requests: 8 posted, 2 rejected, and 0 technical failures. This run helped me become more efficient at repeating the deployment sequence while maintaining separate evidence for each instance, including its unique instance ID, boot time, and Uvicorn process ID.

**Evidence:** `Screenshots/lab1_run6.jpg` and `Screenshots/swift_traffic_run6.jpg`

**Exact output line:** `INFO:     Started server process [34380]`

**Result:** Instance terminated; no remaining EBS volumes or Elastic IPs.

### Run 7 — October 31, 2026
**Instance ID:** `i-0e044b9bfa972626e`

During Run 7, I completed the seventh and final EC2 deployment of the Balerica Legacy Bank application. I used the approved basic launch template to create a new instance and manually installed the application rather than using a preconfigured application image. After completing the installation, I activated the Python virtual environment, captured the required identification and boot-time information, and started Uvicorn on port 8000.

I verified that both `/status` and `/chewbacca` were operational. The SWIFT traffic generator sent 10 simulated payment requests, with 6 posted, 4 rejected, and 0 technical failures. I saved the required Uvicorn and SWIFT screenshots, recorded the instance's public IPv4 address and DNS, and terminated the instance. I then confirmed that no leftover EBS volumes or Elastic IP addresses remained. Completing this run demonstrated that I could repeatedly deploy, test, document, and clean up an EC2-hosted application.

**Evidence:** `Screenshots/lab1_run7.jpg` and `Screenshots/swift_traffic_run7.jpg`

**Exact output line:** `INFO:     Started server process [34145]`

**Result:** Instance terminated; no remaining EBS volumes or Elastic IPs.

## COBOL Practice


### Return Code 0 — Success

I tested the COBOL account lookup program using account number `100001`, which belongs to Alice Johnson. The lookup succeeded and displayed an initial account balance of $5,000.00. Return code 0 indicates that the requested operation completed successfully.

Command:
`./cobol/bin/account_lookup 100001`

Evidence: `Screenshots/cobol_rc0.jpg`

### Return Code 4 — Account Not Found

I tested the COBOL account lookup program using account number `999999`, which did not exist in the account records. The program reported that the account could not be found. Return code 4 identifies an unsuccessful lookup rather than a failure of the operating environment.

Command:
`./cobol/bin/account_lookup 999999`

Evidence: `Screenshots/cobol_rc4.jpg`

### Return Code 8 — Business Rejection

I tested the COBOL payment-processing program with a payment amount that exceeded the account's available balance. The transaction was rejected because sufficient funds were unavailable. Return code 8 represents a business-rule rejection rather than a technical failure.

Evidence: `Screenshots/cobol_rc8.jpg`

### Return Code 12 — Environment Failure

I tested how the COBOL payment-processing program responds when required command arguments are missing. The command was unsuccessful because the necessary transaction information was not supplied. In this lab, return code 12 represents a command or execution failure rather than a normal business rejection.

Evidence: `Screenshots/cobol_rc12.jpg`

### Fixed-Width Ledger Decoding

The Balerica Legacy Bank application stores account records in a fixed-width ledger file located at `data/accounts.dat`. Unlike a CSV file, which separates fields using commas, a fixed-width file stores each field in a predetermined character position.

I examined the ledger structure and identified the following fields:

| Character Positions | Field |
|---|---|
| 1–6 | Account number |
| 7–36 | Customer name |
| 37–44 | Account status |
| 45–56 | Balance in cents |
| 57–59 | Currency |

For account `100001`, belonging to Alice Johnson, the initial balance was $5,000.00. The ledger represents this amount as `000000500000`, which is 500,000 cents.

This exercise helped me understand how legacy banking systems store structured financial information without using modern database tables or CSV delimiters. It also demonstrated why accurately interpreting field positions is essential when connecting COBOL programs to newer applications.

**Evidence:** `Screenshots/cobol_ledger_decode.jpg`


### Transaction Journal and Balance Changes

The Balerica Legacy Bank lab demonstrated how COBOL programs process account lookups and payment transactions. I verified successful account lookup, nonexistent-account handling, insufficient-funds rejection, and missing-argument handling.

Alice Johnson's account (`100001`) had an initial balance of $5,000.00, represented in the fixed-width ledger as `000000500000` cents.

The SWIFT traffic generator also demonstrated successful and rejected payment requests. Across my seven EC2 deployments, the generator processed 70 simulated requests: 44 posted, 26 rejected, and 0 technical failures.

I did not preserve the individual COBOL transaction journal entries, transaction IDs, or final account balances in my local notes. Therefore, I cannot independently document the exact balance changes associated with individual payments.

The exercise helped me understand the importance of recording transaction identifiers, payment amounts, return codes, and account balances when testing financial applications.


### Successful Payment and Journal Verification — October 31, 2026

I launched a separate temporary EC2 instance to complete the COBOL transaction journal verification without altering my seven original deployment records.

**Verification instance:** `i-0ae2faee0ef2700f9`  
**Region:** `us-east-2`  
**Evidence time:** October 31, 2026, 8:48:45 PM PDT  
**Application directory:** `/opt/balerica-bank`

I first used `./cobol/bin/account_lookup 100001` to verify that Alice Johnson's account had a starting balance of $5,000.00. The lookup returned code 0.

I then executed:

`./cobol/bin/payment_post TXN-THJ-0003 100001 125.50 USD INV-1003; echo "RETURN_CODE=$?"`

The payment returned `STATUS=POSTED`, `REASON=APPROVED`, and `RETURN_CODE=0`.

I inspected the transaction journal using:

`cat data/payments.dat`

The journal contained the following record:

`TXN-THJ-0003        100001000000012550USDPOSTED  INV-1003`

This confirmed that the $125.50 payment was recorded as posted.

I subsequently repeated the account lookup for account `100001`. The reported balance remained $5,000.00, producing an observed balance change of $0.00.

Although the payment was recorded as posted, the account lookup did not reflect a debit. I documented this discrepancy rather than assuming that the balance decreased. Further examination of the application would be required to determine why the account balance remained unchanged.

**Evidence:** `Screenshots/cobol_transaction_journal.jpg`


### Explanation of the Unchanged Account Balance

I investigated why Alice Johnson's balance remained $5,000.00 after the $125.50 payment was approved. I inspected the COBOL source file using `grep` and `sed`, focusing on the payment-validation and journal-writing sections.

The code compares the requested payment amount with the available account balance. When the payment satisfies the validation rules, it assigns `POSTED` and `APPROVED`, then writes the transaction to `data/payments.dat`.

The inspected code does not contain an instruction to subtract the payment amount from the account balance or update `data/accounts.dat`. This is consistent with the observed behavior: the payment was recorded in the journal, but the subsequent account lookup still returned $5,000.00.

This exercise helped me distinguish between validating and recording a financial transaction and actually updating an account's stored balance.

### Verified COBOL Transaction Attempts

I used transaction IDs beginning with my initials, THJ.

- `TXN-THJ-0001`: Attempted to post $9,999.00 from account `100001`. The COBOL program returned `STATUS=REJECTED`, `REASON=INSUFFICIENT FUNDS`, and exit code 8.
- `TXN-THJ-0002`: Attempted to post an invalid amount (`ABC`) from account `100001`. The program returned `STATUS=REJECTED`, `REASON=AMOUNT MUST BE GREATER THAN ZERO`, and exit code 8.

Both transactions were rejected. Neither was confirmed as posted. The screenshot does not show the transaction journal file or a subsequent account lookup, so I cannot independently verify journal entries or the final account balance.

Evidence: `Screenshots/cobol_rc12.jpg`


## Mistakes I Made

During the seven EC2 deployments, I encountered several problems that improved my understanding of Linux, AWS, and application deployment.

1. **Missing GnuCOBOL package:** During Run 2, the package manager could not find `gnucobol`. I learned how to compile GnuCOBOL 3.2 from source instead of relying on a prebuilt package.

2. **Missing development dependency:** The GnuCOBOL configuration process could not find `db.h`. Installing `libdb-devel` resolved the missing-header problem.

3. **Missing shared library:** A COBOL executable could not locate `libcob.so.4`. I learned how to configure the Linux dynamic linker and use `ldconfig` to make shared libraries available.

4. **Using a busy terminal:** During Run 4, I entered commands into the terminal already running Uvicorn. I learned to open a second EC2 Instance Connect session for testing while the server continued running.

5. **Copying the shell prompt:** I accidentally included the Linux shell prompt when copying a command. I learned to copy only the command itself.

6. **Incorrect command quoting:** During Run 5, an incorrectly quoted pip command caused an error. I corrected the syntax and completed the operation.

7. **Incomplete transaction documentation:** Although I preserved COBOL return-code screenshots, I did not record the individual transaction journal entries and resulting account balances in my local notes. I learned that financial application testing requires careful documentation of transaction IDs, amounts, return codes, and before-and-after balances.

These experiences reinforced the importance of checking dependencies, understanding Linux processes, validating commands before executing them, and preserving evidence during each deployment.

## Commands I Now Know by Heart

During this lab, I practiced the following commands and learned how they support EC2 application deployment, testing, and troubleshooting.

### Linux and Git Commands

| Command | Purpose |
|---|---|
| `pwd` | Display the current working directory. |
| `ls` | List files and directories. |
| `cd` | Change directories. |
| `sudo dnf install -y git` | Install Git on Amazon Linux 2023. |
| `git clone https://github.com/BalericaAI/SEIR-Foundations.git` | Download the lab source repository. |
| `bash install/install.sh` | Execute the Balerica Bank installation script. |

### Python and FastAPI Commands

| Command | Purpose |
|---|---|
| `source venv/bin/activate` | Activate the Python virtual environment. |
| `uvicorn app.main:app --host 0.0.0.0 --port 8000` | Start the FastAPI application on port 8000. |
| `python3 swift/traffic_generator.py --count 10` | Generate 10 simulated SWIFT payment requests. |
| `curl -s http://127.0.0.1:8000/status` | Check the application's status endpoint. |
| `curl -s http://127.0.0.1:8000/chewbacca` | Verify the Chewbacca endpoint. |

### EC2 Identification Commands

| Command | Purpose |
|---|---|
| `whoami` | Identify the current Linux user. |
| `TZ='America/Los_Angeles' date` | Display the current Pacific date and time. |
| `ec2-metadata -i` | Display the EC2 instance ID. |
| `uptime -s` | Display the instance's system boot time. |

### COBOL Commands

| Command | Purpose |
|---|---|
| `./cobol/bin/account_lookup 100001` | Look up Alice Johnson's account. |
| `./cobol/bin/account_lookup 999999` | Test a nonexistent account. |
| `./cobol/bin/payment_post TXN0001 100001 125.50 USD INV-1001` | Example payment-posting command showing the required arguments. |

### Important Lessons

I learned that Uvicorn occupies the terminal while running in the foreground, so I can use a second EC2 Instance Connect session to execute API tests and SWIFT traffic commands.

I also learned to record the instance ID, Pacific date and time, and boot time immediately before starting Uvicorn. This helps establish that each deployment used a distinct EC2 instance.

Finally, I learned to terminate unused instances and check for leftover EBS volumes and Elastic IP addresses to avoid unnecessary AWS charges.
