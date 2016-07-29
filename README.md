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

## Dependencies

### Test Kitchen dependencies

* Virtualbox
* Vagrant
* Ruby 2.*
* test-kitchen gem
* kitchen-vagrant gem
* kitchen-ansible gem

## Test Kitchen

The role comes with a test environment built with *Test Kitchen*.

First, you have to create your VM:

```
$ kitchen create
```

Then it's time to apply your changes by running:

```
$ kitchen converge
```

You can check either your user or database by logging in the VM:

```
$ kitchen login
Welcome to Ubuntu 14.04.4 LTS (GNU/Linux 3.13.0-86-generic x86_64)

 * Documentation:  https://help.ubuntu.com/
Last login: Fri Jul 29 14:21:09 2016 from 10.0.2.2
vagrant@default-ubuntu-1404:~$ sudo mysql
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 47
Server version: 5.5.50-0ubuntu0.14.04.1 (Ubuntu)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| test               |
+--------------------+
4 rows in set (0.00 sec)

mysql> SELECT User FROM mysql.user;
+------------------+
| User             |
+------------------+
| root             |
| root             |
| root             |
| debian-sys-maint |
| root             |
| test             |
+------------------+
6 rows in set (0.01 sec)
mysql> SHOW GRANTS FOR 'test'@'localhost';
+-------------------------------------------------------------------------------------------------------------+
| Grants for test@localhost                                                                                   |
+-------------------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'test'@'localhost' IDENTIFIED BY PASSWORD '*94BDCEBE19083CE2A1F959FD02F964C7AF4CFC29' |
| GRANT ALL PRIVILEGES ON `test`.* TO 'test'@'localhost' WITH GRANT OPTION                                    |
+-------------------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)
```

When you're done with your tests, you can destroy your test environment by typing:

```
$ kitchen destroy
```

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
