# Blue Team SOC Home Lab

A fully functional Security Operations Center lab that detected and analyzed real multi-vector cyber attacks. This project demonstrates enterprise-grade security monitoring using Wazuh SIEM and Suricata IDS to correlate threats across Windows and Ubuntu targets.

## Key Achievements

- Detected & Analyzed SSH brute force attacks against Ubuntu target
- Identified network reconnaissance scans against Windows target
- Correlated Alerts across multiple security tools (Wazuh + Suricata)
- Documented NIST SP 800-61 compliant incident response
- Built enterprise-grade monitoring infrastructure with layered defense

## Architecture

[Architecture Diagram](https://architecture/diagram.png)

**Multi-Vector Attack Detection Environment**

- **Attacker:** Kali Linux (192.168.0.200)
- **Targets:**
  - Ubuntu Server (192.168.0.11) with Wazuh Agent + Suricata IDS
  - Windows 11 (192.168.0.40) with Wazuh Agent + Windows Firewall
- **SIEM:** Wazuh Server (192.168.0.150) correlating host + network logs
- **Detections:** Rule 5710 (SSH brute force) + Rule 4151 (port scans) + Suricata network alerts

## Technologies Used

- **Virtualization:** VirtualBox
- **SIEM:** Wazuh (Centralized monitoring & alert correlation)
- **IDS:** Suricata (Network intrusion detection)
- **Attack Tools:** Hydra (SSH brute force), Nmap (Port scanning)
- **Monitoring:** Custom alert rules & real-time dashboards
- **Documentation:** NIST SP 800-61 incident response framework

## Incident Summary

**Attack Timeline & Detection:**

**November 13, 2025 (23:24:52-23:26:52):** SSH brute force attacks from Kali (192.168.0.200) against Ubuntu target
- **Detection:** Wazuh Rule 5710 - "sshd: brute force trying to get access to the system. Authentication failed."
- **Result:** 3 failed authentication attempts blocked by SSH service

**November 14, 2025 (23:34:55-23:54:29):** Network reconnaissance from Kali against Windows target
- **Detection:** Wazuh Rule 4151 - "Multiple Firewall drop events from same source"
- **Result:** 4 firewall drop events blocking SMB port scans (135,139,445)

## Project Structure
```
blue-lab-soc/
├── architecture/
│   └── diagram.png                 # Network architecture & attack flow
├── docs/
│   ├── agent_deployment.md         # Wazuh agent installation guide
│   ├── attack-simulation.md        # Detailed attack methodology
│   ├── suricata-setup.md           # IDS configuration
│   └── wazuh_setup.md              # SIEM deployment guide
├── logs/
│   └── alerts.json                 # Suricata detection logs
├── report/
│   └── incident_report.pdf         # NIST-compliant incident report
└── screenshots/                    # Visual evidence & dashboards
    ├── wazuh_dashboard_events.png
    ├── suricata_log_gen.png
    ├── hydra_bruteforce.png
    └── [30+ additional evidence files]
```

## Security Controls Demonstrated

**Host-Based Security:**
- Wazuh Agents for real-time log collection
- Windows Firewall automated packet filtering
- SSH authentication brute force protection

**Network-Based Security:**
- Suricata IDS for network intrusion detection
- Centralized log correlation via Wazuh SIEM

**Detection Capabilities:**
- Real-time attack detection within seconds
- Automated containment via security controls
- Multi-source alert correlation

## Results & Evidence

**Successful Detections:**
- SSH brute force attempts immediately identified and blocked
- Network reconnaissance detected and prevented
- Layered defense strategy proven effective
- All attacks contained without system compromise

**Key Evidence:**
- [View Incident Report](report/incident_report.pdf) - Comprehensive NIST-compliant analysis
- [View Suricata Logs](logs/alerts.json) - Network intrusion detection evidence
- [View Architecture](architecture/diagram.png) - Enterprise security design

## Skills Demonstrated

- **SOC Analysis** - Real-time threat monitoring and investigation
- **Log Correlation** - Cross-referencing host and network security events
- **Incident Response** - NIST SP 800-61 compliant procedures
- **Security Monitoring** - SIEM and IDS configuration and management
- **Threat Detection** - Identifying and analyzing attack patterns
- **Professional Documentation** - Enterprise-ready reporting and evidence collection

## Lessons Learned & Improvements

**Key Findings:**
- Layered defense strategy effectively contained multi-vector attacks
- Automated security controls successfully prevented breach without manual intervention
- Alert correlation across systems provided comprehensive attack context

**Recommended Enhancements:**
- Implement Wazuh active response for automated IP blocking
- Expand Suricata rules for earlier SSH brute force detection
- Develop formal playbooks for common attack patterns
- Conduct regular attack simulations to maintain analyst proficiency

## Professional Contact 

This project demonstrates practical cybersecurity skills applicable to SOC analyst, security engineer, and incident responder roles. The complete lab setup, attack simulation, and enterprise documentation showcase readiness for security operations center environments.

This project is part of a comprehensive cybersecurity portfolio demonstrating end-to-end security capabilities from monitoring to incident response.