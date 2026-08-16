# Detection Rules

This directory indexes detection logic that is supported by published evidence.

| Rule | Purpose | Implementation |
| --- | --- | --- |
| Wazuh `60122` | Detect Windows logon failure events, including Security Event ID `4625` | Built-in Wazuh rule validated in [Incident Report 001](../incident-reports/incident-report-001.md) |
| Wazuh `67027` | Identify Windows process creation events associated with Event ID `4688` | Built-in Wazuh rule recorded in the [validation summary](../evidence/validation-summary.txt) |
| Custom Wazuh `100100` | Detect the authorized PowerShell simulation from Sysmon Event ID `1` | Implemented and validated in the [Attack-to-Detection Wazuh Lab](https://github.com/Eliran1991-sudo/Attack-to-Detection-Wazuh-Lab/blob/main/config/wazuh-local-rules.xml) |

Custom rule `100100` is not duplicated in this repository. The linked advanced project contains the rule source, installation procedure, validation result, and incident analysis.

No additional local rule is claimed until its configuration and real alert evidence are published.
