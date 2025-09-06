## Objective: Collect ansible_facts for each host and save to facts/<host>.json.

## Prerequisites: Python present on managed hosts.

**Check with python --version**

## Create file: playbooks/02_gather_facts.yml

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

(This playbook copies JSON of ansible_facts to control under facts/.)

## Run:

**mkdir -p facts**

**ansible-playbook -i hosts.ini playbooks/02_gather_facts.yml**

## Verify:

**ls -l facts/**

**cat facts/node1.json | head -n 20**


**You should see JSON containing OS, CPU, memory facts like ansible_distribution, ansible_memtotal_mb, etc.**

## Alternative quick command:

**ansible -i hosts.ini all -m setup --tree ./facts**
