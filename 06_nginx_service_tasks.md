**Day 06 — Service Management (install & enable nginx)**

**Objective: Install nginx, enable and start service on both node1 and node2.**

**Create file: playbooks/06_nginx_service_tasks.yml**

<pre>
---
- name: Install Nginx and serve a webpage
  hosts: webservers
  become: yes
  gather_facts: no
  vars:
    nginx_package: nginx
    webpage_title: "Welcome to my webpage created by Ansible"
    webpage_content: "This webpage is served from {{ inventory_hostname }} using Ansible"
    webpage_path: /var/www/html/index.html

  tasks:
    - name: Install nginx package
      apt:
        name: "{{ nginx_package }}"
        state: present
        update_cache: yes

    - name: Deploy custom index.html
      copy:
        dest: "{{ webpage_path }}"
        content: |
          <html>
          <head><title>{{ webpage_title }}</title></head>
          <body><h1>{{ webpage_content }}</h1></body>
          </html>

    - name: Start nginx manually (container-friendly)
      shell: |
        nginx -g 'daemon off;' || true
</pre>

**Run:**

**ansible-playbook playbooks/ 06_nginx_service_tasks.yml**


**Verify:**
  
<pre>
root@node1:~# curl 172.18.0.4
<html>
<head><title>Welcome to my webpage created by Ansible</title></head>
<body><h1>This webpage is served from node2 using Ansible</h1></body>
</html>

root@node2:~# curl 172.18.0.3
<html>
<head><title>Welcome to my webpage created by Ansible</title></head>
<body><h1>This webpage is served from node1 using Ansible</h1></body>
</html>
  
</pre>

**We can see that webapge is hosted on both node1 and node2.**

**Below code is optional and can be used when nginx is running on docker container**
<pre>
- name: Start nginx manually (container-friendly)
      shell: |
        nginx -g 'daemon off;' || true
</pre>
