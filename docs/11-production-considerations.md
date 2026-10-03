# 11 — Production Considerations

[Portfolio overview](../README.md) · [Evidence matrix](12-evidence-matrix.md)

The configurations reflect CCNA educational requirements and available laboratory equipment. The equivalents below describe a future production design discussion; **they were not implemented in this repository**, and the lab configuration has been preserved.

| Laboratory setting / observed evidence | Modern production consideration |
|---|---|
| Community-based SNMP read-only configuration; lab specifies SNMPv2c | SNMPv3 with authentication/privacy, source restrictions and monitored access |
| IKEv1, PSKs, AES-128, SHA-HMAC and DH group 5 | A current, platform-supported IKEv2/IPsec policy, stronger key exchange and lifecycle-managed authentication |
| Shared local lab access and enable credentials in group variables | Centralized AAA with individual identities, scoped authorization and secrets management (for example an external secret store or Ansible Vault) |
| Disabled SSH host-key checking and legacy SSH compatibility sample | Validated host keys, supported modern algorithms and predictable transport configuration |
| Legacy IOS/router platforms and unspecified wireless models | Supported platform/software lifecycle and capability checks before selecting production equivalents |
| Static EtherChannel `mode on` | Negotiated bundling such as LACP where supported, plus operational monitoring of members |
| HSRP/STP role alignment without exported HSRP tracking | Define failure domains, validate convergence and consider tracked upstream reachability |
| Static Ethernet exit-only defaults | Explicit, validated upstream next-hop design appropriate to the carrier/underlay |
| Broad PAT and no evidenced guest/voice interface policy | Explicit least-privilege inter-segment/edge policy with positive and negative tests |
| HTTP/HTTPS management and published TCP ports to the DHCP router | Deliberate management-plane exposure, encrypted management and scoped access paths |
| Console-only test results; versioned lab exports without full execution logs | Retained test results, reproducible collection metadata, restoration procedures and an intentional publication/retention policy |
| Single-address monitoring references | Monitoring ownership, alerting, telemetry integrity and time-synchronization validation |

IPv6 security and routing deserve independent verification rather than inheriting assumptions from IPv4. Management ACL ranges should be compared with the actual subnet plan, particularly the broad branch `/24` declarations.

The main engineering outcome is transferable: preserve intended topology, define controls precisely, and demonstrate behavior with reproducible evidence. Production alternatives are an evolution path, not retroactive claims about this capstone.
