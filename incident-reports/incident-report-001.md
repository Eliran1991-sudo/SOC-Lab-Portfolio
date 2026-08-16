# Incident Report 001: Failed Windows Logon Detection

## Executive summary

Wazuh detected repeated failed logon attempts on the isolated `WIN11-CLIENT` endpoint. The events were generated during an authorized access-validation test and were correctly collected, decoded, and correlated by the SIEM.

## Event details

| Field | Value |
|---|---|
| Endpoint | WIN11-CLIENT |
| Endpoint IP | 192.168.75.132 |
| Wazuh agent | 001, version 4.14.7 |
| Windows event ID | 4625 |
| Wazuh rule ID | 60122 |
| Severity | Level 5 |
| Event channel | Security |
| Result | Authentication failure |
| Cause | Unknown username or incorrect password |
| Caller process | VMware Tools (`vmtoolsd.exe`) |

## Investigation

The alert timeline showed several authentication failures with different Windows logon types in a short period. The originating process was VMware Tools on the monitored endpoint. This matched the authorized attempt to validate remote guest access from the VMware host.

Additional telemetry confirmed that:

- The Wazuh agent remained active throughout the test.
- The endpoint continued sending keep-alive messages.
- File Integrity Monitoring completed successfully.
- Normal Windows process creation events continued after the alert.
- No malware, persistence, lateral movement, or data exfiltration was observed.

## MITRE ATT&CK review

Wazuh associated the rule with `T1531 - Account Access Removal`. For this specific event, the behavior is more accurately treated as failed authentication activity rather than confirmed account-access removal. This highlights the need for analyst validation instead of relying only on an automatic framework mapping.

## Classification

- Detection quality: True positive
- Activity type: Authorized lab test
- Security impact: None
- Escalation required: No
- Recommended action: Document and close

## Lessons learned

The test proved the complete detection pipeline from Windows Security Event Log through the Wazuh agent, manager, indexer, and alert output. It also demonstrated why SOC analysts must validate event context, process lineage, and business authorization before escalating an alert.

