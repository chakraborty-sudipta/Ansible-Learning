**Encrypt variable value using ansible-vault command and avoid hardcoding values in Ansible playbook which makes it more secure**

<pre>
First, I will create a variable file and name it api_variable.yml which contains plain text information like api_url, api_method etc.

root@control:~/ansible-labs# vi api_variable.yml
root@control:~/ansible-labs# cat api_variable.yml
api_url: https://regres.in/api/unknown

api_method: GET
root@control:~/ansible-labs#

Next, I will encrypt the value of the variable api_url in the api_variable.yml file using ansible-vault command.

root@control:~/ansible-labs# ansible-vault encrypt_string 'https://regres.in/api/unknown' --name 'api_url'
New Vault password:
Confirm New Vault password:
api_url: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          65303564626235333261663138363230656338363861613164376462316233343366393330613435
          3732366335346464323433663436336238643465656634390a343165356137316238316638393364
          62336335623736613532303233666435373162343965353038656365643530613661656665343163
          3839313739326537620a353837663536656331336362316437393130316336326463333361653863
          63343836323062363366653333346631306232646262626366636363626638373335
Encryption successful
root@control:~/ansible-labs#

Now, we will replace https://regres.in/api/unknown in variable file with the above generated value which will look like:

root@control:~/ansible-labs# cat api_variable.yml
api_url: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          65303564626235333261663138363230656338363861613164376462316233343366393330613435
          3732366335346464323433663436336238643465656634390a343165356137316238316638393364
          62336335623736613532303233666435373162343965353038656365643530613661656665343163
          3839313739326537620a353837663536656331336362316437393130316336326463333361653863
          63343836323062363366653333346631306232646262626366636363626638373335

api_method: GET

Now, I will create a playbook file & name it vault_demo.yml which looks like:

root@control:~/ansible-labs# cat vault_demo.yml
---
- name: Use encrypted file
  hosts: dbservers
  vars_files:
    - api_variable.yml
  tasks:
    - name: Curl API URL with 200 status
      ansible.builtin.uri:
        url: "{{api_url}}"
        method: "{{api_method}}"
root@control:~/ansible-labs#

root@control:~/ansible-labs/playbooks# ansible-playbook -i ./hosts.ini ./vault_demo.yml --ask-vault-pass
Vault password:

PLAY [Use encrypted file] ***********************************************************************************************************

TASK [Gathering Facts] **************************************************************************************************************
ok: [node3]

TASK [Curl API URL with 200 status] *************************************************************************************************
ok: [node3]

PLAY RECAP **************************************************************************************************************************
node3                      : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

root@control:~/ansible-labs/playbooks#

As we can see that playbook ran successfully after providing the correct vault password.
</pre>

