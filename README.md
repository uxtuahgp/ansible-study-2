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
 
### Task 3 ###
```  
    - name: Get vector distrib
      ansible.builtin.get_url:
        url: https://setup.vector.dev
        dest: "./repo.sh"
```  
```  
    - name: Create vector config dir
      become: true
      ansible.builtin.file:
        state: directory
        owner: vector
        group: vector
        mode: 750
        path: /etc/vector
```  
```  
    - name: Make config for vector
      become: true
      template:
        src="templates/vector.yaml.j2"
        dest="/etc/vector/vector.yaml" 
```  
### Task 4 ###
```  
ASK [Get vector distrib] **********************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Install vector repo] *********************************************************************************************************************************************************************************
changed: [clickhouse-01]

TASK [Install vector] **************************************************************************************************************************************************************************************
ok: [clickhouse-01]

```  
### Task 5 ###  
```  
ASK [Get vector distrib] **********************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Install vector repo] *********************************************************************************************************************************************************************************
changed: [clickhouse-01]

TASK [Install vector] **************************************************************************************************************************************************************************************
ok: [clickhouse-01]
```  
### Task 6 ###  
```  
$ ansible-playbook -i inventory/prod.yml site.yml --check

PLAY [Install Clickhouse] **********************************************************************************************************************************************************************************

...
TASK [Enable vector service] *******************************************************************************************************************************************************************************
ok: [clickhouse-01]

PLAY RECAP *************************************************************************************************************************************************************************************************
clickhouse-01              : ok=9    changed=0    unreachable=0    failed=0    skipped=3    rescued=1    ignored=0   
```  
### Task 8 ###

