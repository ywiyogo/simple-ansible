# Ansible initial setup for Debian VPS servers

## Terminology <sup>[1]</sup>

**Control node**: the host on which you use Ansible to execute tasks on the managed nodes

**Managed node**: a host that is configured by the control node

**Host inventory**: a list of managed nodes

**Ad-hoc command**: a simple one-off task

**Playbook**: a set of repeatable tasks for more complex configurations

**Module**: code that performs a particular common task such as adding a user, installing a package, etc.

## Basic Knowledge

The default configuration file of Ansible is /etc/ansible/ansible.cfg. The order in which a configuration file is located is as follows:

1. `ANSIBLE_CONFIG` (environment variable)
2. ansible.cfg (per directory)
3. ~/.ansible.cfg (home directory)
4. /etc/ansible/ansible.cfg (global)

## Preparation

* Install Ansible on the control node laptop/PC: `sudo apt install ansible`
* Check the hostname and the IP of the managed nodes/servers to connect with the SSH.

## 1. Creating *ansible.cfg*

```
[defaults]
inventory = hosts
remote_user = root
```

## 2. Create *hosts* file

```
[groupname]
hostname
```
## 3. Check connection to all hosts

* Copy the public key to all server node, e.g.: `ssh-copy-id -i ~/.ssh/wiyogo_gitlab_hyperstaking_ed25519.pub root@conta-us1`
* Check the connection with `ansible all -m ping`. Without copying the publkic key use: `ansible all -m ping --ask-pass`

## 5. Create the playbook.yml

If the tasks are too long, they can be split into different roles.
Features:
* New user creation
* SSH hardening
* Setup ufw firewall to open SSH

## 6. Run

`ansible-playbook playbook.yml --extra-vars "newuser=XXX, upasswd=XXX" -v`

[//]: # (References)
[1]: https://www.redhat.com/en/blog/system-administrators-guide-getting-started-ansible-fast?extIdCarryOver=true&sc_cid=701f2000001OH7YAAW