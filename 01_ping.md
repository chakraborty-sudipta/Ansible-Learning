o	**Use ping module to verify connectivity to all managed nodes.**

![Image](https://github.com/user-attachments/assets/de33d8fc-6c48-4055-bcb3-6229ea680d15)


**o	File: playbooks/01_ping.yml**
**root@control:~/ansible-labs/playbooks# ansible-playbook 01_ping.yml --syntax-check**  ## To check playbook syntax errors

playbook: 01_ping.yml
**root@control:~/ansible-labs/playbooks# ansible-playbook 01_ping.yml --check**  ## Dry run to simulate the action not the actual run

PLAY [ping all hosts] ***************************************************************************************************************

TASK [ping the hosts] ***************************************************************************************************************

ok: [node2]

ok: [node1]

ok: [node3]


PLAY RECAP **************************************************************************************************************************

node1                      : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

node2                      : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

node3                      : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0


**root@control:~/ansible-labs/playbooks# ansible-playbook 01_ping.yml**

PLAY [ping all hosts] ***************************************************************************************************************

TASK [ping the hosts] ***************************************************************************************************************

ok: [node2]

ok: [node3]

ok: [node1]


PLAY RECAP **************************************************************************************************************************

node1                      : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

node2                      : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

node3                      : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

