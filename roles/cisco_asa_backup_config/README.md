cisco_asa_backup_config
=======================

A role that creates backups of Cisco ASA configurations.
The role works with ASAs both with and without security contexts.

The filename of the backup is *hostname-context.cfg*. The hostname is taken from the Ansible inventory, while the name of the context is taken from running-config.

Requirements
------------

This role requires the [asa command module](https://docs.ansible.com/ansible/latest/collections/cisco/asa/asa_command_module.html), which can be installed by `ansible-galaxy collection install cisco.asa`.
The asa_command_module is installed automatically if you installed this role by installing the cisco_backup collection by issuing `ansible-galaxy collection install conoa.cisco_backup`.

Role Variables
--------------

#### cabc_backup_destination:
This variable provides the directory name in which the backup configuration file(s) will be stored. If the directory does not exist, it will be created.
If the variable is not given, a backup directory named `backup` will be created in the current working directory and backups will be copied to that directory.

Example Playbook
----------------

```
---
- hosts: all
  gather_facts: no
  tasks:
    - import_role:
        name: conoa.cisco_backup.cisco_asa_backup_config

  vars:
    cabc_backup_destination: /tmp/asa_backups/
```

Example Inventory
-----------------

```
[ciscoasa]
ciscoasa01 ansible_host=192.168.0.1

[ciscoasa:vars]
ansible_connection=ansible.netcommon.network_cli
ansible_network_os=cisco.asa.asa
ansible_user=cisco
ansible_password=cisco
ansible_become_password=cisco
```

License
-------

BSD Zero Clause License

Author Information
------------------

Written by [Farid Joubbi](https://github.com/faridjoubbi) - Conoa AB - https://conoa.se
