**This is for practicing Ansible labs.**

**Platform : WSL Ubuntu docker image.**

**Environment: 1 Ansible control node and 3 managed host nodes.**

**Lab hierarchical Structure:** 
<pre>
root@control:~/ansible-labs/playbooks# tree ~/ansible-labs/

/root/ansible-labs/

|-- README.md

|-- ansible.cfg

|-- files

|   |-- welcome.txt

|-- group_vars

|    |-- all.yml

|    |-- dbservers.yml

|    |-- webservers.yml

|-- host_vars

|   |-- node1.yml

|   |-- node2.yml

|-- hosts.ini

|-- inventories

|   |-- prod

|   |   -- hosts.ini

|   |-- stage

|   |   -- hosts.ini

|-- playbooks

|   |-- 01_ping.yml

|   |-- 02_install_packages.yml

|   |-- 03_manage_users.yml

|   |-- 04_copy_files.yml

|   |-- 05_deploy_template.yml

|   |-- 06_service_tasks.yml

|   |-- 07_loops.yml

|   |-- 08_conditionals.yml

|   |-- 09_handlers.yml

|   |-- 10_roles.yml

|-- roles

|   |-- dbservers

|   |  -- tasks

|   |  -- main.yml

|   |-- webservers

|   |  -- tasks
   
|   |  -- main.yml 

|-- defaults   

|   | -- main.yml

|-- files

|   |  -- nginx.conf

|   |  -- handlers

|   |  -- main.yml

|-- tasks

|   |  -- main.yml

|   |  -- templates

|   |  -- index.html.j2

|-- vars

|   |-- main.yml

|-- templates

|   |-- motd.j2
</pre>
