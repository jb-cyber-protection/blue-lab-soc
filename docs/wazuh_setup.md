# Wazuh Server Setup Documentation

## Steps Completed
✅ Downloaded and executed Wazuh installation script  
✅ All services running   
✅ Services enabled on boot (see screenshots/benabled.png)  
✅ Dashboard accessible with credentials  

## Verification Evidence
- Service status: `/screenshots/status_dashboard.png`
`/screenshots/status_indexer.png`
`/screenshots/status_manager.png`
- Boot configuration: `/screenshots/enabled.png` 
- Dashboard access: `/screenshots/Wazuh_dashboard.png`

## Commands Used
### Wazuh Installation
```bash
- wget https://packages.wazuh.com/4.14/wazuh-install.sh
- sudo chmod +x wazuh-install.sh
- sudo bash wazuh-install.sh --all-in-one
```

### Service Status Verification
```bash
- sudo systemctl status wazuh-manager
- sudo systemctl status wazuh-indexer
- sudo systemctl status wazuh-dashboard
```

### Boot Configuration Check
```bash
- sudo systemctl is-enabled wazuh-manager wazuh-indexer wazuh-dashboard
```

### Server IP Address:
```bash
- ip a
```
