# Ansible Essentials

## Introduction to Ansible

## What is Ansible and the Ansible Way

* Ansible is an automation language (declarative, generally yml) that describes IT Application infrastructure in **Ansible Playbooks**
* Ansible Playbooks run on an automation engine.
* **Ansible Towers** - Enterprise framework for controlling, securing and managing the Ansible Automation with UI and RESTful API.

### Ansible is simple
* Human readable automation
* No special coding skill needed
* Sequential task assignment
* Improves productivity

### Ansible is powerful
* Application deployment
* Configuration Managemnt
* Workflow Orchestration
* Orchestrate the Application Lifecycle

### Ansible is Agentless
* Agentless architecture
* Uses OpenSSH and WinRM
* No agents to exploit or update
* Efficient and Secure

### Ansible is Cross Platform

### Ansible is compatible with existing toolkits
* Comes bundeled with 450 modules

### Community - GitHub Community

### Ansible is the complete Package
1. Configuration Management
2. Application Deployment
3. Multi-Tier Orchestration
4. Provisioning

**Configuration Management or State Management:** Setup base state for the device with all dependencies and configurations.
* Security
* Compliance
* Orchestration
* Continuous delivery
* Provisioning

### Installing Ansible
```
$ sudo apt-get install ansible
```
or
```
$ sudo yum install ansible
```
or
```
$ pip install ansible
```

## How Ansible Works

![Ansible Architecture](img/1.png)

* Users create Ansible Playbook

**Ansible Playbooks:** Declarative language called YAML (Yet Another Markup Language)
Ansible Playbooks invoke **Ansible Modules**

### Ansible Automation Engine
1. Inventory
2. Modules
3. API
4. Plugins

**Modules:** Tools in the Toolkit
Written in Python, Powershell etc.

**Inventory:** Modules are stored on nodes or groups.

**Infrastrucute:** Nodes and groups must be stored somewhere ((Public/Private Cloud))
- Cloud
- Custom CMDB

**Plugins:** Code that plugs into core engine

**Commonly used modules** - 450 total
1. copy
2. file
3. apt
4. yum

https://docs.ansible.com/ansible/latest/modules/modules_by_category.html

**Run command modules**
1. command: execute command but not via shell - direct and secure
2. Shell: execute command through a shell like bash
3. Script: local script execution on remote node
4. Raw: execure command without going through Ansible module subsystem - pure ssh command without Python use case.

## Ad-hoc commands and Demonstration

* Check all hosts are up 
```
$ ansible all -m ping # -m is used to pass commands to ansible
```
```
$ ansible all -i [inventory file] -u [host file name] -m ping # -i is used to pass Inventory file to Ansible, -u is used to pass the host/node type or name
```
Eg: `$ ansible all -i hosts -u vagrant -m ping`


* Check the uptime of all hosts in a specific group
```
$ ansible [group name] -m command -a "uptime" # Command with argument uptime $ command uptime
```

* Check localhost configuration
```
$ ansible localhost -m setup
```

* We know that all commands and modules run on inventory - hosts (nodes) or groups (collection of hosts)

**Inventory:** Collection of hosts against which Ansible can work with.
* Hosts - network devices/ containers/ nodes etc.
* Groups
* Static or Dynamic source
* Inventory specific data

* Check inventory details - groups and IP address of each node is shown
```
$ cat [hosts file]
```

* Gather machine information
```
$ ansible all -i hosts -u vagrant -m setup
```

* Install packages
```
$ ansible [group name/all] -i hosts -u vagrant -m yum -a "name=httpd state=present" -b # a for arguments and b for assigning permission to vagrant user
```

**Generic Ansible command**
```
$ ansible [group name/all] -i [inventory file] -u [hosts] -m [command name] -a [arguments to the command]
```

* Ansible is Idempotent - Re-running same command checks for previous state and does not repeat tasks

* Delete Packages
```
$ ansible [group name/all] -i hosts -u vagrant -m yum -a "name=<package> state=absent" -b
```

