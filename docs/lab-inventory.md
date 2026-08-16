# SOC Lab Inventory

This document records the current VMware lab inventory and separates verified evidence from components whose internal configuration has not yet been documented.

## Status definitions

| Status | Meaning |
| --- | --- |
| Verified and documented | The component is represented by published technical evidence or investigation notes. |
| Present with network assigned | The virtual machine and its VMware network assignment were verified, but its internal services have not yet been documented. |

## Current inventory

| Component | Platform | Network | Role | Documentation status |
| --- | --- | --- | --- | --- |
| WAZUH-SIEM01 | Ubuntu Server 24.04 LTS | VMnet1 | Wazuh manager, indexer, dashboard, and Filebeat | Verified and documented |
| WIN11-CLIENT | Windows 11 Enterprise Evaluation | VMnet1 | Monitored endpoint with Wazuh agent, Sysmon, and Windows Event Logs | Verified and documented |
| KALI01 | Kali Linux | VMnet1 | Authorized reconnaissance source for controlled lab simulations | Documented in the Attack-to-Detection Wazuh Lab |
| SRV-DC01 | Windows Server virtual machine | VMnet1 | Active Directory and Windows Server laboratory role | External network services verified. Authenticated internal role configuration is not yet documented |
| PFSENSE01 | pfSense virtual machine based on FreeBSD 14 | NAT and VMnet1 | Firewall and routing laboratory system | Present with network assigned. Internal firewall configuration is not yet documented |

## Verified virtual hardware

| Component | vCPU | Memory | Verified network adapters |
| --- | ---: | ---: | --- |
| SRV-DC01 | 4 | 4 GB | VMnet1 |
| PFSENSE01 | 2 | 4 GB | NAT and VMnet1 |

The inventory above was verified from the local VMware configuration on 2026-08-16. No virtual machine was started during verification.

## Evidence boundaries

Published evidence currently covers Wazuh services, the Windows endpoint, failed-logon analysis, Sysmon telemetry, custom Wazuh detection, and controlled Kali reconnaissance.

SRV-DC01 network identity and externally reachable DNS, Kerberos, LDAP, LDAPS, Global Catalog, SMB, and WinRM services were verified on 2026-08-16. This evidence is consistent with an active domain controller, but installed-role enumeration, directory objects, audit policy, and event collection still require authenticated review.

The existence and VMware network assignments of PFSENSE01 are verified. Its internal firewall rules and routing behavior are not claimed as validated until separate evidence is collected and published.

## Related documentation

- [Windows SOC Home Lab README](../README.md)
- [Incident Report 001](../incident-reports/incident-report-001.md)
- [SRV-DC01 External Validation](srv-dc01-validation.md)
- [Attack-to-Detection Wazuh Lab](https://github.com/Eliran1991-sudo/Attack-to-Detection-Wazuh-Lab)

## Privacy

This document does not include passwords, keys, personal addresses, production information, or local host filesystem paths. All network references describe the isolated laboratory environment.
