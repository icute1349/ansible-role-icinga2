[![Build Status](https://travis-ci.org/bashrc666/ansible-role-icinga2.svg?branch=master)](https://travis-ci.org/bashrc666/ansible-role-icinga2)

Ansible-Role-Icinga2
=======

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
```
  ansible-galaxy install geerlingguy.mysql
```

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
---
- hosts: localhost
  remote_user: root
  vars:
    icinga2_director: False
    icinga2_grafana: False
    icinga2_snmp_check: True
    icinga2_icingaweb2: True
    icinga2_database:
      name: icinga2
      user: icinga2
      password: icinga2dbpasswd
      host: localhost
    mysql_databases:
      - name: "{{ icinga2_database.name }}"
        encoding: utf8
        collation: utf8_general_ci
      - name: icingaweb2
        encoding: utf8
        collation: utf8_general_ci
      - name: director
        encoding: utf8
        collation: utf8_general_ci
    mysql_users:
      - name: "{{ icinga2_database.user }}"
        host: "{{ icinga2_database.host }}"
        password: "{{ icinga2_database.password }}"
        priv: "{{ icinga2_database.name }}.*:ALL"
      - name: "{{ icinga2_icingaweb2_database.user }}"
        host: "{{ icinga2_icingaweb2_database.host }}"
        password: "{{ icinga2_icingaweb2_database.password }}"
        priv: "icingaweb2.*:ALL"
      - name: director
        host: "localhost"
        password: directordbpasswd
        priv: "director.*:ALL"
  roles:
    -
      role: geerlingguy.mysql
    -
      role: geerlingguy.apache
    -
      role: ansible-role-icinga2
```

TODO
----

- Automate icingadirector 
[DOCS (https://github.com/Icinga/icingaweb2-module-director/blob/master/doc/03-Automation.md)]


License
-------

BSD

Author Information
------------------

gotoole/CAPENSIS - 2016
