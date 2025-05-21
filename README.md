kleinstuff.zabbix-agent
=========

Install zabbix agent (defaults to version 7.2).
Currently supports:
* OpenSuse/Suse Enterprise 15

Requirements
------------

Only a few Collections are necessary (see dependencies).

Role Variables
--------------

Almost everything is setup by defaults/main.yml (you can check there and overrite in your vars).
But you need to set the address of your zabbix-server on "*ansible_zabbix_agent__ServerAddr*".

If you want to setup the hosts on the zabbix_server, you need to add another vars:
```yaml
# (OPTIONAL) Service name, you can set this to "zabbix_agentd" in case you have
# a older package version, like in case you are installing this in raspberrypi
zabbix_service_name: "zabbix-agent"

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

If you use openSUSE Tumbleweed, the default package (as of 20230604) still names
zabbix service `zabbix_agentd` instead of `zabbix-agent`, so you need to set on your
host_vars the follow:
`zabbix_service_name: "zabbix_agentd"`

Dependencies
------------

collections:
  - name: community.zabbix
    version: 3.3.0
  - name: ansible.posix
    version: 2.0.0
  - name: community.general
    version: 10.7.0

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
