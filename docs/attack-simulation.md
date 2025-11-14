 # Attack Simulation Documentation

## Steps Completed
 - Installed attack tools on Kali Linux VM  
 - Executed SSH brute force attack on Ubuntu target  
 - Performed network reconnaissance on Windows target  
 - Confirmed detection in both Wazuh and Suricata  
 - Documented multi-vector attack detection capabilities  

## Verification Evidence
- SSH brute force detection: `/screenshots/wazuh_dashboard_events.png`
- Windows network scan detection: `/screenshots/wazuh_network_scan_detection.png`
- Suricata network alerts: `/screenshots/suricata_log.png`

## Commands Used

### Kali VM Attack Tools Installation
```bash
sudo apt update
sudo apt install hydra nmap -y
```

### SSH Brute Force Attack (Ubuntu Target)
```bash
# Target: 192.168.0.11
hydra -l root -P /usr/share/wordlists/rockyou.txt.gz -t 4 -vV ssh://192.168.0.11

# Quick test version
hydra -l root -p password123 -t 4 -vV ssh://192.168.0.11
```

### Network Reconnaissance (Windows Target)
```bash
# Target: 192.168.0.40
nmap -sS 192.168.0.40
nmap -sV 192.168.0.40
nmap -O 192.168.0.40
nmap -A 192.168.0.40

# SMB enumeration
smbclient -L //192.168.0.40 -N
```

### Detection Monitoring
```bash
# Suricata logs (Ubuntu target)
sudo tail -f /var/log/suricata/fast.log

# Wazuh agent logs (Ubuntu target)
sudo tail -f /var/ossec/logs/alerts/alerts.log

# Windows firewall logs (Windows target)
Get-Content "C:\Windows\System32\LogFiles\Firewall\pfirewall.log" -Tail 20
```

## Attack Results

### Ubuntu Target Detection
- **Wazuh:** Rule 5710 - "sshd: brute force trying to get access to the system. Authentication failed."

- **Alert Level:** 10 (Security event with high confidence)

- **Suricata:** SSH brute force patterns detected in network traffic

- **Multiple authentication failures** correlated from same source IP

### Windows Target Detection

- **Wazuh:** Rule 4151 - "Multiple Firewall drop events from same source"

- **Windows Firewall:** Successfully blocked all reconnaissance attempts

- **Event Details:** Multiple DROP TCP events for ports 135, 139, 445

- **Source IP:** 192.168.0.200 (Kali VM)

### Windows Firewall Log Events
- 2025-11-14 19:31:41 DROP TCP 192.168.0.200 192.168.0.40 56756 139
- 2025-11-14 19:31:42 DROP TCP 192.168.0.200 192.168.0.40 56756 135
- 2025-11-14 19:31:42 DROP TCP 192.168.0.200 192.168.0.40 56756 445

## Security Insights

### Detection Effectiveness
- **Layered Defense:** Combination of host-based (Wazuh) and network-based (Suricata) detection

- **Pattern Recognition:** Multiple failed events from single source triggered automated alerts

- **Real-time Alerting:** SOC team would receive immediate notifications for both attack types

### Technical Configuration

```xml
<!-- Windows firewall log monitoring added to ossec.conf -->
<localfile>
  <location>C:\Windows\System32\LogFiles\Firewall\pfirewall.log</location>
  <log_format>full_log</log_format>
</localfile>
```
### Attack Vectors Tested

- **SSH Brute Force:** Credential-based attack against Linux service
- **Network Reconnaissance:** Service enumeration and port scanning
- **SMB Enumeration:** Windows service discovery attempts

## Lessons Learned

- SSH brute force attacks reliably trigger high-confidence Wazuh alerts (Level 10)

- Network scans generate detectable patterns when correlated across multiple events

- Windows Firewall provides effective first-line defense but requires logging configuration

- Suricata adds valuable network-level context to host-based detections

- Multi-vector testing demonstrates comprehensive SOC monitoring capabilities

## SOC Value Demonstrated

- **Threat Detection:** Automated alerting for common attack patterns
- **Event Correlation:** Linking related security events across multiple systems
- **Incident Response:** Clear evidence for security team investigation
- **Security Monitoring:** Comprehensive coverage of network and host activity

