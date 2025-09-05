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
