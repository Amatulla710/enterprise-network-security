# Security Testing Results

This document records the connectivity and basic security validation performed in Cisco Packet Tracer.

## Test results

| # | Source | Destination / action | Expected behaviour | Result |
|---:|---|---|---|---|
| 1 | Employee workstation | Internal DNS server (`192.168.10.12`) | Allow | Passed |
| 2 | Employee workstation | DMZ website using private address (`192.168.30.10`) | Allow | Passed |
| 3 | Employee workstation | Simulated Internet server (`198.51.100.10`) | Allow | Passed |
| 4 | External test host | Public web address (`203.0.113.3`), HTTP | Allow | Passed |
| 5 | External test host | Employee network | Block | Passed |
| 6 | DMZ web server | Employee network | Block | Passed |
| 7 | External test host | Internal DNS/server network | Block | Passed |

## Observations

- The internal DNS record `www.mycompany.com` resolves to the DMZ server's private address, `192.168.30.10`.
- Employee workstations access the DMZ website using the private address.
- External users access the website using the static NAT address, `203.0.113.3`.
- Hairpin/U-turn NAT is not configured; therefore, internal clients should not use the public mapped address to reach the same server.
- The ASA performs Dynamic PAT for Inside-to-Outside traffic and Static NAT for the DMZ web server.
- Packet Tracer Simulation Mode was used to inspect traffic flow through the ASA and to observe blocked traffic.

## Scope and limitations

These results describe tests performed in the Packet Tracer simulation. They are not a production penetration test or a security certification. ICMP timeouts alone were not treated as proof of a firewall block; packet handling was also inspected in Simulation Mode.
