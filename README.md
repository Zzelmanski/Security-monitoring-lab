# Network Security Monitoring Lab — Suricata (Windows host + VirtualBox VMs)

## Overview
This is a small network security monitoring lab built with:
- Suricata 8.0.1 running on a Windows host (Npcap)
- Two VirtualBox VMs on a Host-Only network (Attacker / Victim)

The lab simulates scanning and simple attacks (ICMP, TCP connect, nmap SYN/NULL/XMAS) and demonstrates detection via Suricata `local.rules`.

## Included artifacts
- `suricata.yaml` — Suricata configuration used
- `local.rules` — custom detection rules used in the lab
- `fast.log.txt` — Suricata `fast.log` alert excerpt
- `startup.txt` — evidence of startup and rule loading
- `nmap_scan.txt` — output of scans run from the attacker VM

## How I ran it (summary)
1. Started Suricata on the Windows host bound to the VirtualBox Host-Only adapter (Npcap device).
2. Launched victim and attacker VMs on Host-Only network.
3. Started service listeners on the victim (SSH, HTTP, netcat) and ran scans/traffic from attacker (nmap, nc, curl).
4. Collected `fast.log`, `eve.json`, and a trimmed PCAP for evidence and correlation.

## How to reproduce (short)
1. Ensure Suricata + Npcap installed on Windows. Bind Suricata to the Host-Only device GUID.
2. Add `local.rules` to Suricata rules directory and list in `suricata.yaml`.
3. Start Suricata, then from attacker VM run `nmap -sS -p1-200 <victim-ip>` and `nc <victim-ip> 54321`.
4. Correlate `fast.log` alerts with packets in Wireshark.

## Notes
This lab was executed entirely within an isolated Host‑Only network. Do not expose services to the public Internet.

