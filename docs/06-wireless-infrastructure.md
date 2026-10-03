# 06 — Wireless infrastructure

[Portfolio overview](../README.md) · [Evidence matrix](12-evidence-matrix.md)

## Evidence boundary

The SRWE laboratory required a WLC, three lightweight APs, wireless/guest networks, AP groups and FlexConnect. The repository contains **switch-side preparation, host aliases and a [reference topology drawing](../images/2.jpeg)** showing a WLC and three APs, but no WLC/AP backups, WLAN configuration, association records or wireless test outputs. Wireless service implementation is therefore **partially evidenced**; the drawing establishes intended attachments, not joined APs or operating WLANs.

## Switch-side attachments

| Export | Interface | Native VLAN | Allowed VLANs | Observed role |
|---|---|---|---|---|
| [SW2-Zg](../playbooks/backups/SW2-Zg_2026-02-12_20-20-51.txt) | Fa0/21 | 5 | 5,50,60 | Description `connection to ap`; no shutdown command |
| SW2-Zg | Fa0/22 | 5 | 5,50,60 | Second prepared AP-style trunk, explicitly shutdown |
| SW2-Zg | Fa0/23 | 6 | 5,6,50,60 | Description `connection to wlc`; no shutdown command |
| [SW1-Pl](../playbooks/backups/SW1-Pl_2026-02-12_20-20-50.txt) | Fa0/21–22 | 5 | 5,50,60 | AP-style trunks inferred from VLAN pattern, not descriptions |
| [SW1-St](../playbooks/backups/SW1-St_2026-02-12_20-20-51.txt) | Fa0/21–22 | 5 | 5,50,60 | AP-style trunks inferred from VLAN pattern, not descriptions |

Native VLAN 5 provides the intended untagged AP infrastructure segment, with tagged wireless and guest VLANs. The WLC-facing native VLAN is 6. Those are switch settings; compatibility with the remote device is unverified. The extra prepared ports do not establish more than three deployed APs.

## Referenced endpoints

Final MLS and Zagreb switch `ip host` entries reference WLC1-Zg `172.20.7.7`, AP1-Zg `172.20.7.131`, AP1-Pl `172.20.11.98` and AP1-St `172.20.13.226`. Site routers and branch switches retain some older WLC/Zagreb aliases. These are name-table references, not device interface evidence or DHCP leases.

The address plan supports AP, management, wireless and guest segments. Branch routers supply IPv4 pools for VLANs 50/60 and gateways for VLAN 5; Zagreb's DHCP router supplies pools for VLANs 50/60. No Zagreb VLAN 5 DHCPv4 pool is exported despite core helper addresses on that VLAN, and no AP discovery option 43 is visible.

## Not evidenced in repository

- WLC model, firmware, management interface, dynamic interface mappings or AP join state.
- SSIDs, WLAN security, authentication method or client association.
- AP groups, FlexConnect mode/local switching, or controller redundancy.
- DHCP/AP discovery behavior, RF parameters or wireless roaming results.
- Guest isolation, guest Internet reachability or successful wireless DHCP.

Useful additional evidence would include sanitized controller configuration, WLAN-to-VLAN mappings, AP inventory/join state and wired/wireless client tests. No wireless configuration was reconstructed or added to operational files.
