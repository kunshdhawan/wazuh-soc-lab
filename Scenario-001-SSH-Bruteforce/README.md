# Scenario 001: SSH Brute Force Detection

## Objective

Simulate an SSH brute force attack from a Kali Linux attacker machine against an Ubuntu target monitored by Wazuh and validate detection, alert generation, and investigation workflows.

## Lab Architecture

* Attacker: Kali Linux VM (192.168.2.132)
* Target: Ubuntu Server VM (192.168.2.134)
* SIEM: Wazuh Manager + Dashboard
* Log Sources:

  * SSH Authentication Logs
  * System Logs (syslog/journald)
  * Auditd

## Attack Simulation

The attacker attempted multiple SSH logins against the Ubuntu server using a non-existent user account.

Example command: ssh user@192.168.2.134

sMultiple incorrect passwords were supplied to generate failed authentication events.

## Detection Results

### Rule 5710

Description:

* sshd: Attempt to login using a non-existent user
* Severity: Level 5
* Observed Fields:

    * Source IP: 192.168.2.132
    * Username: user
    * Agent: ubuntu

### Rule 5503

Description:

* PAM: User login failed
* Severity: Level 5
* Purpose: Detected failed authentication attempts through the PAM authentication subsystem.

### Rule 2502

Description:

* syslog: User missed the password more than one time
* Severity: Level 10
* Purpose: Correlation rule triggered after multiple authentication failures were observed.

## Investigation

The Wazuh Threat Hunting dashboard was used to investigate generated alerts.

Key findings:

* Multiple failed SSH login attempts were detected.
* The attack originated from Kali Linux (192.168.2.132).
* A non-existent account was targeted.
* Wazuh successfully correlated repeated failures into a higher-severity alert.

## MITRE ATT&CK Mapping

Technique ID: T1110
Technique Name: Brute Force
Tactic: Credential Access

## Outcome

The simulated SSH brute force attack was successfully detected by Wazuh.

Evidence collected included:

* Source IP address
* Target username
* Failed authentication events
* Correlated brute-force alert

This scenario validated the visibility of authentication-related attacks and demonstrated the effectiveness of Wazuh's detection and correlation capabilities within the SOC lab environment.
