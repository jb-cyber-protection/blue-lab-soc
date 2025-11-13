# Suricata IDS Setup Documentation

## Steps Completed
✅ Installed Suricata IDS on Ubuntu target VM  
✅ Configured network interface and HOME_NET settings  
✅ Resolved interface configuration issues  
✅ Verified Suricata service is running  
✅ Set up network intrusion detection capability  

## Verification Evidence
- Suricata service status: `/screenshots/suricata_running.png`
- Configuration test: `/screenshots/suricata_log_gen.png`
- Network interface configuration confirmed:`/screenshots/suricata_integrated.png`

## Commands Used

### Suricata Installation
```bash
sudo apt update
sudo apt install suricata -y
sudo systemctl enable suricata
```

### Configuration Updates
```bash
# Fix network interface configuration
sudo sed -i 's/interface: eth0/interface: enp0s1/g' /etc/suricata/suricata.yaml
sudo sed -i 's/interface: eth1/interface: enp0s1/g' /etc/suricata/suricata.yaml
sudo sed -i 's/interface: eth2/interface: enp0s1/g' /etc/suricata/suricata.yaml

# Set HOME_NET to lab environment
# Updated in suricata.yaml: HOME_NET: "[192.168.0.0/24]"
```

### Service Management
```bash
# Test configuration
sudo suricata -T -c /etc/suricata/suricata.yaml

# Start and verify service
sudo systemctl start suricata
sudo systemctl status suricata

# Check logs
sudo tail -f /var/log/suricata/fast.log
```

### Rules Management
```bash
# Download and update Suricata rules
sudo suricata-update
sudo suricata-update enable-source et/open
sudo suricata-update
```

### Network Configuration
- Monitoring Interface: enp0s1
- HOME_NET: 192.168.0.0/24 (entire lab environment)
- Target VM IP: 192.168.0.11

## Issues Resolved
- Fixed "No such device" error by correcting network interface from eth0 to enp0s1
- Configured proper HOME_NET range for lab environment
- Verified rule sets are loaded and functional
