# Project Capstone: Full-Stack Security Lab

---

## 1. Project Goal

The objective of this project was to design, build, and secure a full-stack application environment to demonstrate a comprehensive range of cybersecurity skills. The project spanned cloud infrastructure, CI/CD automation, offensive penetration testing (red team), and defensive security monitoring and detection (blue team).

---

## 2. Architecture

The lab was built on a local host machine, using VirtualBox for virtualization and Docker for containerization. The architecture consists of a Kali Linux "attacker" VM on a private host-only network and a "server" environment running the target web application (OWASP Juice Shop) and a Splunk SIEM instance.

This setup allowed for realistic attack simulation and log analysis in a safe, isolated environment.

![Project Architecture Diagram](assets/architecture.png)

---

## 3. Key Findings & Accomplishments

* **Infrastructure as Code (IaC)**: A reusable cloud network environment (VPC, subnets, security groups, EC2 instance) was built using Terraform.
* **CI/CD Automation**: Automated testing pipelines were created with GitHub Actions to validate Terraform code, build and test the application container, and lint shell scripts.
* **Offensive Security**: A penetration test was conducted against a target web application, resulting in the discovery and exploitation of two major vulnerabilities:
    * **Critical Risk**: Authentication Bypass via SQL Injection.
    * **High Risk**: Stored Cross-Site Scripting (XSS).
* **Defensive Security**: A Splunk SIEM was deployed, and a log forwarding pipeline was created. Logs from the target application were successfully ingested, parsed, and monitored.
* **Detection Engineering**: A custom real-time alert was built in Splunk to successfully detect the SQL injection attack signature observed during the penetration test.
* **Remediation**: The discovered vulnerabilities were remediated in the application source code, and the infrastructure was hardened by restricting insecure firewall rules.

---

## 4. Business Impact & Next Steps

### Business Impact

The identified vulnerabilities posed a significant risk. The SQL injection flaw could have led to a complete compromise of all user data and administrative control, while the XSS flaw could have enabled account takeovers and phishing attacks against users. The successful implementation of a detection and alerting pipeline demonstrates a foundational capability for a modern Security Operations Center (SOC).

### Next Steps

Future work on this project could include:
* Expanding the SIEM detection rule set to cover more MITRE ATT&CK techniques.
* Integrating automated security scanning tools (SAST/DAST) directly into the CI/CD pipeline.
* Migrating the entire lab environment into a real cloud provider using the developed Terraform code.
