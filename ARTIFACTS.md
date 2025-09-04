# Week 3 Artifacts: Red/Blue Team Sprint

This document summarizes the key artifacts and deliverables from the Week 3 security sprint. The work was conducted in private repositories to simulate a real-world engagement.

---

## 1. Penetration Testing (`pentest` repo)

A penetration test was performed against the OWASP Juice Shop application.

* **Final Report**: [juice-shop-report.md](https://github.com/RezaAramjou/pentest/blob/main/reports/juice-shop-report.md)
    * **Summary**: A professional report detailing the scope, methodology, and findings of the test.
    * **Key Findings**: Critical SQL Injection (Authentication Bypass) and High-risk Stored Cross-Site Scripting (XSS).

* **Proof of Concept Evidence**: [attack-log-replay.md](https://github.com/RezaAramjou/pentest/blob/main/poc/attack-log-replay.md)
    * **Summary**: A timeline document connecting the red team attack actions to the blue team detection events.

---

## 2. SIEM & Detection Engineering (`siem-lab` repo)

A Splunk SIEM instance was set up to ingest, monitor, and alert on application logs.

* **Detection Rule**: [suspicious-web-sqli.yml](https://github.com/RezaAramjou/siem-lab/blob/main/rules/suspicious-web-sqli.yml)
    * **Summary**: A documented detection rule (written as a Splunk Alert) to identify successful authentication bypasses via SQL injection.

* **Log Ingestion Script**: [load-logs.sh](https://github.com/RezaAramjou/siem-lab/blob/main/elk/load-logs.sh)
    * **Summary**: A shell script created to stream logs from the target Docker container to the SIEM.

* **Evidence Screenshot**: [splunk-ingestion-success.png](https://github.com/RezaAramjou/siem-lab/blob/main/samples/splunk-ingestion-success.png)
    * **Summary**: A screenshot showing logs from the target application successfully ingested and indexed in Splunk.
