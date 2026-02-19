## Ansible homework 2 ##  
### Pre task ###  
Created 3 VMs with Fedora 37 OS managed with fedora username using ssh key  
Stored public VM IP in /etc/hosts  
 
### Task 1 ###  
Updatetd playbook:  

### Task 2 ###  

Added jinja templates for clickhouse, vector and lighthouse services 

### Task 3 ###
Lighthouse sit is available 
### Task 4 ###
```
---
clickhouse:
  hosts:
    clickhouse-01:
      ansible_host: clickhouse-01
      ansible_user: fedora
vector:
  hosts:
    vector:
      ansible_host: vector-01
      ansible_user: fedora
lighthouse:
  hosts:
    lighthouse:
      ansible_host: lighthouse-01
      ansible_user: fedora

```  
### Task 5 ###  

```  
$ ansible-lint site.yml 
WARNING: PATH altered to include /usr/bin
WARNING  Overriding detected file kind 'yaml' with 'playbook' for given positional argument: site.yml
an AnsibleCollectionFinder has not been installed in this process
```  
### Task 6 ###  
```  
$ ansible-playbook -i inventory/prod.yml site.yml  --check
[WARNING]: Found both group and host with same name: vector
[WARNING]: Found both group and host with same name: lighthouse

PLAY [Install Clickhouse] **********************************************************************************************************************************************************************************

...  
TASK [lighthouse | Create lighthouse config] ***************************************************************************************************************************************************************
ok: [lighthouse]

PLAY RECAP *************************************************************************************************************************************************************************************************
clickhouse-01              : ok=7    changed=0    unreachable=0    failed=0    skipped=2    rescued=1    ignored=0   
lighthouse                 : ok=7    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
vector                     : ok=8    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0   

```  
### Task 7 ###  
```  
TASK [lighthouse | Create lighthouse config] ***************************************************************************************************************************************************************
ok: [lighthouse]

PLAY RECAP *************************************************************************************************************************************************************************************************
clickhouse-01              : ok=9    changed=0    unreachable=0    failed=0    skipped=0    rescued=1    ignored=0   
lighthouse                 : ok=7    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
vector                     : ok=9    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```  
### Task 8 ###  
Вторичный запуск --diff не показал изменений
