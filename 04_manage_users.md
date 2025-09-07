**Day 04 — Manage Users (create ansibleadmin)**

**Objective**: Create a sudo user on remote nodes.

**Prerequisites**: generate SSH key on control (if not present).

**On control (generate key only if you need):**

**ssh-keygen -t rsa -b 4096 -f ~/.ssh/ansible_lab -N ""**

<pre>
Create file: playbooks/04_manage_users.yml

root@control:~/ansible-labs/playbooks# cat 04_manage_users.yml
- name: Create ansibleadmin
  hosts: all
  become: yes
  vars:
    ansible_user_name: ansibleadmin
  tasks:
    - name: Create ansibleadmin user
      user:
        name: "{{ ansible_user_name }}"
        shell: /bin/bash
        groups: sudo
        state: present
        create_home: yes

</pre>

**Run**:

**ansible-playbook -i hosts.ini playbooks/04_manage_users.yml**
<pre>

root@control:~/ansible-labs/playbooks# ansible-playbook 04_manage_users.yml -i /root/ansible-labs/hosts.ini --check

PLAY [Create ansibleadmin] **********************************************************************************************************

TASK [Gathering Facts] **************************************************************************************************************
ok: [node3]
ok: [node2]
ok: [node1]

TASK [Create ansibleadmin user] *****************************************************************************************************
changed: [node1]
changed: [node2]
changed: [node3]

PLAY RECAP **************************************************************************************************************************
node1                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node2                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node3                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

root@control:~/ansible-labs/playbooks# ansible-playbook 04_manage_users.yml -i /root/ansible-labs/hosts.ini

PLAY [Create ansibleadmin] **********************************************************************************************************

TASK [Gathering Facts] **************************************************************************************************************
ok: [node2]
ok: [node3]
ok: [node1]

TASK [Create ansibleadmin user] *****************************************************************************************************
changed: [node1]
changed: [node2]
changed: [node3]

PLAY RECAP **************************************************************************************************************************
node1                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node2                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node3                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
</pre>

**Verify**:

**root@node1:~# cat /etc/passwd | grep ansibleadmin**

ansibleadmin:x:1001:1001::/home/ansibleadmin:/bin/bash

**root@node2:~# cat /etc/passwd | grep ansibleadmin**

ansibleadmin:x:1001:1001::/home/ansibleadmin:/bin/bash

**root@node3:~# cat /etc/passwd | grep ansibleadmin**

ansibleadmin:x:1001:1001::/home/ansibleadmin:/bin/bash

**We can see ansibleadmin user is created on all 3 remote nodes managed by Ansible control node.**
