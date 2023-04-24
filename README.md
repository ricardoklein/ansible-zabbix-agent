[![Build Status](https://travis-ci.org/kleinstuff/ansible-zabbix-agent.png)](https://travis-ci.org/kleinstuff/ansible-zabbix-agent)

kleinstuff.zabbix-agent
=========

Install (by default) zabbix agent (6.4).
Currently supports:
* OpenSuse/Suse Enterprise 15

Requirements
------------

collections:
  - name: community.zabbix
    version: 1.9.3
  - name: ansible.posix
    version: 1.3.0
  - name: community.general
    version: 3.7.0


Role Variables
--------------

Almost everything is setup by defaults/main.yml (you can check there and overrite in your vars).
But you need to set the address of your zabbix-server on "*ansible_zabbix_agent__ServerAddr*".

If you want to setup the hosts on the zabbix_server, you need to add another vars:
```yaml
# Activate the feature
ansible_zabbix_agent__add_hosts_to_server: True

# Add API Token to talk to the zabbix server
# Please use ansible-vault or other method to encrypt this values always
ansible_zabbix_agent__Server_auth_key: "your_super_secret_token"

# Set the group(s) (you can set this per group_vars/host_vars/host)
ansible_zabbix_agent__Groups:
  - some_zabbix_group_name

# Set the template(s) (you can set this per group_vars/host_vars/host)
ansible_zabbix_agent__Templates:
  - "Template 1"
  - "Template 2"

# OPTIONAL Set host Macros
ansible_zabbix_agent__zabbix_macros:
  - { macro: "{$A_MACRO}", value: "{{ a_host_var }}" }
  - { macro: "{$ANOTHER_MACRO}", value: "a-simple-string" }
  - { macro: "{$CONFIGURED_BY}", value: "Ansible" }

# OPTIONAL Set host TAGs
ansible_zabbix_agent__zabbix_tags:
  - "OneTag"
  - "AnotherTag"

```

By default, we set the hostname of the monitored machine as ``` {{ ansible_host }} ```
But you can override this setting this ``` ansible_zabbix_agent__Hostname ``` per host.

Dependencies
------------

collections:
  - name: community.zabbix
    version: 1.9.3
  - name: ansible.posix
    version: 1.3.0
  - name: community.general
    version: 3.7.0

Example Playbook
----------------

```
    - hosts: servers
      roles:
         - { role: kleinstuff.zabbix-agent, ansible_zabbix_agent__ServerAddr: 'youzabbixserver.example.com' }
```
License
-------

GPL

Author Information
------------------

If you want to suggest changes or request new features, please feel free to create a issue or send a pull request.
