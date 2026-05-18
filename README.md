# DFIR - Web Server Breach Investigation

This project is a controlled DFIR (Digital Forensics & Incident Response) laboratory designed to simulate a full web-based attack lifecycle and analyze it using centralized logging, file integrity monitoring, and SIEM correlation.

The environment is built around an Nginx web server, a custom PHP-based application, and the Wazuh SIEM platform for real-time detection and forensic analysis.

---

# Objective

To simulate and analyze a complete intrusion chain from initial reconnaissance to system-level escalation, while generating forensic artifacts across web, system, and authentication layers.

---

# Architecture Overview

- Nginx Web Server (Application Layer)
- Custom PHP & HTML Web Application
- Linux Ubuntu Host (System Layer)
- Wazuh Agent + SIEM Manager (Detection Layer)
- Centralized log collection and correlation

---

# Attack Lifecycle Summary

## Phase 1: Reconnaissance
External probing activity was observed against the web server, generating repeated 404 errors and directory enumeration patterns. These events were captured through Nginx error logs and flagged by SIEM correlation rules as potential scanning behavior.

---

## Phase 2: Initial Access
A vulnerability in the file upload mechanism allowed unauthorized file placement within the web directory. The event was immediately detected by Wazuh File Integrity Monitoring (FIM), which recorded file creation, ownership, and cryptographic hash artifacts.

VirusTotal analysis of the extracted SHA256 hash confirmed malicious characteristics, validating the integrity alert as a true positive compromise indicator.

---

## Phase 3: Command Execution
Post-compromise activity was identified through abnormal HTTP requests containing execution-like parameters. Nginx access logs captured structured query patterns consistent with system command interaction attempts, enabling full forensic reconstruction of attacker behavior.

---

## Phase 4: Escalation
The attacker transitioned from web interaction to system-level authentication probing via SSH. Multiple invalid login attempts were detected and correlated with earlier web activity, confirming a progression toward lateral movement and privilege escalation attempts.

---

# Key Security Insights

- File Integrity Monitoring is critical for detecting initial foothold establishment
- Web logs provide high-fidelity visibility into attacker intent
- Cross-log correlation enables full attack chain reconstruction
- External threat intelligence (VirusTotal) strengthens SIEM validation
- Single IP correlation across layers confirms unified attack sequence

---

# Tools Used

- Nginx (Web Server Logging)
- PHP (Custom Application Layer)
- Wazuh SIEM (Detection & Correlation)
- Linux Auth Logs (System Monitoring)
- VirusTotal (Threat Intelligence Validation)

---

# Outcome

This simulation demonstrates how a seemingly simple web application compromise can escalate into system-level intrusion attempts. The environment successfully captures the full lifecycle of an attack, enabling end-to-end DFIR analysis, alert correlation, and forensic investigation.

---

