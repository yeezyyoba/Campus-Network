# Campus Network Design – Cisco Packet Tracer

A two-building campus network (G+3), designed and built in Cisco Packet Tracer 9.0.

## Files

| File | What it is |
|------|------------|
| `Campus-Network-Topology.pkt` | The Packet Tracer file (open with Packet Tracer 9.0 or later) |
| `Campus-Network-Report.pdf` | Report covering the topology, VLAN table, IP table, VLAN 99 table, cabling, configs and tests |

## Design at a glance

- **Core (data center):** CORE-DC, a Cisco 3560 Layer-3 switch. It holds all VLAN gateways (SVIs), does inter-VLAN routing, runs DHCP and is the VTP server.
- **Access layer:** one Cisco 2960 per floor, 4 per building (8 in total). Each has one 802.1Q trunk to the core, native VLAN 99.
- **Per floor:** 3 PCs (Faculty / Student / Guest) and 3 access points (Faculty / Student / Guest). Each AP serves a tablet and a smartphone.
- **Wireless:** 24 standalone APs with WPA2-PSK/AES and one SSID per AP (e.g. `B1-F2-STUDENT`).
- **WAN:** CORE-DC → ETHIO-TELECOM (Cisco 2911) → REMOTE-CORE, using OSPF area 0. The remote site has 3 buildings.

## VLANs

| Building | Wired (Faculty / Student / Guest) | Wireless (Faculty / Student / Guest) | Network |
|----------|-----------------------------------|--------------------------------------|---------|
| B1 | 10 / 11 / 12 | 13 / 14 / 15 | 172.168.&lt;VLAN&gt;.0/24 |
| B2 | 16 / 17 / 18 | 19 / 20 / 21 | 172.168.&lt;VLAN&gt;.0/24 |
| All switches | Management VLAN 99 | – | 172.168.99.0/24 |
| Remote site | 30 / 40 / 50 | – | 172.168.&lt;VLAN&gt;.0/24 |

The gateway for each VLAN is `.1` on CORE-DC (or on REMOTE-CORE for the remote VLANs). DHCP hands out `.11–.254`.

## Diagram colours

- Building 1: blue frame.
- Building 2: orange frame.
- Each floor has its own colour.
- Data center: red. Remote site: grey.

## Author

Eyob Nebyou
