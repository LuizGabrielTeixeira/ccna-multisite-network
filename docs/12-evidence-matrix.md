# 12 — Evidence matrix

[Portfolio overview](../README.md) · [Validation and review register](10-validation-and-testing.md)

## Reading the evidence

- **Verified:** directly present in the selected configuration or playbook code; this is not live operational verification.
- **Partially evidenced:** supporting configuration/code exists, but complete implementation or runtime success is not established.
- **Required by lab but not evidenced:** supplied project context specifies it, but the available final configurations/code do not establish it.
- **Not applicable:** not a device/service under evaluation or not a repository-supported role.

Requirements come from the project brief; assignment files are not present. Configuration precedence is newest device export → ENSA → SRWE → ITN. Every latest export was read in full. Older exports were compared selectively for evolution, not substituted for missing final features.

**Availability:** all 31 retained text exports under `playbooks/backups/` are included in version control. Scoped exceptions in [.gitignore](../.gitignore) allow this laboratory evidence while preserving the general `backups/` and `*.txt` ignore rules elsewhere. The playbooks and supporting images are also versioned, so the linked evidence accompanies a repository clone. No operational configuration or playbook contents were changed for this publication update.

## Supporting images

All three supplied images are included in version control. They were inspected and preserved; they supplement rather than supersede the newest configuration exports.

| Image | Evidence supplied | Limit |
|---|---|---|
| [images/1.jpeg](../images/1.jpeg) | Physical lab workspace, topology/document and terminal/dashboard screens | Screen content is insufficient for a complete readable feature-validation report or verified monitoring deployment |
| [images/2.jpeg](../images/2.jpeg) | Reference three-site topology, exact drawn core/access port mapping, server/WLC/AP attachments and intended branch phones | No explicit stage/date; branch voice drawing conflicts with latest VLAN/port configuration |
| [images/3.jpeg](../images/3.jpeg) | Historical Ansible recap for all ten aliases, zero reported failures/unreachable hosts, delegated localhost messages | Invocation/full tasks absent; consistent with backup collection, not evidence of ping/IPsec/HSRP success |

## Primary final-state sources

Source IDs used below link to the exact newest file by filename timestamp. Internal config/NVRAM timestamps corroborate history but do not override filename selection. Controller filename timezone is unspecified. Each hostname is the inventory alias plus `-222`.

| ID | Device alias | Newest export | Key blocks / line ranges |
|---|---|---|---|
| ZR | RT1-Zg | [2026-02-12_20-20-50](../playbooks/backups/RT1-Zg_2026-02-12_20-20-50.txt) | Crypto 101–121; interfaces 127–171; OSPF/NAT/routes 183–216; VTY/NTP 259–272 |
| PR | RT1-Pl | [2026-02-12_20-20-50](../playbooks/backups/RT1-Pl_2026-02-12_20-20-50.txt) | DHCP 32–98; crypto 129–146; interfaces 153–240; OSPF/NAT 253–285; VTY/NTP 311–322 |
| SR | RT1-St | [2026-02-12_20-20-50](../playbooks/backups/RT1-St_2026-02-12_20-20-50.txt) | DHCP 33–96; crypto 128–145; interfaces 152–238; OSPF/NAT 251–283; VTY/NTP 309–320 |
| DH | DHCP-SRV | [2026-02-12_20-20-50](../playbooks/backups/DHCP-SRV_2026-02-12_20-20-50.txt) | DHCP 33–131; interfaces 169–190; route/HTTP 192–206; VTY/NTP 232–242 |
| M1 | MLS1-Zg | [2026-02-12_20-20-51](../playbooks/backups/MLS1-Zg_2026-02-12_20-20-51.txt) | STP 163–166; trunks/channel 230–277; SVIs 405–528; OSPF/defaults 530–557; VTY/NTP 576–585 |
| M2 | MLS2-Zg | [2026-02-12_20-20-51](../playbooks/backups/MLS2-Zg_2026-02-12_20-20-51.txt) | STP 163–166; trunks/channel 230–275; SVIs 403–526; OSPF/defaults 528–555; VTY/NTP 574–583 |
| A1 | SW1-Zg | [2026-02-12_20-20-51](../playbooks/backups/SW1-Zg_2026-02-12_20-20-51.txt) | Snooping/DAI 24–29; PVST 60; server/voice ports 70–350; trunks/management 372–403; VTY/NTP 416–425 |
| A2 | SW2-Zg | [2026-02-12_20-20-51](../playbooks/backups/SW2-Zg_2026-02-12_20-20-51.txt) | Snooping/DAI 24–29; PVST 60; access 70–348; AP/WLC/trunks 350–396; management/VTY/NTP 402–434 |
| PA | SW1-Pl | [2026-02-12_20-20-50](../playbooks/backups/SW1-Pl_2026-02-12_20-20-50.txt) | Snooping 28–30; PVST 59; access 73–225; AP/uplink 252–282; management/VTY/NTP 293–324 |
| SA | SW1-St | [2026-02-12_20-20-51](../playbooks/backups/SW1-St_2026-02-12_20-20-51.txt) | DAI/snooping 24–29; PVST 60; access 78–230; trunks 70–76,272–286; management/VTY/NTP 312–343 |

## Snapshot catalog

All snapshots are dated **2026-02-12**. Each listed time maps to the exact path `playbooks/backups/<alias>_2026-02-12_<time>.txt` (hyphens separate hours/minutes/seconds). The latest entry is bold and linked in the source table above.

Repository cleanup removed five exports with filename time `18-39-24`: DHCP-SRV, RT1-Zg, RT1-Pl, RT1-St and SW1-Pl. The retained count decreased from 36 to **31**. No latest export was removed, so all ten primary sources, their line references and the reconstructed final architecture are unchanged. The Pula evolution comparison now uses the retained `18-40-11` export. The catalog below lists only files that remain in the repository.

| Device alias | Count | All filename times, oldest → newest |
|---|---|---|
| DHCP-SRV | 2 | 18-40-11, **20-20-50** |
| MLS1-Zg | 6 | 18-13-56, 18-22-22, 18-26-53, 18-39-25, 18-40-12, **20-20-51** |
| MLS2-Zg | 6 | 18-13-56, 18-22-22, 18-26-53, 18-39-25, 18-40-12, **20-20-51** |
| RT1-Zg | 2 | 18-40-11, **20-20-50** |
| RT1-Pl | 2 | 18-40-11, **20-20-50** |
| RT1-St | 2 | 18-40-11, **20-20-50** |
| SW1-Zg | 3 | 18-39-25, 18-40-12, **20-20-51** |
| SW2-Zg | 3 | 18-39-25, 18-40-12, **20-20-51** |
| SW1-Pl | 2 | 18-40-11, **20-20-50** |
| SW1-St | 3 | 18-39-25, 18-40-12, **20-20-51** |
| **Total** | **31** | Ten device aliases; final collection spans two filename seconds |

## Network feature evidence

Source IDs reference the exact paths and line ranges above. Negative findings refer to absence in the complete latest exports, not a claim that the technology never existed elsewhere.

| Feature | Devices | Evidence | Status | Notes |
|---|---|---|---|---|
| Three-site router infrastructure | RT1-Zg/Pl/St | ZR/PR/SR hostnames and interface descriptions; [inventory](../inventory) | Verified | Logical roles, not physical neighbor discovery |
| IPv4 addressing / subnet segmentation | All ten | Interface blocks in all sources | Verified | Addressing tables derived from masks, not host-table aliases |
| IPv6 LAN addressing | Routers, MLS pair | ZR/PR/SR/DH/M1/M2 interface blocks | Verified | ZR core transits link-local only; branches/MLS have global LAN addresses |
| Inter-site IPv6 connectivity | Site routers | No IPv6 tunnel addressing, OSPFv3 or corresponding inter-site IPv6 routes in ZR/PR/SR | Required by lab but not evidenced | LAN IPv6 does not prove end-to-end IPv6 |
| VLAN use / SVIs / 802.1Q | MLS and access, branches | M1/M2 SVIs/trunks; A1/A2/PA/SA ports; PR/SR encapsulation | Verified | Explicit VLAN database/names not captured |
| Static EtherChannel | MLS pair | M1/M2 Po1, Gi1/0/2–3, `mode on` | Verified | Bundle state unverified; LACP/PAgP not evidenced |
| HSRPv2 IPv4/IPv6 | MLS pair | M1/M2 eight SVI standby groups | Verified | Matching VIPs/group preferences; elections/failover not captured |
| Split STP priority roles | MLS pair | M1/M2 priority 4096/8192 by VLAN subset | Verified | Root election not captured |
| Rapid PVST | MLS pair | M1/M2 `spanning-tree mode rapid-pvst` | Verified | Access uses PVST |
| End-to-end rapid STP | All switches | A1/A2/PA/SA `spanning-tree mode pvst` | Required by lab but not evidenced | Mixed mode final state |
| OSPF 100 / area 0 | Site routers and MLS | ZR/PR/SR/M1/M2 `router ospf 100` | Verified | Configured interface selection, not adjacency |
| OSPF on Pula–Split tunnel | RT1-Pl/St | PR/SR Tunnel1 and OSPF blocks | Partially evidenced | Tunnel exists; `.9/.10` not selected by OSPF |
| Default routes / OSPF origination | Routers, MLS | ZR `default-information originate`; IPv4 routes in ZR/PR/SR/DH/M1/M2 | Verified | Only Zagreb originates; MLS IPv6 defaults also present |
| Stage 1 / SRWE static and floating routes | Earlier design | Supplied lab context; latest exports retain defaults, not original inter-site/floating routes | Required by lab but not evidenced | Do not recreate obsolete routing |
| GRE tunnel pairs | Site routers | ZR/PR/SR Tunnel0/1 | Verified | Reciprocal endpoints and /30s; tunnel status absent |
| IPsec / ISAKMP | Site routers | ZR/PR/SR crypto policies, keys, maps and selectors | Verified | IKEv1 AES/DH5 and ESP AES/SHA-HMAC; no established-SA output |
| DHCP WAN addressing | Site routers | ZR/PR/SR WAN `ip address` lines are static | Required by lab but not evidenced | Final config supersedes requirement |
| PAT | Site routers | ZR/PR/SR NAT inside/outside, ACL 1 and overload | Verified | Translation table/test absent |
| Static NAT port forwarding | RT1-Zg | ZR TCP translations 80/443/22 to DH `.67` | Verified | TCP port mappings, not one-to-one IP NAT |
| DHCPv4 / relay | DHCP-SRV, branches, MLS | DH/PR/SR pools; M1/M2 helper addresses | Verified | Pools only for listed VLANs; no leases |
| Stateful DHCPv6 on branch VLAN 30/50 | RT1-Pl/St | PR/SR pools, M flag and server attachments | Verified | Successful leases not established |
| Centralized Zagreb DHCPv6 | DHCP-SRV, MLS | DH pool definitions; no server attachment or MLS relay | Partially evidenced | Pools alone insufficient |
| Pula VLAN 60 stateful DHCPv6 | RT1-Pl | PR pool exists, VLAN 60 lacks attachment | Partially evidenced | No client result |
| WLC / AP / WLAN infrastructure | Access switches | A2 AP/WLC descriptions; PA/SA AP-style trunks; host aliases; images/2.jpeg | Partially evidenced | Drawing plus switch preparation; no controller/AP configs or WLAN runtime evidence |
| AP groups / FlexConnect | Wireless equipment | No WLC/AP exports or matching automation | Required by lab but not evidenced | Trunk pattern does not prove mode |
| Port-security / PortFast / BPDU Guard | Four access switches | A1/A2/PA/SA access blocks | Verified | Scope varies; counters/events absent |
| DHCP snooping | Four access switches | A1/A2/PA/SA global enable, VLAN lists and trust/rate commands | Verified | No bindings; no MLS global enable |
| Dynamic ARP Inspection | SW1/2-Zg, SW1-St | A1/A2 VLAN lists; SA VLAN 30 | Verified | Not evidenced on Pula or MLS; nonuniform coverage |
| Shutdown unused ports | Switches | VLAN 99 assignments and shutdown ranges in M1/M2/A1/A2/PA/SA | Partially evidenced | Empty blocks/prepared unshutdown ports prevent universal claim |
| SSH / local management hardening | All ten | VTY/local-user/login-block settings in all sources | Partially evidenced | SA VTY 3–15 differs; explicit SSHv2 not uniform |
| SNMP community / syslog destination | All ten | All sources; [config-monitor.yml](../playbooks/config-monitor.yml) | Verified | Read-only communities, `.70` logging; no successful collection evidence |
| SNMP limited to monitoring server | All ten intended | [acl.yml](../playbooks/acl.yml) ACL_SNMP and community task; absent from final exports | Partially evidenced | Authored automation only; final community unbound |
| SSH limited to ADMIN/STAFF | All ten intended | acl.yml ACL_SSH/VTY tasks; absent from final exports | Partially evidenced | No final binding; branch ranges broader than comments |
| Guest-only-Internet policy | Routed guest segments | No applied interface ACL in latest sources | Required by lab but not evidenced | VLAN/NAT presence is not isolation |
| Voice Internet prohibition | Zagreb voice segment | M1/M2 VLAN 40; ZR broad NAT ACL; no policy ACL | Required by lab but not evidenced | No negative test results |
| NTP hierarchy | All ten | NTP lines in all sources | Verified | No synchronization status |
| LibreNMS deployment | Monitoring endpoint | `.70` comments in [test-conn.yml](../playbooks/test-conn.yml) and acl.yml | Partially evidenced | Intended endpoint; no installation, dashboard or polls |
| Voice VLAN / DHCP preparation | Zagreb | M1/M2 VLAN 40; DH pool; A1/A2 voice assignments | Verified | No branch voice VLAN gateway |
| Telephony / option 150 / ephones | Telephony service | No relevant final command blocks or RTVi backup | Required by lab but not evidenced | Voice-card/MGCP defaults do not prove service |
| DNS configuration references | RT1-Zg, DHCP pools | ZR DNS server/name-server; DH/PR/SR DNS pool settings | Verified | Resolution success unverified; host-table drift |

## Automation and validation evidence

| Feature | Devices | Evidence | Status | Notes |
|---|---|---|---|---|
| Inventory grouping | Ten Cisco aliases | [inventory](../inventory) | Verified | routers + switches under cisco; addresses match final interfaces |
| SSH/enable connection model | Controller and cisco group | [ansible.cfg](../ansible.cfg), [all.yml](../group_vars/all.yml), [ssh-config](../ssh-config) | Verified | Authored settings; effective transport/version not tested |
| Running-config backup | cisco group | [backup.yml](../playbooks/backup.yml), 31 versioned exports | Verified | Collection workflow and historical artifacts; execution attribution not proven |
| Configuration save | cisco group | [save.yml](../playbooks/save.yml), acl.yml; latest NVRAM headers | Verified | Authored workflow plus recorded historical save timestamps, no play recap |
| Critical IPv4 endpoint test | cisco group | test-conn.yml: `.193`, `.70`, `.67` | Verified | Test code only; no retained outcomes/assertions |
| Inventory-wide IPv4 test | cisco group | [full-conn.yml](../playbooks/full-conn.yml) | Verified | 90 directed invocations for ten hosts; no retained results |
| Monitoring automation | cisco group | config-monitor.yml | Verified | SNMP/syslog only, not NTP/LibreNMS deployment; no explicit save |
| Management ACL automation | cisco group | acl.yml | Verified | Code present; application not evidenced in final exports |
| Historical Ansible execution recap | Ten inventory aliases | images/3.jpeg | Partially evidenced | Successful photographed recap; invocation/task attribution incomplete |
| Successful historical ping/traceroute | Clients / devices | No retained command output | Required by lab but not evidenced | Existence of test playbooks is not success evidence |
| Wireshark ICMP analysis | Stage 1 testing | No captures/reports | Required by lab but not evidenced | Project background only |
| Live validation during documentation | All devices | No connections or Ansible runs performed | Not applicable | Offline reconstruction task |

## Traceability and follow-up

Architecture diagrams are grounded in interface addresses/descriptions, trunk configuration, routing selection and crypto relationships. Inferred physical links and unavailable endpoint configuration are labeled in [02](02-final-architecture.md). The snapshot inventory and this matrix anchor the README's technology claims. The [review register](10-validation-and-testing.md#manual-review-register) records discrepancies and recommends additional state evidence.

The published backup evidence package establishes the configuration baseline. Additional priorities are retained connectivity results, OSPF/IPsec/HSRP state captures, exact cable mapping, and missing wireless/telephony/monitoring artifacts. Preserve the distinction between assignment intent, authored automation, configured final state and demonstrated behavior.
