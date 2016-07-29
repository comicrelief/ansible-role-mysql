# ansible-role-mysql

An Ansible role that manages MySQL databases and users

## Requirements

none

## Role Variables

**mysql_dependencies** - List of dependencies required by Ansible to use the MySQL module.

Default deps listed below:

* python-dev
* libmysqlclient-dev
* python-pip
* mysql-client

**mysql_pip_packages** - List of *pip* packages required by Ansible to run this Role.

Default packages listed below:

* MYSQL-python

## Default Variables

**mysql_users** - Dictionary of MySQL users to be added to your host.

Below a list of required properties:

* name - user name
* password - user password
* state - whether the user is present or absent

Below a list of optional properties:

* priv - user MySQL privilegies(default: *\*.\*:ALL,GRANT*)
* append_privs - boolean value which decides whether the privs have to be appended or not (default: *no*)
* host - user database's host (default: *localhost*)
* login_host - host running the database (default: *localhost*)
* login_user - username used to authenticate with database's host (default: *''*)
* login_password - login_user's password (default: *''*)
* login_port - login_host's port (default: *3306*)

**mysql_db** - Dictionary of MySQL databases to be addedd to your host.

Below a list of required properties:

* name - database name
* state - whether the database is present or absent

Below a list of optional properties:

* login_host - host running the database (default: *localhost*)
* login_user - username used to authenticate with database's host (default: *''*)
* login_password - login_user's password (default: *''*)
* login_port - login_host's port (default: *3306*)

## dependencies

None.

## Example Playbook

```
---

- hosts: mysql-server
  roles:
    - ansible-role-mysql
```

## License

MIT / BSD    

## Author Information

This role was created in 2016 by [Davide Di Mauro](github.com/davidedimauro88).
