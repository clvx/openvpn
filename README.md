OpenVPN
=========

Role to install, configure and update OpenVPN servers and clients.

Future Work
-----------

- PAM support, *maybe?* 

Requirements
------------

- Ansible >= 2.1
- Ubuntu >= 16.04

Role Variables
--------------

| Variables | Default | Description |
| ----------- | ------- | ---------- |
| openvpn_port | 1194 | default port  |
| openvpn_proto | udp | default protocol |
| openvpn_server_dh | 2048 | dh keysize |
| openvpn_dir | /etc/openvpn | openvpn server directory |
| openvpn_keydir | "{{ openvpn_dir }}/keys" | openvpn server key directory |
| deploy_key_dir | "{{ role_path }}/files }}" | local key directory |
| local_openvpn_keydir | "{{ deploy_key_dir }}"  | local key directory, same as deploy_key_dir |
| openvpn_server_dh | "{{ lookup('pipe', 'basename {{ deploy_key_dir }}/dh*.pem | cut -d. -f1') }}"  | gets the dh key size dynamically |
| openvpn_tls_push | True | If true, it pushes secret.key to servers and clients |
| openvpn_is_client | False | If true, host is marked as client |
| openvpn_is_server | False | If true, host is marked as server |

Dependencies(Optional)
----------------------

This role works much better if you use clvx.easy-rsa to create your PKI.
- clvx.easy-rsa

Example Playbook
----------------

- Inventory 

    localhost

- group_vars/localhost.yml

        ---
        openvpn_is_client: True


or

        ---
        openvpn_is_server: True

YOU CAN NOT ASSIGN `openvpn_is_client` and `openvpn_is_server` AT THE SAME TIME
 OR IT WILL FAIL.

- Playbook 

    - hosts: lab-servers
      roles:
        - openvpn

    - hosts: lab-servers
      roles:
        - openvpn

License
-------

GPLv3

Author Information
------------------

Luis Michael Ibarra

clvx: Twitter, IRC, Reddit 
