# Integrating Auditd with Wazuh

## Overview

The default Wazuh deployment was collecting Linux `journald` and system logs, providing basic visibility into authentication and sudo events. To improve endpoint telemetry, `auditd` was integrated with Wazuh to collect Linux audit events.

## Installing Auditd

```bash
sudo apt update
sudo apt install auditd audispd-plugins -y
```

Verify the service is running:

```bash
sudo systemctl status auditd
```

## Configuring Wazuh

Edit the Wazuh configuration file:

```bash
sudo nano /var/ossec/etc/ossec.conf
```

Add the following log collector entry:

```xml
<localfile>
  <log_format>audit</log_format>
  <location>/var/log/audit/audit.log</location>
</localfile>
```

Restart the Wazuh manager:

```bash
sudo systemctl restart wazuh-manager
```

## Verification

Confirm Wazuh is monitoring the audit log:

```bash
sudo grep -i "audit" /var/ossec/logs/ossec.log
```

Expected output:

```text
Analyzing file: '/var/log/audit/audit.log'
```

## Results

After integration, Wazuh was able to collect additional audit-related telemetry, including:

* Source user (`data.srcuser`)
* Destination user (`data.dstuser`)
* Executed commands (`data.command`)
* Audit event fields (`data.audit.*`)

This improved the visibility of privilege escalation and command execution activities within the SOC lab environment.
