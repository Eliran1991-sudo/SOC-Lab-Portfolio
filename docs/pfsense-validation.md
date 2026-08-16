# PFSENSE01 External Validation

## Objective

Verify the VMware interface assignments, observed addresses, and externally reachable management services of `PFSENSE01` without logging in or changing the firewall configuration.

## Validation scope

- Validation date: 2026-08-16
- Virtual hardware: 2 vCPU and 4 GB memory
- VMware guest profile: FreeBSD 14, 64-bit
- Method: VMX review, MAC-to-IP correlation, ARP discovery, TCP service checks, and HTTP response inspection

## Verified interfaces

| Interface role | VMware network | Observed address | Verification |
| --- | --- | --- | --- |
| WAN | VMware NAT, VMnet8 | `192.168.93.128` | Address correlated with the WAN MAC configured in the VMX file |
| LAN | Host-only VMnet1 | `192.168.75.2` | Address correlated with the LAN MAC configured in the VMX file |

Hardware addresses were used locally for correlation and are not published in this document.

## External service validation

| Side | Port | Service | Result |
| --- | ---: | --- | --- |
| LAN | 53/TCP | DNS | Reachable |
| LAN | 80/TCP | HTTP management | Reachable, HTTP `200` |
| LAN | 22/TCP | SSH | Not reachable |
| LAN | 443/TCP | HTTPS management | Not reachable |
| LAN | 8443/TCP | Alternate HTTPS | Not reachable |
| WAN | 22/TCP | SSH | Not reachable |
| WAN | 53/TCP | DNS | Not reachable |
| WAN | 80/TCP | HTTP management | Not reachable |
| WAN | 443/TCP | HTTPS management | Not reachable |
| WAN | 8443/TCP | Alternate HTTPS | Not reachable |

The LAN HTTP response was served by nginx and identified the page title as `pfSense - Login`. No credential was entered and no form was submitted.

## Analyst assessment

The two VMware adapters and their observed addresses match the planned WAN and LAN roles. Management access and DNS were exposed on the tested LAN side, while the tested services were not exposed on the WAN side.

## Evidence boundaries

This was an external, unauthenticated validation. It does not prove the contents of firewall rules, NAT behavior, DHCP configuration, DNS resolver settings, routing tables, aliases, VPN configuration, update state, or administrative accounts.

No interface, route, rule, service, credential, or network setting was changed.

## Next step

Perform an authenticated, read-only review of interface assignments, firewall rules, NAT, DHCP, DNS, routes, and system logs. Publish only sanitized configuration summaries and screenshots captured directly from pfSense.

## Privacy

The document excludes credentials, hardware addresses, public addresses, and production information. All published addresses belong to the local laboratory.
