mysql
=========

Installs and configures mysql.

[![CI](https://github.com/Rheinwerk/ansible-role-mysql/actions/workflows/ci.yml/badge.svg)](https://github.com/Rheinwerk/ansible-role-mysql/actions/workflows/ci.yml)

Requirements
------------

None.

Role Variables
--------------

`_mysql` configures the whole role; cf. below or `defaults/main.yml`.

Dependencies
------------

None.

Example Playbook
----------------

```
---
- hosts: localhost
  connection: local
  become: yes
  vars:
    RW_APT_CACHE_UPDATE: yes
    MYSQL:
      default_config: no
      listen:
        ip: 127.0.0.1
        port: 3306
      root:
        password: "root"
      users:
        wordpress:
          state: present
          name: wordpress
          password: "wordpress"
          privileges: "wordpress.*:ALL,GRANT"
          hosts:
            - localhost
        backup:
          state: present
          name: backup
          password: "backup"
          privileges: '*.*:SELECT,LOCK TABLES,RELOAD,REPLICATION CLIENT'
          hosts:
            - localhost
      databases:
        wordpress:
          state: present
  roles:
    - { role: ansible-role-mysql, tags: ['mysql'], _mysql: "{{ MYSQL }}" }
```

License
-------

See LICENSE file.

Author Information
------------------

Initially created by Lukas Pustina [@drivebytesting](https://twitter.com/drivebytesting) as member of the [Rheinwerk](https://github.com/Rheinwerk) project.

