# 01 — Project evolution

[Portfolio overview](../README.md) · [Evidence matrix](12-evidence-matrix.md)

## One infrastructure, three stages

The stage descriptions below come from the supplied laboratory context. They establish the intended progression, not proof that each deliverable was completed. Repository exports take precedence over ENSA requirements, then SRWE requirements, then ITN requirements.

| Stage | Intended engineering progression | What the repository establishes |
|---|---|---|
| **1 — ITN** | Three sites, three routers, three access switches and PCs; IPv4/IPv6 planning, hardening, SSH, static routing, ping/traceroute and Wireshark ICMP analysis | Later exports retain site identity, addressing and management foundations. No separately identified ITN exports, packet captures or test reports are present. |
| **2 — SRWE** | Expanded Zagreb core, VLANs/SVIs, EtherChannel, HSRP, STP role distribution, DHCP, access security and centralized wireless | Final exports contain redundant Zagreb SVIs, static EtherChannel, HSRP, STP priorities, DHCP and access protection. Controller/AP configuration, AP groups and FlexConnect are not evidenced. |
| **3 — ENSA** | GRE/IPsec, OSPF, Internet edge, NAT, ACL policy, voice services, monitoring and Ansible | Final exports contain tunnel/IPsec configuration, OSPF, PAT, Zagreb port forwarding, NTP and monitoring references. Playbooks cover backup, tests, save, monitoring and management ACLs. Several lab requirements are absent or only partially represented. |

## What “final” means here

The newest **filename timestamp per inventory alias** is the primary final-state source: four devices at `2026-02-12_20-20-50`, six at `2026-02-12_20-20-51`. All ten configured hostnames append `-222` to their inventory aliases. These are running-config exports, not a synchronized live discovery or an independent startup-config comparison.

The [catalog](12-evidence-matrix.md#snapshot-catalog) lists all 31 retained snapshots. They cover one day in the final-stage lab, not three independently archived stages. Earlier same-day backups must not be relabeled as ITN or SRWE evidence. Five snapshots with filename time `18-39-24` were removed during repository cleanup; none was a device's newest export, so final-state selection is unchanged.

## Observable same-day evolution

- Comparing [MLS1 at 18:13:56](../playbooks/backups/MLS1-Zg_2026-02-12_18-13-56.txt) with [MLS1 at 20:20:51](../playbooks/backups/MLS1-Zg_2026-02-12_20-20-51.txt) shows addition of a read-only SNMP community and updated configuration/NVRAM headers. Routing and SVI blocks persist across that comparison.
- Comparing [RT1-Pl at 18:40:11](../playbooks/backups/RT1-Pl_2026-02-12_18-40-11.txt) with [RT1-Pl at 20:20:50](../playbooks/backups/RT1-Pl_2026-02-12_20-20-50.txt) shows addition of syslog destination and SNMP community plus updated headers. This retained earlier export replaces the removed 18:39:24 source used in the initial analysis.
- These differences are consistent with [monitoring automation](../playbooks/config-monitor.yml), but no execution log proves which method applied the changes.

## Superseded intent and retained configuration

The old inter-site `/30` networks appear on GRE tunnel interfaces in the final state. OSPF replaces the intended static inter-site routing model on the Zagreb–branch paths; static default routes remain, so this is not a static-route-free design. WAN interfaces are static despite the ENSA DHCP requirement. IPv6 LAN configuration remains, but inter-site IPv6 routing is not evidenced.

The final state should be read as an engineering artifact with explicit evidence gaps, not as a checklist claiming full assignment completion.

## Supporting lab imagery

[images/2.jpeg](../images/2.jpeg) illustrates the intended campus/branch layout, including WLC/APs and phones at all three sites. Its stage/date is not explicitly identified. The latest branch configurations lack VLAN 40 gateways and shut down the drawing's Fa0/16 phone ports, so the drawing is contextual design evidence rather than the authoritative final configuration. [images/1.jpeg](../images/1.jpeg) documents the lab workspace; [images/3.jpeg](../images/3.jpeg) records an Ansible recap. These images are included in version control as supporting evidence.
