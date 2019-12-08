[![Build Status](https://travis-ci.org/kleinstuff/ansible-zabbix-agent.png)](https://travis-ci.org/kleinstuff/ansible-zabbix-agent)

kleinstuff.zabbix-agent
=========

Install (by default) zabbix agent (4.3.x).
Currently supports:
* CentOS/RHEL 6/7
* OpenSuse/Suse Enterprise 12/15

Requirements
------------

No extra requirements needed.

Role Variables
--------------

Almost everything is setup by defaults/main.yml (you can check there and overrite in your vars).
But you need to set the address of your zabbix-server on "*ansible_zabbix_agent__ServerAddr*".

If you want to setup the hosts on the zabbix_server, you need to add another vars:
```yaml
# Activate the feature
ansible_zabbix_agent__add_hosts_to_server: True

# Add login/password to talk to the zabbix server
# Please use ansible-vault or other method to encrypt this values always
ansible_zabbix_server__login: "your zabbix server api user"
ansible_zabbix_server__password: "your zabbix server api password"

# Set the group(s) (you can set this per group_vars/host_vars/host)
ansible_zabbix_agent__Groups:
  - some_zabbix_group_name

# Set the template(s) (you can set this per group_vars/host_vars/host)
ansible_zabbix_agent__Templates:
  - "Template 1"
  - "Template 2"

```

Dependencies
------------

No deps.

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
