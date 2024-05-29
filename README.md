# wazuh
## Install on client
### Ways 1:
1. Login wazuh mananger --> Agent --> Deploy New Agent
2. Fill up information --> copy command line
3. Past on Client

### Ways 2:
```sh
wget https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.7.4-1_amd64.deb && sudo WAZUH_MANAGER='10.255.33.80' WAZUH_REGISTRATION_PASSWORD=$'password' dpkg -i ./wazuh-agent_4.7.4-1_amd64.deb
```
/var/ossec/bin/agent-auth -m 10.255.33.78 -A {name}

