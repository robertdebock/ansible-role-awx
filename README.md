awx
=========

<img src="https://docs.ansible.com/ansible-tower/3.2.4/html_ja/installandreference/_static/images/logo_invert.png" width="10%" height="10%" alt="Ansible logo" align="right"/>
<a href="https://travis-ci.org/robertdebock/ansible-role-awx"><img src="https://travis-ci.org/robertdebock/ansible-role-awx.svg?branch=master" alt="Build status" align="left"/></a>

Install and configure collectd on your system.

<img src="https://img.shields.io/ansible/role/d/29004"/>
<img src="https://img.shields.io/ansible/quality/29004"/>

Example Playbook
----------------

This example is taken from `molecule/resources/playbook.yml`:
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - robertdebock.awx
```

The machine you are running this on, may need to be prepared.
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.core_dependencies
    - role: robertdebock.epel
    - role: robertdebock.buildtools
    - role: robertdebock.python_pip
    - role: robertdebock.docker
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

Role Variables
--------------

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for awx

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

# The ports AWX should listen to.
awx_http_port: 80
awx_https_port: 443

# Details for rabbitmq
awx_rabbitmq_password: awxpass
awx_rabbitmq_erlang_cookie: cookiemonster

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
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.core_dependencies
- robertdebock.buildtools
- robertdebock.epel
- robertdebock.python_pip
- robertdebock.docker

```

This role uses the following modules:
```yaml
---
- assert
- command
- include
- include_tasks
- meta
- pause
- pip
- set_fact
- template
- tower_credential
- tower_inventory
- tower_job_template
- tower_organization
- tower_project
- tower_team
- tower_user
- unarchive
- uri
```

Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/awx.png "Dependency")


Compatibility
-------------

This role has been tested on these [container images](https://hub.docker.com/):

|container|allow_failures|
|---------|--------------|
|docker-alpine-openrc|yes|
|docker-alpine-openrc|yes|
|docker-centos-systemd|no|
|docker-centos-systemd|no|
|docker-debian-systemd|yes|
|docker-debian-systemd|yes|
|docker-debian-systemd|yes|
|docker-fedora-systemd|yes|
|docker-fedora-systemd|yes|
|opensuse/|no|
|docker-ubuntu-systemd|yes|
|docker-ubuntu-systemd|yes|
|docker-ubuntu-systemd|yes|

This role has been tested on these Ansible versions:

- ansible~=2.7
- ansible~=2.8
- git+https://github.com/ansible/ansible.git@devel

The indicator '~=' means [compatible with](https://www.python.org/dev/peps/pep-0440/#compatible-release). For example 'ansible~=2.8' would pick the latest ansible-2.8, for example ansible-2.8.5.




Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-awx) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-awx/issues)

To test this role locally please use [Molecule](https://github.com/ansible/molecule):
```
pip install molecule
molecule test
```

To test on Amazon EC2, configure [~/.aws/credentials](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html) and set a region using `export AWS_REGION=eu-central-1` before running `molecule test --scenario-name ec2`.

There are many specific scenarios available, please have a look in the `molecule/` directory.

License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/)
