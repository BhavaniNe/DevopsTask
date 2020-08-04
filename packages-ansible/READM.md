## Role info

> Ansible Role to Install telnet, nslookup,java, curl, firewalld on CentOS Linux.


## Tested on the following operating systems

- CentOS 7
- CentOS 7 Ec2 instances

## Tasks in the role

This role contains tasks to:

- Install  firewalld
- Install Packages
- Install java
- Start & enable firewalld , Telnet

## How to use this role

- Clone the Project:

```
$ git clone https://github.com/jmutai/tomcat-ansible.git
$ cd packages-ansible

- Update your inventory, e.g:

```
$ vi hosts
[host]
172-31-33-101       # Remote user to act on
```

If you are using non root remote user, then set username and enable sudo:

```
become: yes
become_method: sudo
```

## Running Playbook

Once all values are updated, you can then run the playbook against your nodes.

```
$ ansible-playbook -i inventory packages.yml
