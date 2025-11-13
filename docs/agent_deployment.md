# Wazuh Agent Deployment Documentation

## Steps Completed
- Installed Wazuh agent on Ubuntu target VM  
- Installed Wazuh agent on Windows target VM  
- Both agents actively reporting to Wazuh server  
- Agents visible and connected in Wazuh dashboard  

## Verification Evidence
- Ubuntu agent status: `/screenshots/utarget_agent.png`
- Windows agent status: `/screenshots/wtarget_agent.png`
- Both agents showing as active endpoints in dashboard

## Commands Used

### Ubuntu Target VM Installation
```bash
wget https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.14.0-1_arm64.deb
sudo WAZUH_MANAGER='192.168.0.150' dpkg -i ./wazuh-agent_4.14.0-1_arm64.deb
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

### Windows Target VM Installation
```bash
Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.14.1-1.msi -OutFile $env:tmp\wazuh-agent
msiexec.exe /i $env:tmp\wazuh-agent /q WAZUH_MANAGER="192.168.0.150"
NET START Wazuh
```

### Updated Network Configuaration
- Wazuh Server IP: 192.168.0.150
- Ubuntu Target VM IP: 192.168.0.11
- Windows Target VM IP: 192.168.0.40
