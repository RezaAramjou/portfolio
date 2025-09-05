------------------------------------------------------------------------

# Full Capstone Project Report: End-to-End Pentesting and Detection Engineering

**Author**: Reza Aramjou **Date**: \[2025.09.06\]

------------------------------------------------------------------------

## 2. Detailed Architecture

The lab is comprised of three distinct components, simulating an
analyst's workstation, an attacker's machine, and a target server.

-   **Main OS (Ubuntu)**: The **Analyst Workstation**. This machine
    serves as the "office" and hosts all project repositories, including
    `portfolio`, `pentest`, and `siem-lab`, where all documentation,
    findings, and detection rules are developed.
-   **Kali Linux VM**: The dedicated **Attacker Machine**. It is
    connected to the target via a VirtualBox Host-Only network and is
    used to conduct all offensive activities, from reconnaissance to
    exploitation.
-   **Ubuntu Server VM**: The **Target Host**. This server runs Docker
    to host the primary target, **OWASP Juice Shop**, and is the focal
    point for all monitoring. It generates the logs (web server,
    `auditd`) that are conceptually forwarded to a SIEM.
-   **Networking**: A private `192.168.56.0/24` network facilitates
    communication between the attacker VM and the target host, creating
    an isolated and safe testing environment.

------------------------------------------------------------------------

## 3. How to Reproduce the Lab

The following steps outline how to set up and run the entire lab
environment.

### Prerequisites

-   Git
-   VirtualBox
-   Docker & Docker Compose

### Step 1: Clone All Repositories

Clone all project repositories to your **Main OS (Ubuntu)**.

``` bash
git clone https://github.com/RezaAramjou/portfolio.git
git clone https://github.com/RezaAramjou/labs.git
git clone https://github.com/RezaAramjou/pentest.git
git clone https://github.com/RezaAramjou/siem-lab.git
```

### Step 2: Set Up the Target Environment (Ubuntu Server VM)

1.  Create a new Ubuntu Server VM in VirtualBox.
2.  Install Docker and Docker Compose.
3.  Use the Docker Compose file in the `labs` repository to start the
    Juice Shop application.
    `bash     # From the 'labs' repo on the Target VM     docker-compose -f docker/juice-shop/docker-compose.yml up -d`
4.  Configure `auditd` for host-level logging as per the Day 1 plan.

### Step 3: Set Up the Attacker Environment (Kali VM)

1.  Create a Kali Linux VM in VirtualBox.
2.  Configure two network adapters: one **NAT** (for internet) and one
    **Host-Only** (to connect to the Target VM).

### Step 4: Run the Red + Blue Team Exercises

1.  Follow the daily procedures in the 30-day plan, using the Kali VM
    for attacks.
2.  Document all findings in the `pentest` repo and all detections in
    the `siem-lab` repo from your Main OS.

------------------------------------------------------------------------

## 4. Threat Model

A threat model was developed for the environment using the **STRIDE**
framework.
     -------------------------------------------------------------------
| Threat Category | Description | Scenario for This Project |
| :--- | :--- | :--- |
| **S**poofing | An attacker illegitimately assumes the identity of another user. | An attacker could steal a valid session token (JWT) via a Cross-Site Scripting (XSS) vulnerability and use it to impersonate a logged-in user. |
| **T**ampering | An attacker modifies data on the system. | An attacker exploits a file upload vulnerability to upload a malicious script to the `/ftp` directory, altering the web server's content. |
| **R**epudiation | An attacker performs malicious actions in a way that cannot be traced back to them. | Without proper host-level logging (`auditd`), an attacker who gains root access could install a rootkit and erase their command history. |
| **I**nformation Disclosure | An attacker gains access to sensitive or private information. | An attacker exploits an Insecure Direct Object Reference (IDOR) in the basket API to view the contents of other users' shopping carts. |
| **D**enial of Service | An attacker makes a system or service unavailable to legitimate users. | An aggressive directory scan using a tool like `gobuster` could overwhelm the Node.js process, causing the application to crash and become temporarily unavailable. |
| **E**levation of Privilege | An attacker with limited user access gains higher-level permissions. | An attacker with a low-privilege shell on the Ubuntu VM could exploit a misconfigured `sudo` rule to execute commands as the root user. |
     -------------------------------------------------------------------

------------------------------------------------------------------------

## 5. Detection & Hardening Plan

Instead of fixing source code, this project focused on detecting and
responding to threats. The following are examples of detections
developed during the project.

### 5.1. Web Reconnaissance (Directory Enumeration)

-   **Threat**: An attacker uses a tool like `gobuster` to discover
    hidden directories and API endpoints.
-   **Detection**: A SIEM rule was developed to detect a high frequency
    of requests to varied URLs from a single source IP. The rule is
    designed to be SIEM-agnostic using a Sigma-like format.
-   **Evidence**:
    -   **Detection Rule**:
        [siem-lab/rules/web-dirbusting.yml](https://github.com/RezaAramjou/siem-lab/blob/main/rules/web-dirbusting.yml)
    -   **Test Plan**:
        [pentest/web/test-catalog.md](https://github.com/RezaAramjou/pentest/blob/main/web/test-catalog.md)

### 5.2. Insecure File Uploads

-   **Threat**: An attacker uploads a web shell or other malicious
    script disguised as an image file.
-   **Detection**: A rule was created to alert on two conditions: 1) A
    file is uploaded with a dangerous extension (e.g., `.php`,
    `.sh`). 2) The file's extension (e.g., `.jpg`) does not match its
    actual content (MIME type).
-   **Evidence**:
    -   **Detection Rule**:
        [siem-lab/rules/suspicious-file-upload.yml](https://github.com/RezaAramjou/siem-lab/blob/main/rules/suspicious-file-upload.yml)

### 5.3. Host-Level Privilege Escalation

-   **Threat**: An attacker on the host enumerates SUID binaries or
    abuses `sudo` privileges to gain root access.
-   **Detection**: Detections were created to monitor for abnormal
    `sudo` command patterns and suspicious process executions
    originating from common enumeration scripts.
-   **Evidence**:
    -   **Detection Rule**:
        [siem-lab/rules/linux-sudo-anomaly.yml](https://github.com/RezaAramjou/siem-lab/blob/main/rules/linux-sudo-anomaly.yml)
    -   **Pentest Notes**:
        [pentest/linux/privesc-methods.md](https://github.com/RezaAramjou/pentest/blob/main/linux/privesc-methods.md)
