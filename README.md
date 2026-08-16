# Windows SOC Home Lab with Wazuh


Hands-on Security Operations Center lab built with VMware Workstation, Wazuh, and Windows 11. The project demonstrates endpoint onboarding, Windows event collection, alert validation, and basic incident triage in an isolated virtual network.


## Recruiter quick view


| Area | Demonstrated outcome |
|---|---|
| SIEM operations | Deployed and validated Wazuh manager, indexer, dashboard, and Filebeat |
| Endpoint onboarding | Connected and monitored a Windows 11 endpoint |
| Alert triage | Investigated Windows logon failure Event ID `4625` |
| Evidence handling | Produced a sanitized validation summary and incident report |
| Lab safety | Used an isolated host-only VMware network with no production data |


**Start here:** [Incident Report 001](docs/incident-report-001.md) · [Validation summary](evidence/validation-summary.txt)


## Validated lab evidence


At the recorded validation time on 2026-08-10, the Wazuh manager, indexer, and dashboard were active. Windows agent `001` was registered and reported as active on the private laboratory network.


![Wazuh services and active Windows endpoint](docs/images/wazuh-server-status.png)


The recorded Windows endpoint evidence includes Sysmon process telemetry. Both `Sysmon64` and `WazuhSvc` were configured for automatic startup and were running during collection.


![Windows Sysmon event and security agent status](docs/images/windows-endpoint-evidence.png)


## Lab architecture


```mermaid
flowchart LR
    H[Windows 11 host] --> V[VMware Workstation]
    V -->|VMnet1 192.168.75.0/24| W[WAZUH-SIEM01\nUbuntu Server\n192.168.75.20]
    V -->|VMnet1 192.168.75.0/24| C[WIN11-CLIENT\nWindows 11 Enterprise\n192.168.75.132]
    C -->|Wazuh agent 4.14.7| W
    W --> M[Wazuh Manager]
    W --> I[Wazuh Indexer]
    W --> D[Wazuh Dashboard]
```


## Components


| Component | Platform | Purpose |
|---|---|---|
| WAZUH-SIEM01 | Ubuntu Server 24.04 LTS | Wazuh manager, indexer, dashboard, and Filebeat |
| WIN11-CLIENT | Windows 11 Enterprise Evaluation | Monitored endpoint with Wazuh agent |
| VMnet1 | Host-only virtual network | Isolated communication between lab systems |


## Lab inventory status

| Component | Status |
| --- | --- |
| WAZUH-SIEM01 | Verified and documented |
| WIN11-CLIENT | Verified and documented |
| KALI01 | Documented in the Attack-to-Detection Wazuh Lab |
| SRV-DC01 | VM present with VMnet1 assigned; internal configuration not yet documented |
| PFSENSE01 | VM present with NAT and VMnet1 assigned; internal configuration not yet documented |

See [SOC Lab Inventory](docs/lab-inventory.md) for verified platform, network, and evidence boundaries.

## Status recorded during validation


- Wazuh Manager 4.14.7: active
- Wazuh Indexer 4.14.7: active
- Wazuh Dashboard 4.14.7: active
- Filebeat: active
- Windows endpoint agent ID `001`: active
- Dashboard HTTPS endpoint: reachable
- File Integrity Monitoring scan: completed successfully
- Windows Security events: received and analyzed


## Detection scenario: failed Windows logon


A controlled invalid guest-login attempt was performed against `WIN11-CLIENT`. Windows generated Security Event ID `4625`, which the Wazuh agent forwarded to the manager.

## Related projects

- [Attack-to-Detection Wazuh Lab](https://github.com/Eliran1991-sudo/Attack-to-Detection-Wazuh-Lab): extends this foundation with Sysmon telemetry, controlled Kali reconnaissance, a custom Wazuh rule, MITRE ATT&CK mapping, and deeper incident analysis.
- [Incident Report Template](docs/incident-report-template.md): reusable structure for future evidence-based investigations.
