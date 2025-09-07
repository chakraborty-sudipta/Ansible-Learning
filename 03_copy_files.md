**Ansible playbook file 03_copy_files.yml has been created and executed to copy files to remote nodes.**

<pre>
  
root@control:~/ansible-labs/playbooks# cat 03_copy_files.yml
---
- name: Create a file and copy to all managed nodes
  hosts: all
  remote_user: root
  gather_facts: no
  tasks:
    - name: file creation
      delegate_to: localhost
      file:
        path: /tmp/testfile.txt
        state: touch


    - name: copy files to remote nodes
      copy:
        src: /tmp/testfile.txt
        dest: /tmp/testfile.txt


root@control:~/ansible-labs/playbooks# ansible-playbook 03_copy_files.yml -i /root/ansible-labs/hosts.ini

PLAY [Create a file and copy to all managed nodes] **********************************************************************************

TASK [file creation] ****************************************************************************************************************
changed: [node2]
changed: [node1]
changed: [node3]

TASK [copy files to remote nodes] ***************************************************************************************************
changed: [node1]
changed: [node2]
changed: [node3]

PLAY RECAP **************************************************************************************************************************
node1                      : ok=2    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node2                      : ok=2    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node3                      : ok=2    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

Verify on Nodes:

root@node1:~# cat /tmp/testfile.txt
This is a test file

root@node2:~# cat /tmp/testfile.txt
This is a test file

root@node3:~# cat /tmp/testfile.txt
This is a test file

we can see testfile.txt is copied to 3 remote nodes successfully.

</pre>
