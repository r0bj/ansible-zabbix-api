ansible Zabbix-API
==================

This module will let you synchronize ansible hosts state with Zabbix. It means that it sets hosts via Zabbix API according to ansible variables:
-   groups which host should belongs to;
-   templates which host should be linked to;
-   macros which host should contains.

Groups and Tempalates provided by ansible variables MUST be already present in Zabbix.

Web access from nodes managed by ansible to the Zabbix API should be allowed (firewall).

Make sure API user for provided credentials has enough permissions for host groups in Zabbix.

You can treat ansible inventory as an authoritative source of hosts information and sync it to Zabbix.

Tested on Zabbix 2.4.1.

Requirements
============

None.

Role Variables
==============

Available variables are listed below, along with default values (see `defaults/main.yml`):

- `zabbix_default_group` - Default Zabbix group which all hosts should belongs to. Hosts only from this group are considered during synchronization (default "ansible").
- `zabbix_templates` - Comma separated list of Zabbix templates which host should be linked to.
- `zabbix_groups` - Comma separated list of Zabbix groups which host should belongs to.
- `zabbix_macros` - Comma separated list of Zabbix macros which should be add to the host. Even items are macro key, odd items are macro value, eg.: '{$macro1},value1,{$macro2},value2'.
- `zabbix_url` - Zabbix API URL.
- `zabbix_user` and `zabbix_password` - Zabbix API credentials.
- `zabbix_basic_auth_user` and `zabbix_basic_auth_password` - Optional basic AUTH credentials if required.

Example
=======

Variables
---------

    zabbix_url: 'http://zabbixhost.com/api_jsonrpc.php'
    zabbix_user: 'ansible'
    zabbix_password: 'secretpassword'
  
    zabbix_templates: 'mysql,nginx,php-fpm,LXC Containers,Web Test'
    zabbix_groups: 'LXC Containers,Webservers'
    zabbix_macros: '{$PAGE_STRING},User logged,{$SNMP_COMMUNITY},public'

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
