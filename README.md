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
