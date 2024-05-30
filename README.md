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
