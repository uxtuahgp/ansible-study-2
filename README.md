## Ansible homework 2 ##  
### Pre task ###  
Created VM with Fedora 37 OS managed with core username using ssh key  
Stored public VM IP in /etc/hosts  
 
### Task 1 ###  
Changed prod.yml  
```  
---
clickhouse:
  hosts:
    clickhouse-01:
      ansible_host: ch-01
      ansible_user: core

```  
### Task 2 ###
Added jinja template for /etc/vector/vector.yaml
Added tasks to get distr for vector and to install it
Added handler to restart service vector


