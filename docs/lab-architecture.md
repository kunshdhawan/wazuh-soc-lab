# Lab Architecture

## Goal

Build a home SOC environment for learning:

- Security Monitoring
- Log Analysis
- Alert Investigation
- Incident Response

## Components

### Wazuh Server
Central SIEM platform.

### Monitored Endpoint
Ubuntu system running Wazuh Agent.

### Attacker Machine
Kali Linux used to generate test activity.

## Planned Scenarios

1. Failed Login Attempts
2. Brute Force Activity
3. Reconnaissance Scanning
4. File Integrity Monitoring Alerts
5. Suspicious Authentication Events