# IP Addressing Plan

This document records the IPv4 addressing used in the Cisco Packet Tracer enterprise network lab.

## Inside network

- Subnet: `192.168.10.0/24`
- ASA Inside gateway: `192.168.10.1`

| Device | IP address | Default gateway | Address method |
|---|---|---|---|
| ASA Inside (VLAN 1) | `192.168.10.1` | N/A | Static |
| PC0 | `192.168.10.100–192.168.10.131` pool | `192.168.10.1` | DHCP |
| PC1 | `192.168.10.100–192.168.10.131` pool | `192.168.10.1` | DHCP |
| Server0 (DNS) | `192.168.10.12` | `192.168.10.1` | Static |

The DHCP pool is configured on the ASA for the Inside interface. The DNS option provided to clients is `192.168.10.12`.

## DMZ network

- Subnet: `192.168.30.0/24`
- ASA DMZ gateway: `192.168.30.1`

| Device | IP address | Default gateway | Address method |
|---|---|---|---|
| ASA DMZ (VLAN 3) | `192.168.30.1` | N/A | Static |
| Server1 (HTTP web server) | `192.168.30.10` | `192.168.30.1` | Static |

## Outside network

- Subnet: `203.0.113.0/29`

| Device | Interface | IP address |
|---|---|---|
| Router | GigabitEthernet0/0 | `203.0.113.1` |
| ASA | Outside (VLAN 2) | `203.0.113.2` |
| DMZ web server public NAT mapping | Static NAT | `203.0.113.3` |

## Simulated Internet network

- Subnet: `198.51.100.0/24`

| Device | Interface | IP address | Default gateway |
|---|---|---|---|
| Router | GigabitEthernet0/1 | `198.51.100.1` | N/A |
| Server2 (external test host) | FastEthernet0 | `198.51.100.10` | `198.51.100.1` |

## Addressing notes

- PC0 and PC1 obtain addresses dynamically from the ASA's Inside DHCP pool.
- Server0 and Server1 use static addresses so that DNS and NAT references remain stable.
- Internal users access the web server using `192.168.30.10`; external users use the mapped public address `203.0.113.3`.
- Hairpin/U-turn NAT is not configured in this lab.
