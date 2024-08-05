1. Delete Agents
- List pob wazuh
```
kubectl get pod -n wazuh -o wide
```
- Exec pob
```
kubectl exec -it wazuh-manager-master-0 -n wazuh -- /bin/bash
```
- Use manage_agents
```
sudo /var/ossec/bin/manage_agents
```
```
****************************************
* Wazuh v4.7.5 Agent manager.          *
* The following options are available: *
****************************************
   (A)dd an agent (A).
   (E)xtract key for an agent (E).
   (L)ist already added agents (L).
   (R)emove an agent (R).
   (Q)uit.
Choose your action: A,E,L,R or Q:
```
