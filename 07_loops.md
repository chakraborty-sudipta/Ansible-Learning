**Install multiple packages using loop in Ansible.**

<pre>
root@control:~/ansible-labs/playbooks# cat 07_loops.yml
---
- name: Install multiple packages using a loop
  hosts: all
  become: true
  tasks:
    - name: Install multiple packages
      apt:
        name: "{{ item }}"
        state: present
      loop:
        - vim
        - tree
        - unzip

root@control:~/ansible-labs/playbooks# ansible-playbook 07_loops.yml -i /root/ansible-labs/hosts.ini --syntax-check

playbook: 07_loops.yml

  root@control:~/ansible-labs/playbooks# ansible-playbook 07_loops.yml -i /root/ansible-labs/hosts.ini

PLAY [Install multiple packages using a loop] **************************************************************************

TASK [Gathering Facts] *************************************************************************************************
ok: [node1]
ok: [node3]
ok: [node2]

TASK [Install multiple packages] ***************************************************************************************
ok: [node3] => (item=vim)
ok: [node1] => (item=vim)
ok: [node2] => (item=vim)
changed: [node2] => (item=tree)
changed: [node3] => (item=tree)
changed: [node1] => (item=tree)
changed: [node2] => (item=unzip)
changed: [node1] => (item=unzip)
changed: [node3] => (item=unzip)

PLAY RECAP *************************************************************************************************************
node1                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node2                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node3                      : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

Verification: We can verify from Ansible control using below Adhoc command that packages are installed on managed nodes as can be seen.
We can even check from individual managed node.

root@control:~/ansible-labs/playbooks# ansible all -i /root/ansible-labs/hosts.ini -m shell -a "dpkg -l | grep -E 'vim|tree|unzip'"
node1 | CHANGED | rc=0 >>
ii  tree                           2.0.2-1                                 amd64        displays an indented directory tree, in color
ii  unzip                          6.0-26ubuntu3.2                         amd64        De-archiver for .zip files
ii  vim                            2:8.2.3995-1ubuntu2.24                  amd64        Vi IMproved - enhanced vi editor
ii  vim-common                     2:8.2.3995-1ubuntu2.24                  all          Vi IMproved - Common files
ii  vim-runtime                    2:8.2.3995-1ubuntu2.24                  all          Vi IMproved - Runtime files
node3 | CHANGED | rc=0 >>
ii  tree                        2.0.2-1                                 amd64        displays an indented directory tree, in color
ii  unzip                       6.0-26ubuntu3.2                         amd64        De-archiver for .zip files
ii  vim                         2:8.2.3995-1ubuntu2.24                  amd64        Vi IMproved - enhanced vi editor
ii  vim-common                  2:8.2.3995-1ubuntu2.24                  all          Vi IMproved - Common files
ii  vim-runtime                 2:8.2.3995-1ubuntu2.24                  all          Vi IMproved - Runtime files
node2 | CHANGED | rc=0 >>
ii  tree                           2.0.2-1                                 amd64        displays an indented directory tree, in color
ii  unzip                          6.0-26ubuntu3.2                         amd64        De-archiver for .zip files
ii  vim                            2:8.2.3995-1ubuntu2.24                  amd64        Vi IMproved - enhanced vi editor
ii  vim-common                     2:8.2.3995-1ubuntu2.24                  all          Vi IMproved - Common files
ii  vim-runtime                    2:8.2.3995-1ubuntu2.24                  all          Vi IMproved - Runtime files

</pre>
