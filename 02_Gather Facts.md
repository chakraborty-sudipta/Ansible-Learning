## Objective: Collect ansible_facts for each host and save to facts/<host>.json.

## Prerequisites: Python present on managed hosts.

**Check with python --version**

## Create file: playbooks/02_gather_facts.yml

<pre> ``` 
  
---

- name: Gather facts and save to control
  hosts: all
  gather_facts: yes
  tasks:
    - name: Save facts to control machine
      copy:
        content: "{{ ansible_facts | to_nice_json }}"
        dest: "/root/ansible-labs/facts/{{ inventory_hostname }}.json"
      delegate_to: localhost
      run_once: false

  ``` </pre>

(This playbook copies JSON of ansible_facts to control under facts/.)

## Run:

**mkdir -p facts**

**ansible-playbook -i hosts.ini playbooks/02_gather_facts.yml**

root@control:~/ansible-labs# ansible-playbook playbooks/02_gather_facts.yml

PLAY [Gather facts and save to control] *********************************************************************************************

TASK [Gathering Facts] **************************************************************************************************************

ok: [node1]

ok: [node2]

ok: [node3]

TASK [Save facts to control machine] ************************************************************************************************

changed: [node3]

changed: [node1]

changed: [node2]


PLAY RECAP **************************************************************************************************************************

node1                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

node2                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

node3                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

root@control:~/ansible-labs# ls

README.md  ansible.cfg  facts  files  group_vars  host_vars  hosts.ini  inventories  playbooks  roles  templates

root@control:~/ansible-labs# cd facts/

root@control:~/ansible-labs/facts# ls

node1.json  node2.json  node3.json

## Verify:

**ls -l facts/**

**cat facts/node1.json | head -n 20**

root@control:~/ansible-labs# cat facts/node1.json | head -n 20

{
    "_ansible_facts_gathered": true,
    
    "all_ipv4_addresses": [
    
        "172.18.0.3"
        
    ],
    "all_ipv6_addresses": [],
    
    "ansible_local": {},
    
    "apparmor": {
    
        "status": "disabled"
        
    },
    
    "architecture": "x86_64",
    
    "bios_date": "NA",
    
    "bios_vendor": "NA",
    
    "bios_version": "NA",
    
    "board_asset_tag": "NA",
    
    "board_name": "NA",
    
    "board_serial": "NA",
    
    "board_vendor": "NA",
    
    "board_version": "NA",
    
    "chassis_asset_tag": "NA",
    
root@control:~/ansible-labs#


**You should see JSON containing OS, CPU, memory facts like ansible_distribution, ansible_memtotal_mb, etc.**

## Alternative quick command:

**ansible -i hosts.ini all -m setup --tree ./facts**
