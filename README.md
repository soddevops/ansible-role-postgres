ansible-role-postgres
=====================

![](https://github.com/kevincoakley/ansible-role-postgres/workflows/Molecule%20Test/badge.svg)

Install Postgres 10, 11, 12, 13, 14, 15, & 17. Tested with Postgres 10-15 and CentOS/RHEL 8, Ubuntu 20.04 & Ubuntu 22.04. Postgres 17 support added for EL8/EL9.

Notes for EL8/EL9
-----------------

- This role uses the upstream PostgreSQL Global Development Group (PGDG) yum repository by installing the `pgdg-redhat-repo` RPM for the target EL major version. For EL9 this uses the same RPM location pattern as EL8; the role installs the RPM from: `https://download.postgresql.org/pub/repos/yum/reporpms/EL-<major>-x86_64/pgdg-redhat-repo-latest.noarch.rpm`.
- On EL8 and EL9 the OS ships modular streams for PostgreSQL; the role disables the distro `postgresql` module via `dnf module disable postgresql` before installing the PGDG packages so the expected PG packages can be installed.

Requirements
------------

None

Role Variables
--------------

See defaults/main.yml and the example inventory below

Dependencies
------------

None

Example Playbook
----------------
  
    - name: Postgres role 
      hosts: postgres
      become: yes
      become_method: sudo
    
      vars:
        - postgres_listen_addresses: "*"
        - postgres_client_auth:
          - type: host
            database: all
            user: all
            address: 0.0.0.0/0
            method: md5
          - type: local
            database: all
            user: all
            method: md5
    
      roles:
        - ansible-role-postgres
    
      tags:
        - postgres

License
-------

BSD

Author Information
------------------

Kevin Coakley (https://github.com/kevincoakley)