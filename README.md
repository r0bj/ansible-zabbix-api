ansible Zabbix-API
==================

This module will let you synchronize ansible hosts state with Zabbix. It means that it sets hosts via Zabbix API according to ansible variables:
- groups which host should belongs to;
- templates which host should be linked to;
- macros which host should contains.

Groups and Tempalates provided by ansible variables MUST be already present in Zabbix.

Web access from nodes managed by ansible to the Zabbix API should be allowed (firewall).

You can treat ansible inventory as an authoritative source of hosts information and sync it to Zabbix.

Requirements
============

None.

Role Variables
==============

Available variables are listed below, along with default values (see `defaults/main.yml`):

    zabbix:
      default_group: ansible
      templates: []
      groups: []
      macros: ''

    zabbix_api:
      url: ''
      user: ''
      password: ''
      basic_auth_user: ''
      basic_auth_password: ''
      
- `zabbix.default_group` - Default Zabbix group which all hosts should belongs to. Hosts only from this group are considered during synchronization.
- `zabbix.templates` - Comma separated list of Zabbix templates which host should be linked to.
- `zabbix.groups` - Comma separated list of Zabbix groups which host should belongs to.
- `zabbix.macros` - Comma separated list of Zabbix macros which should be add to the host. Even items are macro key, odd items are macro value, eg.: '{$macro1},value1,{$macro2},value2'.

- `zabbix_api.url` - Zabbix API URL.
- `zabbix_api.user` and `zabbix_api.password` - Zabbix API credentials.
- `zabbix_api.basic_auth_user` and `zabbix_api.basic_auth_password` - Optional basic AUTH credentials if required.

Example
=======

Variables
---------

    zabbix_api:
      url: 'http://zabbixhost.com/api_jsonrpc.php'
      user: 'ansible'
      password: 'secretpassword'
  
    zabbix:
      default_group: ansible
      templates:
        - mysql
        - nginx
        - php-fpm
        - LXC Containers
        - Web Test
      groups:
        - LXC Containers
      macros: '{$PAGE_STRING},User logged,{$SNMP_COMMUNITY},public'
      
Playbook
--------

```yaml
- name: zabbix API
  hosts: all
  roles:
    - role: robj.zabbix-api
```

License
=======
MIT

Author Information
==================
This role was created in 2014 by Robert Jerzak.
