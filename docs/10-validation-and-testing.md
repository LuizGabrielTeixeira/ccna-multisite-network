# 10 — Validation and testing

[Portfolio overview](../README.md) · [Evidence matrix](12-evidence-matrix.md)

## Evidence levels

| Level | Established here? | Meaning |
|---|---|---|
| Configured | Yes, for explicitly exported commands | A feature appears in the selected latest running-config export |
| Automation exists to test | Yes, for critical-target and inventory IPv4 pings | Playbook code describes a test procedure |
| Historical evidence exists | Yes, for configuration capture, recorded save headers and a photographed Ansible recap | Exports and recap exist; no feature-specific runtime success reports were found |
| Currently live-tested | **No** | No device connections or Ansible runs were performed for this documentation |

**Verified** in the evidence matrix means verified by repository configuration/code, not a working live service. No ping success, OSPF adjacency, IPsec SA, HSRP election, DHCP lease, wireless association, monitoring poll or failover measurement is established by the available files.

## Static relationship checks

| Check | Result from latest exports |
|---|---|
| Inventory address versus interface | All ten inventory connection addresses match final device interfaces |
| Zagreb routed transit endpoints | Reciprocal descriptions and consistent `.193/.194` and `.197/.198` `/30` pairs |
| GRE peer endpoint/subnet pairs | All three tunnel pairs match reciprocal WAN endpoints and `/30` addressing |
| IPsec traffic selectors and peers | Reciprocal GRE selectors, crypto peers and matching per-pair PSK entries; WAN crypto-map application present |
| HSRP gateways | All eight IPv4 VIPs agree across MLS; corresponding IPv6 groups agree |
| HSRP versus STP preference | Aligned VLAN subsets and complementary priorities |
| Core/access trunk lists | Zagreb infrastructure lists/native VLANs match; branch tagged VLANs match router subinterfaces |
| OSPF network selection | Core and Zagreb–branch interfaces match; Pula–Split Tunnel1 omitted at both ends |
| DHCP default gateways | Served IPv4 pools agree with HSRP VIPs or branch gateways |
| Monitoring destinations | All ten final exports reference syslog `.70`; SNMP communities have no ACL bindings |

These checks validate configuration relationships only. Exact physical adjacency, platform defaults and runtime state remain outside that evidence.

## Existing test automation

[test-conn.yml](../playbooks/test-conn.yml) pings three critical IPv4 endpoints from every Cisco device. [full-conn.yml](../playbooks/full-conn.yml) checks directed inventory-to-inventory IPv4 reachability, excluding self. Both print status based on the literal 100% success string, without asserting failure on packet loss or saving reports. No outputs from either playbook are retained.

Stage 1 required ping/traceroute and Wireshark IPv4/IPv6 ICMP analysis, but no evidence of those specific tests is present. Configuration backups and the Ansible recap photograph cannot substitute for those validation artifacts.

### Historical Ansible recap photograph

[images/3.jpeg](../images/3.jpeg) shows a terminal dated Thu Feb 12, 18:43 and a recap covering all ten inventory aliases, with zero reported failures and unreachable hosts. Delegated-localhost messages above the recap are consistent with local backup tasks. The photograph does not expose the playbook invocation, full task list or retained output files, so attribution to a specific run is incomplete. It supports historical automation execution, not successful pings, VPN establishment or save verification. [images/1.jpeg](../images/1.jpeg) shows the workspace and screens, but is not a readable device-by-device validation report.

## Manual-review register

| ID | Observed state | Implication / useful follow-up |
|---|---|---|
| R01 | Branch Tunnel1 `.9/.10` is absent from OSPF selection | Three-pair GRE/IPsec configuration does not establish an OSPF full mesh; capture interface/neighbor/routes |
| R02 | WAN interfaces are static `.77/.78/.79`, not DHCP | Documented final state differs from ENSA requirement; obtain underlay gateway/route evidence |
| R03 | Site defaults point only to Ethernet exit interfaces | Next-hop/proxy-ARP behavior may matter; inspect route/ARP and upstream topology |
| R04 | Named management ACLs/bindings are absent from all latest exports | acl.yml authors the policy but does not prove deployment; obtain later exports and execution logs |
| R05 | ACL_SSH branch `/24`s include wireless and other segments | Comments do not match strict ADMIN/STAFF scope; compare policy intent with actual prefixes before any change |
| R06 | config-monitor declares an unrestricted SNMP community; acl.yml declares a restricted replacement | Playbook ordering can affect effective restriction; collect execution order and final community binding |
| R07 | Access switches use PVST; cores use Rapid PVST | Do not claim uniform rapid convergence; capture STP modes/roles and measured failover |
| R08 | Branch passive declaration names Gi0/1 rather than VLAN subinterfaces | LAN passive-interface intent is not explicitly represented for each subinterface; capture OSPF interface state |
| R09 | DHCP-SRV has DHCPv6 pools but no attachment; MLS has no relay; Pula VLAN 60 pool unattached | Centralized DHCPv6 and guest stateful DHCPv6 cannot be claimed; capture complete server/relay and client evidence |
| R10 | No applied guest/voice policy ACL; broad NAT permit includes those subnets | Guest isolation and voice Internet prohibition are not evidenced; obtain positive/negative client policy tests |
| R11 | SW1-St VTY 3–15 lacks exported local-login/SSH-only settings | Uniform SSH-only management is not established; inspect all effective VTY settings |
| R12 | Stale host aliases: old Zagreb addresses and RT1-St mapped to guest `.193` in some devices | Name-based diagnostics could reach the wrong interface/device; inventory and interfaces are stronger evidence |
| R13 | Trusted DHCP/DAI AP/WLC/server ports include more than the DHCP router; DAI scope varies by site | Protection is not uniform; collect snooping bindings/DAI counters and intended trust boundaries |
| R14 | Empty MLS uplink/Split Gigabit blocks and selected prepared ports are not shutdown | “All unused ports disabled” is unsupported; capture actual port usage before deciding intent |
| R15 | Shutdown branch loopbacks remain addressed and some selected by OSPF | Do not describe them as active service networks |
| R16 | No Zagreb VLAN 5/6/10 DHCPv4 pools despite helpers on those SVIs | Helpers do not prove those segments receive leases; verify static versus dynamic infrastructure addressing |
| R17 | No interface tracking in HSRP configuration | Upstream-path-aware failover is not evidenced; obtain failover behavior under defined scenarios |
| R18 | DHCP domain spelling differs from management domain; RTVi alias shares management VIP `.62` | Treat naming/service identity as unresolved; do not infer a telephony server from host aliases |
| R19 | Initial evidence-publication gap resolved: 31 retained exports are versioned with scoped ignore exceptions; playbooks and images are versioned | Five earlier snapshots were removed, but all ten final-state sources remain; links/catalog checked against retained files |
| R20 | Reference drawing shows branch phones on Fa0/16; final branch switches shut down Fa0/16 in VLAN 99 and routers lack VLAN 40 gateways | Treat drawing as intent/context, not proof of final branch voice implementation |

Sources for each observation are indexed in [12](12-evidence-matrix.md); routing specifics are in [05](05-routing-vpn-and-nat.md), access policy in [07](07-network-security.md), and services in [08](08-network-services-and-monitoring.md). No discrepancy was silently corrected.

## Recommended additional evidence

The following are **future, owner-operated collection suggestions**, not commands executed here. Capture timestamp, device identity, source interface and test outcome with each artifact.

| Area | Useful read-only evidence |
|---|---|
| Physical/logical links | `show cdp neighbors detail` or `show lldp neighbors detail`, `show interfaces status`, `show interfaces trunk`, `show vlan brief` |
| Core resilience | `show etherchannel summary`, `show spanning-tree vlan <id>`, `show standby brief`; measured failover under an agreed lab procedure |
| Routing and IPv6 | `show ip ospf neighbor`, `show ip ospf interface brief`, `show ip route`, `show ipv6 route`; source-qualified IPv4/IPv6 tests |
| VPN and NAT | `show crypto isakmp sa`, `show crypto ipsec sa`, `show ip nat translations`, `show ip nat statistics`; before/after traffic counters |
| DHCP/access protection | `show ip dhcp binding`, `show ip dhcp snooping binding`, `show ip arp inspection`, `show port-security interface <port>`; IPv6 lease/client information |
| Management/services | `show access-lists`, effective VTY configuration, `show ntp associations`/status; server-side SNMP polls/syslog receipts |
| Wireless and voice | WLC/AP configs, joins, WLAN mappings and association tests; telephony config, phone registrations and call tests |
| Automation | Retained Ansible recap/ping outputs, collection versions, invocation directory and backup manifest |

Guest-to-internal denial, allowed guest Internet traffic, voice Internet denial and management-source restrictions need source-specific positive/negative tests. Inventory pings alone cannot validate them.
