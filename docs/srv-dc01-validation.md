# SRV-DC01 External Validation

## Objective

Verify the network identity and externally reachable services of `SRV-DC01` without changing the guest operating system or using guest credentials.

## Validation scope

- Validation date: 2026-08-16
- VMware network: VMnet1
- Observed address: `192.168.75.10`
- Observed hostname: `SRV-DC01`
- Observed NetBIOS domain name: `LAB`
- Method: host-side connectivity and service-port validation

## Results

| Service | Port | Result |
| --- | ---: | --- |
| DNS | 53 | Reachable |
| Kerberos | 88 | Reachable |
| RPC Endpoint Mapper | 135 | Reachable |
| NetBIOS Session Service | 139 | Reachable |
| LDAP | 389 | Reachable |
| SMB | 445 | Reachable |
| Kerberos password service | 464 | Reachable |
| LDAPS | 636 | Reachable |
| Global Catalog | 3268 | Reachable |
| Global Catalog over TLS | 3269 | Reachable |
| WinRM | 5985 | Reachable |
| Remote Desktop | 3389 | Not reachable during validation |

The server responded to ICMP with local laboratory latency. Reverse DNS returned `SRV-DC01`. NetBIOS registrations included the `LAB` group and domain-controller registration types.

## Analyst assessment

The observed identity and service combination is consistent with an active Windows domain controller providing DNS and Active Directory services in the private lab.

## Evidence boundaries

This was an external, unauthenticated validation. It does not prove the installed Windows role list, directory object configuration, Group Policy, audit policy, privileged-group membership, replication health, or Wazuh event collection.

No directory change, authentication attempt, group-membership change, detection simulation, or configuration change was performed.

## Next step

Perform an authenticated, read-only review of installed roles and audit policy. Only then run an authorized privileged-group membership scenario and validate the resulting event in Wazuh.

## Privacy

The evidence excludes credentials, user accounts, hardware addresses, and production information. All addresses belong to the isolated laboratory network.
