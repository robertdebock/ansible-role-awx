awx
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-awx.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-awx)

The purpose of this role is to install and configure collectd on your system.

Example Playbook
----------------

This example is taken from `molecule/default/playbook.yml`:
```
---
- name: Converge
  hosts: all
  gather_facts: false
  become: true

  vars:
    python_pip_modules:
      - name: ansible

  roles:
    - robertdebock.bootstrap
    - robertdebock.epel
    - robertdebock.python_pip
    - robertdebock.awx

```

Role Variables
--------------

These variables are set in `defaults/main.yml`:
```
---
# defaults file for awx

# The version of AWX to install
awx_version: 2.0.1

# The default password for the user `admin`.
awx_admin_password: password

# The location where PostgreSQL should store its data.
awx_postgres_data_dir: /var/lib/pgdata
awx_postgres_database:
  database: awx
  username: awx
  password: awxpass
  port: 5432

# AWX uses a secret key to encrypt data. This value should be stored in vault.
awx_secret_key: awxsecret

# To update packages this role places on the system, set `awx_package_state` to `latest`.
awx_package_state: present

# When using the API, should the SSL be verified?
awx_tower_verify_ssl: no

# You can populate AWX using this structure.
# awx_organizations:
#  - name: demo
#    description: Demo organization
#    users:
#      - name: demo
#        password: demo
#        email: demo@example.com
#        first_name: De
#        last_name: Mo
#        superuser: true
#    teams:
#      - name: demo
#        description: Demo team
#    credentials:
#      - name: demo_ssh
#        description: demo ssh credentials
#        kind: ssh
#        username: demo
#        password: demo
#      - name: demo_scm
#        description: demo scm credentials
#        kind: scm
#        username: Null
#        password: Null
#    projects:
#      - name: demo
#        description: demo project
#        scm_credential: demo_scm
#        scm_type: git
#        scm_url: "https://github.com/robertdebock/ansible"
#    inventories:
#      - name: demo
#        description: demo inventory
#    job_templates:
#      - name: demo
#        description: demo_job_template
#        project: demo
#        playbook: ping.yml
#        inventory: demo
#        credential: demo_ssh
#        job_type: run

```

Requirements
------------

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the last 3 release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

---
- robertdebock.bootstrap
- robertdebock.buildtools
- robertdebock.epel
- robertdebock.python_pip


Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/awx.png "Dependency")


Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.4|ansible 2.5|ansible 2.6|ansible 2.7|ansible devel|
|------------|-----------|-----------|-----------|-----------|-------------|
|alpine-edge*|yes|yes|yes|yes|yes*|
|alpine-latest|yes|yes|yes|yes|yes*|
|archlinux|yes|yes|yes|yes|yes*|
|centos-6|no|no|no|no|no*|
|centos-latest|yes|yes|yes|yes|yes*|
|debian-latest|yes|yes|yes|yes|yes*|
|debian-stable|yes|yes|yes|yes|yes*|
|debian-unstable*|yes|yes|yes|yes|yes*|
|fedora-latest|yes|yes|yes|yes|yes*|
|fedora-rawhide*|yes|yes|yes|yes|yes*|
|opensuse-leap|yes|yes|yes|yes|yes*|
|opensuse-tumbleweed|yes|yes|yes|yes|yes*|
|ubuntu-artful|yes|yes|yes|yes|yes*|
|ubuntu-devel*|yes|yes|yes|yes|yes*|
|ubuntu-latest|yes|yes|yes|yes|yes*|

A single star means the build may fail, it's marked as an experimental build.

Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-awx) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-awx/issues)

To test this role locally please use [Molecule](https://github.com/metacloud/molecule):
```
pip install molecule
molecule test
```
There are many specific scenarios available, please have a look in the `molecule/` directory.

Run the [ansible-galaxy[(https://github.com/ansible/galaxy-lint-rules) and [my](https://github.com/robertdebock/ansible-lint-rules) lint rules if you want your change to be merges:
```
ansible-lint -r /path/to/galaxy-lint-rules/rules .
ansible-lint -r /path/to/ansible-lint-rules/rules .
```

License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
