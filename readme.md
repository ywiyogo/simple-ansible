# A Simple Ansible Project for Beginner

This repository provides a simple example how to learn Ansible to automate the server setup. My experience learning Ansible shows that separating the task in different folders creates a huge confusion. Thus, this Ansible project centralizes all the tasks in the [playbook.yml](./playbook.yml) file to avoid confusion during navigating the tasks. The available servers are structured and listed in the [hosts.yml](./hosts.yml) file. The file [./vars/default.yml](./vars/default.yml) provides the list of the OS setup and its software packages that will be installed.

This Ansible setup is mainly prepared for an initial docker and kubernetes setup for different VPSs and single board computers. For another usecases please refer to the official documentation<sup>[1]</sup>.

## Terminology 

The terms are synced to the RedHat Guide<sup>[2]</sup>.

**Control node**: the host on which you use Ansible to execute tasks on the managed nodes

**Managed node**: a host that is configured by the control node

**Host inventory**: a list of managed nodes

**Ad-hoc command**: a simple one-off task

**Playbook**: a set of repeatable tasks for more complex configurations

**Module**: code that performs a particular common task such as adding a user, installing a package, etc.

## Basic Knowledge

The default configuration file of Ansible is `/etc/ansible/ansible.cfg`. The order in which a configuration file is located is as follows:

1. `ANSIBLE_CONFIG` (environment variable)
2. ansible.cfg (per directory)
3. ~/.ansible.cfg (home directory)
4. /etc/ansible/ansible.cfg (global)

## Start from Scratch

* Install Ansible on the control node laptop/PC: `sudo apt install ansible`
* Check the hostname and the IP of the managed nodes/servers to connect with the SSH.

### 1. Creating *ansible.cfg*

```
[defaults]
inventory = hosts
remote_user = root
```

### 2. Create *hosts* file

```
[groupname]
hostname
```
### 3. Check connection to all hosts

* Without copying the public key use: `ansible all -m ping --ask-pass`
* (optional) If the public key has been copied to the servers, check the connection with `ansible all -m ping`. 
 

### 4. Create the playbook.yml

If the tasks are too long, they can be split into different roles.
Features:
* New user creation
* SSH hardening
* Setup ufw firewall to open SSH

### 5. Run

Running initial new server with root user with the parameter `-u root` :

```
ansible-playbook playbook.yml -u root -k -v --extra-vars "newuser=<username> upasswd=<usr_passwd>"
```

Running an update after the initialitaion with a new user:
```
ansible-playbook playbook.yml --extra-vars "newuser=<username> upasswd=<usr_passwd>" -v
```

[//]: # (References)
[1]: https://docs.ansible.com/ansible/latest/user_guide/index.html
[2]: https://www.redhat.com/en/blog/system-administrators-guide-getting-started-ansible-fast?extIdCarryOver=true&sc_cid=701f2000001OH7YAAW