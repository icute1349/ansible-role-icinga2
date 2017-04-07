[![Build Status](https://travis-ci.org/bashrc666/ansible-icinga2.svg?branch=master)](https://travis-ci.org/bashrc666/ansible-icinga2)

Icinga2
=========

This role is compatible by settings var and role with :

 - Influxdb
 - manubulon snmp-plugin
 - Icingaweb2


Install of Icingaweb2

 - After install you will need to setup requirement above and finish the install at http://IP/icingaweb2/setup

Compatibility
-------------
 - CentOS6
 - CentOS7

Requirements
------------

- Mysql roles


For CentOS :
 - Disable selinux or make your own policies
 - if icingaweb2 set date.timezone in php.ini

ansible >= 2.1.2

Role Variables
--------------

```
# [[ Icingaweb2 ]]
    icinga2_icingaweb2: boolean
    icinga2_icinga2influxdb: boolean
    icinga2_icinga_snmp_check: boolean
    icinga2_icinga2influxdb: boolean
```

Dependencies
------------

### On remote Host

Everything will be installed by roles if it's not installed

Example Playbook
----------------

```
- hosts: all
  become: yes
  vars:
# [[ Icingaweb2 ]]
    icinga2_icingaweb2: True
    icinga2_icinga_snmp_check: True
    icinga2_icinga2influxdb: True
# [[ Roles Def ]
  roles:
    - icinga2
```

License
-------

BSD

Author Information
------------------

gotoole/CAPENSIS - 2016
