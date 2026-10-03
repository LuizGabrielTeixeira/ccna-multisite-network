# 07 — Network security

[Portfolio overview](../README.md) · [Evidence matrix](12-evidence-matrix.md)

## Access-layer protection

| Control | Final scope | Engineering purpose / evidence limit |
|---|---|---|
| DHCP snooping | SW1-Zg/SW2-Zg VLANs 5–7,10,20,30,40,50,60; SW1-Pl/SW1-St VLANs 30,50,60 | Restricts server responses to trusted paths and learns bindings. Infrastructure trunks are trusted; many user ports have rate limit 5. No binding table captured. |
| Dynamic ARP Inspection | Zagreb access switches for the same VLAN list; Split VLAN 30 only | Validates ARP against DHCP snooping bindings. No DAI enablement evidenced on Pula or the MLS pair; platform class-map names on MLS are not DAI/snooping enable commands. |
| Port-security | Many user/server access ports on all four access switches | Maximum 5 MACs and 5-minute inactivity aging; sticky learning on Zagreb, not branch access blocks. No violation counters retained. |
| PortFast / BPDU Guard | Many access ports | Host activation and protection against unexpected BPDUs; configuration only, no event evidence. |
| Unused-port shutdown | VLAN 99 ranges and numerous functional-VLAN ports | Reduces available attachment points. Empty uplink blocks and some unshutdown ports prevent an all-ports-hardened claim. |

Sources: final [SW1-Zg](../playbooks/backups/SW1-Zg_2026-02-12_20-20-51.txt), [SW2-Zg](../playbooks/backups/SW2-Zg_2026-02-12_20-20-51.txt), [SW1-Pl](../playbooks/backups/SW1-Pl_2026-02-12_20-20-50.txt) and [SW1-St](../playbooks/backups/SW1-St_2026-02-12_20-20-51.txt).

Trusted ports include Zagreb server-facing ports, both core uplinks and AP/WLC trunks. SW1-Zg Fa0/2 (`SRV-1`) is trusted for DHCP and DAI as well as Fa0/1 (`SRV-DHCP`). This is broader trust than the DHCP router alone; the configuration must be documented as observed. Static clients on untrusted DAI ports would require binding/ARP-policy evidence; none is retained.

## Management access

Device exports include local user authentication, password encryption, login blocking and SSH transport configuration. Routed devices and MLS exports explicitly use `no aaa new-model`; centralized AAA is not evidenced. SSHv2 is explicitly selected on RT1-St; other exports should not be described as uniformly explicit SSHv2 configurations.

Most devices set `login local`, `transport input ssh` and `exec-timeout 0 30` across VTY 0–15. **SW1-St differs:** only VTY 0–2 has that complete configuration; VTY 3–4 and 5–15 show `login` alone. Their defaults and access behavior require review. No latest device export has a VTY `access-class ACL_SSH in`.

HTTP/HTTPS servers are enabled on DHCP-SRV and switch exports, while the three site routers disable them. SSH-only VTY settings do not disable these separate management services.

## Required policy versus observed implementation

| Lab policy | Repository evidence | Conclusion |
|---|---|---|
| Guests may access Internet only | Guest gateways/pools and NAT eligibility; no interface policy ACL application | Required by lab but not evidenced |
| Voice may not access Internet | Zagreb VLAN 40 and voice port assignments; NAT ACL permits broad 172.20/16 | Required by lab but not evidenced |
| SNMP only from monitoring server | [acl.yml](../playbooks/acl.yml) defines ACL_SNMP for 172.20.7.70 and binds community | Automation exists; latest exports have unbound read-only communities |
| SSH only from ADMIN and STAFF | acl.yml defines ACL_SSH and applies it to VTY 0–15 | Automation exists; restriction absent from latest exports |
| Protected site tunnels | Peer-matched GRE selectors, crypto maps and IPsec transforms | Configured, but SA establishment/traffic encryption unverified |

The ACL_SSH playbook permits `/24` source ranges `172.20.5.0`, `172.20.4.0`, `172.20.9.0`, `172.20.10.0`, `172.20.12.0` and `172.20.13.0`. The Zagreb ranges match administration/staff. At Pula, `172.20.9.0/24` is configured wireless, and `172.20.10.0/24` includes the staff `/25` plus a shutdown loopback subnet. At Split, `172.20.12.0/24` includes staff and wireless; `172.20.13.0/24` includes guest, AP, management and shutdown loopback ranges. Thus the automation's source policy is broader than its ADMIN/STAFF comments suggest.

[config-monitor.yml](../playbooks/config-monitor.yml) declares an unrestricted SNMP community, while acl.yml removes it and declares an ACL-bound version. Execution order matters; retained exports show the unrestricted form, but no logs establish playbook order or execution. No data-plane `ip access-group` is exported; crypto selectors and NAT ACL 1 must not be presented as enforcing user isolation.

Modern equivalents are described neutrally in [Production Considerations](11-production-considerations.md). The [manual-review register](10-validation-and-testing.md#manual-review-register) records final-state discrepancies without changing them.
