##	**o Use ping module to verify connectivity to all managed nodes.**

![Image](https://github.com/user-attachments/assets/de33d8fc-6c48-4055-bcb3-6229ea680d15)


**o	File: playbooks/01_ping.yml**

  ## To check playbook syntax errors
  
**root@control:~/ansible-labs/playbooks# ansible-playbook 01_ping.yml --syntax-check**

playbook: 01_ping.yml

 ## Dry run to simulate the action not the actual run
 
**root@control:~/ansible-labs/playbooks# ansible-playbook 01_ping.yml --check**

PLAY [ping all hosts] ***************************************************************************************************************

TASK [ping the hosts] ***************************************************************************************************************

ok: [node2]

ok: [node1]

ok: [node3]


PLAY RECAP **************************************************************************************************************************

node1                      : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

node2                      : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

node3                      : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0


## Actual run of playbook to check the ping test

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

