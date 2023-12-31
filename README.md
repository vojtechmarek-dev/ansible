# Ansible
Repository for storing personal ansible playbooks (mainly for setting up personal home server)

Ansible automates the management of remote systems and controls their desired state. It is better to read official documentation. Ansible in its clear form has the following components:

Control node - a computer, that has Ansible installed and is used to manage all hosts.
Managed node - a remote computer (host), that Ansible manages.

There are many tools that automates host management via Ansible, but in its clear form, Ansible is a set of command line tools, that needs to be executed manually.

# Why
With the intention to learn ansible and server managment without any crutches I wanted to setup a home server but with every step documented in Ansible playbooks. 

Therefore I can easilly replicate the set-up on new server (I am using RPi 4 as my "training" server).


This playbook is used to easily setup a basic Debian Server with . I've added a few more roles to this playbook since then. You can modify your site.yml file and select the roles which suit your needs.

# Getting started

0. Prerequisites

- Python3 installed on the Control node
- Python3 installed on the Managed node. 

1. Install Ansible
```BASH
sudo python3 -m pip install --upgrade pip
pip install --user ansible
```
For more detailed installation instructions see [installation guide](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installation-guide).

:warning: If the Ansible commands are still not accessible, try adding your Python user bin directory to your PATH, e.g. for macOS, this can be configured in `~/.bash_profile`

```
echo "export PATH=\"`python3 -m site --user-base`/bin:\$PATH\"" >> ~/.bash_profile
```

# Playbooks
There are two two main playbooks:
- `server.yml` - main playbook thats configures server - uses most roles @see server_roles Todo
- `user.yml` - user access playbook that creates my user and adds to sudoers group
    
    :warning: For obvious security risks - this playbook's tasks has all sensitive data (passwords, authorized keys) stored elsewhere (i.e. not in this repository) it references var secrets, playbook should be run as follows:
    
    ```
    ansible-playbook -i inventory.ini -i ../ansible-secrets/secrets.yml user.yml --ask-vault-pass
    ``` 

# Roles
Playbooks currently includes the following roles:

- base: represents basic configuration of Linux Debian server