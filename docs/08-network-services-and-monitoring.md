# 08 — Network services and monitoring

[Portfolio overview](../README.md) · [Source index](12-evidence-matrix.md#primary-final-state-sources)

## DHCPv4

The final [DHCP-SRV](../playbooks/backups/DHCP-SRV_2026-02-12_20-20-50.txt) is a Cisco router at `172.20.7.67/26` in server VLAN 10. Its five IPv4 pools serve Zagreb VLANs **20, 30, 40, 50 and 60**, using the matching MLS HSRP VIPs as default routers. DNS is `1.1.1.1`; exclusions include physical gateways, VIPs and selected clients. Both MLS devices configure `ip helper-address 172.20.7.67` on all eight routed VLANs, including VLANs 5/6/10 for which corresponding DHCPv4 pools are absent.

Pula and Split routers supply local DHCPv4 pools for VLANs **30, 50 and 60**, with their respective subinterface addresses as gateways. Pools, exclusions and gateway subnets agree for those served VLANs. No binding, conflict or relay statistics establish actual address assignment.

The DHCP pool domain string is `isepacadamy.ccna.itn.com`, while the management `ip domain name` string uses `isepacademy.ccna.itn.com`. This spelling difference is retained as evidence.

## IPv6 and DHCPv6

- DHCP-SRV defines stateful pools for Zagreb VLANs 20/30/40/50/60, with matching `2001:A` LAN prefixes and Google's IPv6 DNS server.
- No `ipv6 dhcp server` attachment on DHCP-SRV or DHCPv6 relay/server attachment on the MLS SVIs is exported. Pool definitions alone do not establish a working centralized DHCPv6 service.
- Pula/ Split attach stateful DHCPv6 pools and `ipv6 nd managed-config-flag` to VLAN 30 and 50 subinterfaces; prefixes match those interfaces.
- Pula defines a VLAN 60 stateful pool but does not attach it to the VLAN 60 subinterface. Split has no VLAN 60 DHCPv6 pool definition.
- MLS devices retain IPv6 HSRP groups and IPv6 defaults towards RT1-Zg. Site routers have no evidenced inter-site IPv6 tunnel/routing configuration.

## NTP hierarchy

| Devices | Configured time source | Notes |
|---|---|---|
| RT1-Zg | `pool.ntp.org` (static host mapping 162.159.200.1) | WAN source Gi0/2, `ntp master 10`, calendar update |
| RT1-Pl and SW1-Pl | 10.0.0.1 | Zagreb's Pula-facing tunnel address |
| RT1-St and SW1-St | 10.0.0.5 | Zagreb's Split-facing tunnel address |
| DHCP-SRV, MLS1/2, SW1/2-Zg | 172.20.7.193 | Zagreb edge core-facing address |

This forms a configured Zagreb-centered hierarchy. No association/status capture demonstrates synchronization. `ntp master 10` is a configured local fallback/reference behavior, not proof of an external synchronized clock. NTP is not configured by the monitoring playbook.

## SNMP, syslog and LibreNMS references

All ten latest device exports contain a read-only SNMP community without an access-list binding and a syslog destination `172.20.7.70`. [config-monitor.yml](../playbooks/config-monitor.yml) declares SNMP read-only access, syslog destination, informational trap level and logging enabled. The final exports show the endpoint, but do not uniformly export the playbook's explicit trap-level/on lines; platform defaults and execution history are not separately captured.

[test-conn.yml](../playbooks/test-conn.yml) identifies `.70` as “Server 1 (LibreNMS)”, and [acl.yml](../playbooks/acl.yml) labels it LibreNMS. This supports the intended monitoring role, **not** a verified LibreNMS deployment. No server installation/configuration, SNMP poll result, dashboard, alert, syslog receipt or retention policy is present. SNMPv2c is specified by the lab context; the exported community-based configuration alone does not demonstrate a particular successful poll version.

## Voice service boundary

Zagreb has VLAN 40 SVIs, HSRP, a DHCPv4 pool and access ports with `switchport voice vlan 40`. SW1-Zg Fa0/10 is described `IP-Phone-1001`; SW2-Zg Fa0/20 is described as an IP-phone connection. These establish **voice network preparation**.

No final export contains `telephony-service`, ephones, directory numbers or DHCP option 150. Router `voice-card`, MGCP defaults, voice license statements and a shutdown gatekeeper do not establish an operating telephony service. No RTVi-Zg configuration backup exists despite host-table references to that alias; `.62` is also the management HSRP VIP. Phone registration, calls and telephony server identity are not evidenced.

## DNS references

RT1-Zg contains `ip dns server`, name-server `8.8.8.8`, WAN lookup source and static host mappings; other devices commonly disable domain lookup while retaining `ip host` entries. DHCP DNS settings are configured separately. Stale host entries are cataloged for review rather than used as authoritative topology evidence.
