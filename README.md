# wazuh
## Install on client
### Ways 1:
1. Login wazuh mananger --> Agent --> Deploy New Agent
2. Fill up information --> copy command line
3. Past on Client

### Ways 2:
Install Wazuh client
```sh
wget https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.7.4-1_amd64.deb && sudo WAZUH_MANAGER='10.255.33.80' WAZUH_REGISTRATION_PASSWORD=$'password' WAZUH_AGENT_GROUP='default,Linux' WAZUH_AGENT_NAME='{name}' dpkg -i ./wazuh-agent_4.7.4-1_amd64.deb
```
Register Wazuh agents as authorized members
```sh
/var/ossec/bin/agent-auth -m 10.255.33.78 -A {name}
```
Restart services:
```sh
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

## Configure FIM (File Intergiry Monitoring)
### 1. Location configure:
Agent /var/ossec/etc/ossec.conf
```
    <syscheck>
       <directories><FILEPATH_OF_MONITORED_FILE></directories>
       <directories><FILEPATH_OF_MONITORED_DIRECTORY></directories>
    </syscheck>
```
### 2. AdvanceInstall Who-data monitoring
```
apt-get install auditd audispd-plugins
systemctl restart auditd
```
Edit the Wazuh agent /var/ossec/etc/ossec.conf configuration file and add the configuration below:
```
<syscheck>
   <directories check_all="yes" whodata="yes">/etc</directories>
</syscheck>
```
Once you add this configuration, restart the Wazuh agent to apply the changes. This will add an audit rule for the monitored directory:
```
systemctl restart wazuh-agent
```
Execute the following command to check if the audit rule for monitoring the selected directory is applied:
```
auditctl -l | grep wazuh_fim
```
From the output, you can see the rule was added:
Output
auditctl -w /etc -p wa -k wazuh_fim

Collect log from agent
```
  <localfile>
    <log_format>syslog</log_format>
    <location>/var/log/audit/audit.log/location>
  </localfile>
```

## Malware detection
