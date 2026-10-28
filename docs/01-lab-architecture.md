# Lab Architecture

## Host machine

| Item | Value |
| --- | --- |
| CPU | Intel Core i5-13400F |
| RAM | 32 GB DDR5 |
| Hypervisor | Oracle VirtualBox 7.2 |

## Virtual machines

| VM | OS | Role | RAM | CPUs | Disk |
| --- | --- | --- | --- | --- | --- |
| splunk-siem | Ubuntu Server 26.04 LTS | SIEM (Splunk Enterprise) | 8 GB | 4 | 60 GB |
| DC1 | Windows Server 2022 | Domain controller (lab.local), log source | 6 GB | 2 | default |
| CLIENT1 | Windows | Domain workstation | - | - | - |
| Ethical-Hacker-Kali | Kali Linux | Attacker, for future simulations | 4 GB | 2 | default |

## IP plan

| Host | Network | Address | Notes |
| --- | --- | --- | --- |
| splunk-siem | NatNetwork 10.0.2.0/24 | 10.0.2.3 | DHCP |
| DC1 adapter 1 | Domain lab 192.168.10.0/24 | 192.168.10.10 | Static, DNS points to itself |
| DC1 adapter 2 | NatNetwork 10.0.2.0/24 | 10.0.2.4 | DHCP, used to reach Splunk |
| CLIENT1 | Domain lab 192.168.10.0/24 | 192.168.10.20 | |

## Design decisions

**Dual-homed domain controller.** DC1 already had a static address for the Active Directory lab. Changing it would have broken the domain, so I added a second adapter on the NAT Network instead. Real servers often use multiple network interfaces for the same reason.

**VirtualBox NAT Network instead of plain NAT.** With plain NAT, every VM sits on its own isolated network and the VMs cannot reach each other. A NAT Network puts the VMs on one shared network that also has internet access.

**Port forwarding bound to 127.0.0.1.** Binding to localhost means only my own PC can reach the lab, not other devices on my home network.

| Rule | Protocol | Host IP:Port | Guest IP:Port | Purpose |
| --- | --- | --- | --- | --- |
| SSH | TCP | 127.0.0.1:2222 | 10.0.2.3:22 | Remote admin of the Splunk server |
| Splunk | TCP | 127.0.0.1:8000 | 10.0.2.3:8000 | Splunk Web in my browser |

**DNS forwarder on the domain controller.** DC1 must use itself (127.0.0.1) for DNS so Active Directory works. To resolve internet names, I added a DNS forwarder (8.8.8.8) instead of pointing the network card at a public DNS server.

## Ports used

| Port | Service |
| --- | --- |
| 22 | SSH |
| 8000 | Splunk Web |
| 8089 | Splunk management |
| 9997 | Splunk receiving (from forwarders) |
