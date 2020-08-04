## Role info

> Ansible Role to Install Oracle JDK on CentOS Ec2 instances Linux.


## Tested on the following operating systems

- CentOS 7
centos 7 ec2instances

## Tasks in the role

This role contains tasks to:

- Install Oracle JDK

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
$ vi tomcat-setup.yml
---
- hosts: host
  become: yes
  vars:
    tomcat_archive_url: https://apachemirror.sg.wuchna.com/tomcat/tomcat-9/v{{ tomcat_ver }}/bin/apache-tomcat-{{ tomcat_ver }}.tar.gz
    tomcat_archive_dest: /tmp/apache-tomcat-{{ tomcat_ver }}.tar.gz
    tomcat_ver: 9.0.37
    Java_home: /usr/lib/jvm/java-1.8.0-openjdk/bin/java
    owner : centos
    group : centos   
    ui_manager_user: manager                    # User who can access the UI manager section only
    ui_manager_pass: SP@ssw0rd      # UI manager user password
    ui_admin_username: admin                    # User who can access bpth manager and admin UI sections
    ui_admin_pass: SP@ssw0rd          # UI admin password
  tasks:
      - include: "tasks/main.yaml"
```

If you are using non root remote user, then set username and enable sudo:

```
become: yes
become_method: sudo
```

## Running Playbook

Once all values are updated, you can then run the playbook against your nodes.

```
$ ansible-playbook -i inventory Install_oraclejdk.yml
