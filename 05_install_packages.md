**Day 05 — Install Common Packages**

**Objective: Install utilities (curl, git, htop) on all nodes.**

**Create file: playbooks/05_install_packages.yml**

<pre>
- name: Install common packages
  hosts: all
  become: yes
  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes
        cache_valid_time: 3600

    - name: Install utilities
      apt:
        name:
          - curl
          - git
          - htop
        state: present
</pre>
**Run:**

**ansible-playbook 05_install_packages.yml -i /root/ansible-labs/hosts.ini**
<pre>
root@control:~/ansible-labs/playbooks# ansible-playbook 05_install_packages.yml -i /root/ansible-labs/hosts.ini

PLAY [Install curl, git and htop] ***************************************************************************************************

TASK [Gathering Facts] **************************************************************************************************************
ok: [node3]
ok: [node1]
ok: [node2]

TASK [Update the apt package cache] *************************************************************************************************
[WARNING]: Updating cache and auto-installing missing dependency: python3-apt
ok: [node3]
ok: [node2]
ok: [node1]

TASK [Install curl, git and htop] ***************************************************************************************************
changed: [node1]
changed: [node2]
changed: [node3]

PLAY RECAP **************************************************************************************************************************
node1                      : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node2                      : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node3                      : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
</pre>

**Verify:**

<pre>
root@control:~/ansible-labs/playbooks# ansible -i /root/ansible-labs/hosts.ini all -m shell -a "which git && git --version" -o
node3 | CHANGED | rc=0 | (stdout) /usr/bin/git\ngit version 2.34.1
node2 | CHANGED | rc=0 | (stdout) /usr/bin/git\ngit version 2.34.1
node1 | CHANGED | rc=0 | (stdout) /usr/bin/git\ngit version 2.34.1
root@control:~/ansible-labs/playbooks# ansible -i /root/ansible-labs/hosts.ini all -m shell -a "which curl && curl --version" -o
node2 | CHANGED | rc=0 | (stdout) /usr/bin/curl\ncurl 7.81.0 (x86_64-pc-linux-gnu) libcurl/7.81.0 OpenSSL/3.0.2 zlib/1.2.11 brotli/1.0.9 zstd/1.4.8 libidn2/2.3.2 libpsl/0.21.0 (+libidn2/2.3.2) libssh/0.9.6/openssl/zlib nghttp2/1.43.0 librtmp/2.3 OpenLDAP/2.5.19\nRelease-Date: 2022-01-05\nProtocols: dict file ftp ftps gopher gophers http https imap imaps ldap ldaps mqtt pop3 pop3s rtmp rtsp scp sftp smb smbs smtp smtps telnet tftp \nFeatures: alt-svc AsynchDNS brotli GSS-API HSTS HTTP2 HTTPS-proxy IDN IPv6 Kerberos Largefile libz NTLM NTLM_WB PSL SPNEGO SSL TLS-SRP UnixSockets zstd
node1 | CHANGED | rc=0 | (stdout) /usr/bin/curl\ncurl 7.81.0 (x86_64-pc-linux-gnu) libcurl/7.81.0 OpenSSL/3.0.2 zlib/1.2.11 brotli/1.0.9 zstd/1.4.8 libidn2/2.3.2 libpsl/0.21.0 (+libidn2/2.3.2) libssh/0.9.6/openssl/zlib nghttp2/1.43.0 librtmp/2.3 OpenLDAP/2.5.19\nRelease-Date: 2022-01-05\nProtocols: dict file ftp ftps gopher gophers http https imap imaps ldap ldaps mqtt pop3 pop3s rtmp rtsp scp sftp smb smbs smtp smtps telnet tftp \nFeatures: alt-svc AsynchDNS brotli GSS-API HSTS HTTP2 HTTPS-proxy IDN IPv6 Kerberos Largefile libz NTLM NTLM_WB PSL SPNEGO SSL TLS-SRP UnixSockets zstd
node3 | CHANGED | rc=0 | (stdout) /usr/bin/curl\ncurl 7.81.0 (x86_64-pc-linux-gnu) libcurl/7.81.0 OpenSSL/3.0.2 zlib/1.2.11 brotli/1.0.9 zstd/1.4.8 libidn2/2.3.2 libpsl/0.21.0 (+libidn2/2.3.2) libssh/0.9.6/openssl/zlib nghttp2/1.43.0 librtmp/2.3 OpenLDAP/2.5.19\nRelease-Date: 2022-01-05\nProtocols: dict file ftp ftps gopher gophers http https imap imaps ldap ldaps mqtt pop3 pop3s rtmp rtsp scp sftp smb smbs smtp smtps telnet tftp \nFeatures: alt-svc AsynchDNS brotli GSS-API HSTS HTTP2 HTTPS-proxy IDN IPv6 Kerberos Largefile libz NTLM NTLM_WB PSL SPNEGO SSL TLS-SRP UnixSockets zstd
root@control:~/ansible-labs/playbooks# ansible -i /root/ansible-labs/hosts.ini all -m shell -a "which htop && htop --version" -o
node1 | CHANGED | rc=0 | (stdout) /usr/bin/htop\nhtop 3.0.5
node3 | CHANGED | rc=0 | (stdout) /usr/bin/htop\nhtop 3.0.5
node2 | CHANGED | rc=0 | (stdout) /usr/bin/htop\nhtop 3.0.5
</pre>

**We can see git, curl and htop are installed in all 3 nodes.**
