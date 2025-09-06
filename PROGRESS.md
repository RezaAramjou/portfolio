- | 3 | Master Subnetting | [Timed Problems](https://github.com/RezaAramjou/subnetting-cheatsheet/tree/main/examples/timed_problems.md) | Completed (Avg time: ~23s) |
- | **Week 1** | **Network Fundamentals & Lab Setup** | **[View Week 1 Deliverable](https://github.com/RezaAramjou/labs/blob/main/network-lab/README.md)** | **Completed** |
---
### Week 2: Infrastructure as Code (IaC) and Automation

| Day | Task                                                               | Link                                                                                                                             | Status      |
|-----|--------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|-------------|
| 8   | Terraform design and state backend planning                        | [Terraform Design](https://github.com/RezaAramjou/terraform/blob/main/design.md)                                          | ✅ Complete |
| 9   | Built VPC, Subnets, and Bastion Host with Terraform                | [Terraform Code](https://github.com/RezaAramjou/terraform/tree/main/examples/ec2-vpc-demo)                                  | ✅ Complete |
| 10  | Created Dockerized App and EC2 user data script                    | [Docker App](https://github.com/RezaAramjou/docker-app) / [User Data Script](https://github.com/RezaAramjou/terraform/blob/main/examples/ec2-vpc-demo/userdata.sh) | ✅ Complete |
| 11  | Added Terraform examples for logging and billing alarms            | [Logging Examples](https://github.com/RezaAramjou/terraform/tree/main/examples/logging)                                   | ✅ Complete |
| 12  | Built CI/CD pipelines with GitHub Actions for all repos            | [Docker CI](https://github.com/RezaAramjou/docker-app/blob/main/.github/workflows/ci.yml) / [Terraform CI](https://github.com/RezaAramjou/terraform/blob/main/.github/workflows/terraform-ci.yml) | ✅ Complete |
| 13  | Formalized LocalStack testing setup and documentation              | [LocalStack Setup](https://github.com/RezaAramjou/labs/blob/main/docker/localstack/docker-compose-localstack.yml)         | ✅ Complete |
| 14  | Published Week 2 deliverable and safety checklist                  | [Safety Checklist](https://github.com/RezaAramjou/terraform/blob/main/examples/ec2-vpc-demo/README.md#%EF%B8%8F-billing-safety-checklist) | ✅ Complete |

---
### Week 3: Red Team / Blue Team Sprint

| Day | Task                                                               | Link                                                                                  | Status      |
|-----|--------------------------------------------------------------------|---------------------------------------------------------------------------------------|-------------|
| 15  | Deployed vulnerable application (Juice Shop) & performed baseline scans | [Week 3 Artifacts Summary](https://github.com/RezaAramjou/portfolio/blob/main/ARTIFACTS.md) | ✅ Complete |
| 16  | Performed offensive testing; exploited SQLi and XSS vulnerabilities   | [Week 3 Artifacts Summary](https://github.com/RezaAramjou/portfolio/blob/main/ARTIFACTS.md) | ✅ Complete |
| 17  | Deployed Splunk SIEM and created a log ingestion pipeline          | [Week 3 Artifacts Summary](https://github.com/RezaAramjou/portfolio/blob/main/ARTIFACTS.md) | ✅ Complete |
| 18  | Conducted a purple team exercise; created a detection rule in Splunk | [Week 3 Artifacts Summary](https://github.com/RezaAramjou/portfolio/blob/main/ARTIFACTS.md) | ✅ Complete |
| 19  | Wrote a professional penetration test report                       | [Week 3 Artifacts Summary](https://github.com/RezaAramjou/portfolio/blob/main/ARTIFACTS.md) | ✅ Complete |
| 20  | Remediated vulnerabilities and re-tested to verify fixes           | [Week 3 Artifacts Summary](https://github.com/RezaAramjou/portfolio/blob/main/ARTIFACTS.md) | ✅ Complete |
| 21  | Published Week 3 deliverable (Artifacts Summary)                   | [Week 3 Artifacts Summary](https://github.com/RezaAramjou/portfolio/blob/main/ARTIFACTS.md) | ✅ Complete |

---
### Week 4: Polish, Interview Kit, and Capstone

| Day | Task                                                               | Link                                                                                  | Status      |
|-----|--------------------------------------------------------------------|---------------------------------------------------------------------------------------|-------------|
| 22  | Created Capstone Executive Summary & Architecture Diagram          | [Capstone Summary](https://github.com/YourGitHubUsername/portfolio/blob/main/CAPSTONE.md) | ✅ Complete |
| 23  | *(Skipped)* Technical Walkthrough Videos                           | N/A                                                                                   | N/A         |
| 24  | Wrote 10 Resume Bullets Tailored for Cloud/Security Roles          | [Resume Bullets](https://github.com/YourGitHubUsername/job-kit/blob/main/resume-bullets.md) | ✅ Complete |
| 25  | Prepared Mock Interview Q&A Document                               | [Interview Q&A](https://github.com/YourGitHubUsername/job-kit/blob/main/mock-interviews/README.md) | ✅ Complete |
| 26  | Finalized all repository READMEs for clarity and reproducibility   | N/A                                                                                   | ✅ Complete |
| 27  | Wrote Full Capstone Document with Threat Model and Mitigations     | [Full Capstone](https://github.com/YourGitHubUsername/portfolio/blob/main/CAPSTONE_FULL.md) | ✅ Complete |
| 28+ | Polished documentation and prepared job application materials      | [Cover Letters](https://github.com/YourGitHubUsername/job-kit/tree/main/cover-letters) | ✅ Complete |



# 30-Day Pentesting Mastery Plan

## Day 1: Lab Kickoff & OSINT Sandbox (2025-09-04)

*Summary:* Kicked off the engagement by defining the scope, including a Juice Shop container and an Ubuntu VM, within a formal Rules of Engagement document. On the defensive side, I enabled `auditd` on the target VM to establish baseline host telemetry. This initial state was captured in documentation and a dashboard screenshot, providing a clean baseline for future threat detection.

*Deliverables:*
* `pentest/ROE.md`
* `siem-lab/baseline/host-baseline.md`
* `siem-lab/dashboards/baseline.png`

## Day 2: External Recon & Wordlists (2025-09-05)

*Summary:* Performed external reconnaissance against the Juice Shop web application. I used nmap for port scanning, whatweb for technology fingerprinting, and a fine-tuned gobuster scan to discover key directories like `/api` and `/ftp`. Based on these findings, I created a custom wordlist and wrote a Sigma-style detection rule to identify directory enumeration activity.

*Deliverables:*
* `pentest/recon/recon-notes.md`
* `pentest/wordlists/custom.txt`
* `siem-lab/rules/web-dirbusting.yml`

## Day 3: Web Mapping & Auth Flows (2025-09-05)

*Summary:* Set up Burp Suite to proxy and analyze the Juice Shop's web traffic. I successfully mapped the user registration and login flows, identifying that the application uses JWTs for session management. Key discoveries include a potential IDOR vulnerability in the basket API and a hidden `/ftp` directory, all of which have been documented.

*Deliverables:*
* `pentest/web/mapping.md`
* `pentest/web/proxy-export.xml`
* `siem-lab/parsers/web-headers.md`

## Day 4: Input Validation & File Handling Tests (2025-09-06)

*Summary:* Shifted focus to planning active tests by creating a systematic test catalog for the Juice Shop application. The plan outlines methodologies for identifying vulnerabilities like SQLi, XSS, and insecure file uploads without using live payloads. In parallel, I developed a corresponding defensive rule to detect suspicious file uploads based on dangerous extensions or MIME type mismatches.

*Deliverables:*
* `pentest/web/test-catalog.md`
* `siem-lab/rules/suspicious-file-upload.yml`

## Day 5: AuthZ/AuthN Weaknesses (2025-09-06)

*Summary:* Conducted an assessment of the web application's authentication and session management controls. I identified several weaknesses, including a weak password policy, no account lockout mechanism, and improper session invalidation on logout. To counter these threats, I designed two new detection rules: one to identify brute-force login attempts and another to detect session hijacking via token anomalies.

*Deliverables:*
* `pentest/web/auth-findings.md`
* `siem-lab/rules/auth-brute.yml`
* `siem-lab/rules/auth-token-anomaly.yml`

## Day 6: API Security (REST/JSON) (2025-09-06)

*Summary:* Focused on the application's API security. I created a comprehensive inventory of all discovered API endpoints and then developed a methodical test plan to check for common vulnerabilities like IDOR, rate-limiting issues, and mass assignment. To counter these threats, I designed a SIEM rule to detect API abuse by monitoring for an abnormally high volume of requests from a single source.

*Deliverables:*
* `pentest/api/inventory.md`
* `pentest/api/api-test-plan.md`
* `siem-lab/rules/api-ratelimit-breach.yml`

## Day 7: Web/App Mini-Report & Hotfix Sprint (2025-09-06)

*Summary:* Concluded Week 1 by consolidating all web and API findings into a concise mini-report. The report summarizes key vulnerabilities, including weak authentication, potential IDOR, and lack of rate limiting. As a Blue Team exercise, I documented three high-impact "hotfix" recommendations to mitigate the most critical risks discovered.

*Deliverables:*
* `pentest/reports/week1-web-mini-report.md`


## Day 8: Linux Foothold & Basics (2025-09-06)

*Summary:* Shifted focus to host-level security by performing an initial enumeration of the target Ubuntu VM. This process revealed several critical privilege escalation paths, including full `sudo` privileges and membership in the `docker` and `lxd` groups. I documented this enumeration process in a reusable checklist and created a corresponding Blue Team rule to detect SUID enumeration, a common attacker technique.

*Deliverables:*
* `pentest/linux/enum-checklist.md`
* `siem-lab/rules/linux-suid-hunting.yml`

## Day 9: Linux Privilege Escalation Lab (2025-09-06)

*Summary:* Performed hands-on privilege escalation on the target Linux VM. I successfully escalated to root by abusing overly permissive `sudo` rights and by leveraging my user's membership in the `docker` group, documenting the methodology for each. In response, I created a SIEM rule to detect anomalous `sudo` usage, specifically looking for commands that spawn interactive root shells.

*Deliverables:*
* `pentest/linux/privesc-methods.md`
* `siem-lab/rules/linux-sudo-anomaly.yml`
