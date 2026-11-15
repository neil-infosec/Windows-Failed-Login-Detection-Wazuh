# SOC Incident Investigation Report
## Windows Failed Login Detection Using Wazuh SIEM

**Investigation Date:** 14 November 2026  
**Project Type:** Beginner SOC Analyst Home Lab  
**Status:** Completed

---

### 1. Objective

The objective of this investigation was to generate a controlled Windows failed-login event, collect it using the Wazuh agent, and investigate the resulting security alert through the Wazuh dashboard.

### 2. Lab Environment

| Component | Configuration |
|---|---|
| Host Operating System | Windows 11 |
| SIEM Platform | Wazuh |
| SIEM Server | Ubuntu 24.04 LTS VM |
| Endpoint | Windows-SOC |
| Endpoint Agent ID | 001 |
| Log Source | Windows Security Event Log |

### 3. Detection Details

A failed login attempt was intentionally generated on the Windows endpoint by entering an incorrect password.

The following Windows Security Event was recorded:

| Field | Observed Value |
|---|---|
| Windows Event ID | 4625 |
| Event Description | An account failed to log on |
| Account | [REDACTED] |
| Logon Type | 2 – Interactive |
| Failure Reason | Unknown user name or bad password |
| Status | 0xC000006D |
| Substatus | 0xC000006A |
| Source Network Address | 127.0.0.1 |
| Authentication Package | Negotiate |
| Process | svchost.exe |

### 4. Wazuh Alert Analysis

The Windows event was successfully collected by the Wazuh agent and appeared in the Wazuh Threat Hunting section.

**Observed Wazuh alert details:**

- Agent Name: Windows-SOC
- Agent ID: 001
- Rule ID: 60122
- Rule Level: 5
- Windows Event ID: 4625
- Target Account: [REDACTED]
- Logon Type: 2

### 5. Investigation and Findings

1. A controlled failed-login attempt was generated on the Windows endpoint.
2. Windows Security Event ID 4625 recorded the failed authentication.
3. The Wazuh agent successfully forwarded the event to the SIEM.
4. The event was located in Wazuh Threat Hunting using the query `data.win.system.eventID:4625`.
5. The source address was `127.0.0.1`, indicating a local loopback address rather than evidence of a remote source.
6. The event was consistent with the intentionally generated incorrect-password test.

### 6. Incident Classification

**Classification:** Benign – Controlled Lab Activity

**Severity:** Low – Wazuh Rule Level 5

**Conclusion:** The event was generated intentionally for testing. There was no evidence in this single event of an external attack or unauthorized remote access.

### 7. Conclusion

This exercise demonstrated the process of detecting and investigating a Windows failed-login event using Wazuh SIEM.

The investigation covered Windows Event Viewer, Security Event ID 4625, Wazuh agent log collection, Threat Hunting, and basic alert analysis.

This project represents a beginner-level hands-on SOC investigation conducted in a controlled home lab.

### 8. Skills Practiced

- Windows Security Event Log analysis
- Failed-login detection
- Wazuh SIEM monitoring
- Event ID 4625 investigation
- Basic alert triage
- Incident documentation
- Linux and virtual machine lab administration

---

**Disclaimer:** This was a controlled educational lab exercise. It does not represent a real-world security incident.
