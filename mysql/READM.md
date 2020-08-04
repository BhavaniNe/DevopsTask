## Role info

> Ansible Role to Install Mysql on CentOS Linux.


## Tested on the following operating systems

- CentOS 7
- CentOS 7 Ec2 instances

## Tasks in the role

This role contains tasks to:

- Install Mysql

## How to use this role

- Clone the Project:

```
$ git clone https://github.com/jmutai/tomcat-ansible.git
$ cd packages-ansible



- Update your inventory, e.g:

```
$ vi hosts
[host]
172-31-33-101      # Remote user to act on
```

- Update variables in playbook file - Set Tomcat version, remote user and Tomcat UI access credentials

```
$ vi mysql-setup.yml
---
- name: Configure remote machines
  hosts: host
  become: yes
  gather_facts: yes
  vars:
     user_name: centos
     ansible_ip : 54.179.140.135
     dbname : employ
     passwd_mysql_root : Admin@123
     passwd_mysql_app_user : Admin@123
  tasks:

   - name: Include tasks for packages installation on specific distribution
     include_tasks: "tasks/packages/centos.yaml"

   - name: Include common tasks for configuration
     include_tasks: "tasks/packages/common.yaml"

   - name: Include tasks for MySQL server installation on specific distributions
     include_tasks: "tasks/mysql/centos.yaml"
  
   - name: Include common tasks for MySQL server configuration
     include_tasks: "tasks/mysql/common.yaml"
```

If you are using non root remote user, then set username and enable sudo:

```
become: yes
become_method: sudo
```

## Running Playbook

Once all values are updated, you can then run the playbook against your nodes.

```
$ ansible-playbook -i inventory mysql_setup.yml
