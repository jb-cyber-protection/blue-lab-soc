# Blue Team SOC Home Lab

This project builds a Security Operations Center (SOC) home lab to simulate real-world detection and monitoring. It integrates a SIEM (Wazuh) and IDS (Suricata) to detect attacks launched from Kali Linux against Windows and Ubuntu targets. The goal is to demonstrate SOC analysis, log correlation, and detection engineering.

## Tools & Technologies

- VirtualBox / VMware – Virtualization platform for lab VMs
- Kali Linux – Attacker machine
- Ubuntu Server – Target VM (with Suricata IDS)
- Windows 10 – Target VM (with Wazuh agent)
- Wazuh – SIEM for log collection and correlation
- Hydra – Brute force attack tool

## Setup

- Create 3 VMs: Kali, Ubuntu, Windows 10
- Install and configure Wazuh server on a dedicated VM
- Add Wazuh agents to Ubuntu and Windows targets
- Install Suricata on Ubuntu target
- Configure networking so all VMs can communicate

## VM Specifications

| VM       | OS Version        | vCPUs | RAM  | Disk  | IPv4 Address   | Subnet Mask     |
|----------|------------------|-------|------|-------|----------------|-----------------|
| Kali     | Kali Linux 2025  | 2     | 4 GB | 40 GB | 192.168.128.2 | 255.255.255.0   |
| Ubuntu   | Ubuntu 24.04.3 LTS | 2     | 2 GB | 30 GB | 192.168.128.3 | 255.255.255.0   |
| Windows  | Windows 11 Home   | 2     | 4 GB | 50 GB | 192.168.128.4 | 255.255.255.0   |


## Attack Simulation

From Kali, launch an SSH brute force attack against Ubuntu:

```bash
hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://<Ubuntu-IP>
```
Then:

Monitor Wazuh dashboard for alerts

Collect Suricata logs from /var/log/suricata/fast.log

## Monitoring & Log Collection

- Monitor Wazuh dashboard for alerts
- Collect Suricata logs from `/var/log/suricata/fast.log`

## Results

- **Wazuh Alerts:** Screenshots of detections
- **Suricata Logs:** Saved in `logs/alerts.json`
- **Architecture Diagram:** `architecture/diagram.png`

## Lessons Learned

- Importance of combining SIEM + IDS for layered defense
- How brute force attacks appear in logs
- How to document incidents like a SOC analyst

## Deliverables

- `architecture/diagram.png` – Lab network diagram
- `logs/alerts.json` – Suricata detection logs
- `report/incident_report.pdf` – SOC-style incident report

## Skills Demonstrated

- SOC analysis
- Log correlation
- Detection engineering
- Professional documentation

## Portfolio Notes

This README will serve as your portfolio front page for the project.

Each time you complete a step (VM setup, Wazuh install, attack, logs, report), update the README with:

- Screenshots
- Links to files
- Notes and observations