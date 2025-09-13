**Install a package on multiple nodes using Ansible when condtional**

<pre>

root@control:~/ansible-labs/playbooks# cat 08_conditionals.yml
---
- name: Install snapd package when it meets condition
  hosts: all
  become: true
  tasks:
    - name: Install snapd when OS is a specific version
      apt:
        name: snapd
        state: present
      when: ansible_facts['distribution']=="Ubuntu" and ansible_facts['distribution_version'] is search ("22.04")
  root@control:~/ansible-labs/playbooks# ansible-playbook 08_conditionals.yml -i /root/ansible-labs/hosts.ini --syntax-check

playbook: 08_conditionals.yml
root@control:~/ansible-labs/playbooks# ansible-playbook 08_conditionals.yml -i /root/ansible-labs/hosts.ini --check

PLAY [Install snapd package when it meets condition] ********************************************************************************

TASK [Gathering Facts] **************************************************************************************************************
ok: [node1]
ok: [node2]
ok: [node3]

TASK [Install snapd when OS is a specific version] **********************************************************************************
changed: [node3]
changed: [node2]
changed: [node1]

PLAY RECAP **************************************************************************************************************************
node1                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node2                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node3                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

root@control:~/ansible-labs/playbooks# ansible-playbook 08_conditionals.yml -i /root/ansible-labs/hosts.ini

PLAY [Install snapd package when it meets condition] ********************************************************************************

TASK [Gathering Facts] **************************************************************************************************************
ok: [node2]
ok: [node1]
ok: [node3]

TASK [Install snapd when OS is a specific version] **********************************************************************************
changed: [node1]
changed: [node2]
changed: [node3]

PLAY RECAP **************************************************************************************************************************
node1                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node2                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node3                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

Verification: Snapd package is installed on all managed nodes as can be seen using below adhoc command from control node.  

root@control:~/ansible-labs/playbooks# ansible -i /root/ansible-labs/hosts.ini all -m shell -a "dpkg -l | grep snapd"
node2 | CHANGED | rc=0 >>
ii  snapd                          2.68.5+ubuntu22.04.1                    amd64        Daemon and tooling that enable snap packages
node1 | CHANGED | rc=0 >>
ii  snapd                          2.68.5+ubuntu22.04.1                    amd64        Daemon and tooling that enable snap packages
node3 | CHANGED | rc=0 >>
ii  snapd                       2.68.5+ubuntu22.04.1                    amd64        Daemon and tooling that enable snap packages
</pre>
