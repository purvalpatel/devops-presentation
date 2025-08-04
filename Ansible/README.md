Ansible Architecture:
---------------------
![image info](Ansible-architecture.png)

Ansible installation:
---------------------
For ubuntu:

```bash
apt-get update
apt-get install ansible-core
```
verify installation:

`ansible --version`

Setup inventory:
----------------

Create directory:
```bash
mkdir -p /etc/ansible/inventory
```
Create inventory file:
nano /etc/ansible/inventory/hosts.ini
```yaml
[web]
10.10.110.24

[diff_ssh_port]
#server12 ansible_host=10.10.110.12 ansible_user=root ansible_port=2222
```

Verify inventory:
```
ansible-inventory -i /etc/ansible/inventory/hosts --list
```

Ping group in your inventory:
```
ansible web -m ping -i /etc/ansible/inventory/hosts
```

How to set public key authentication ?

Basics of Yaml:
--------------
YAML - Human readable language mostly used for writing configuration files.

Key-Value pairs:
```yaml
vars:
  username: dev_user
  server: 127.0.0.1
```

Lists:
```yaml
packages:
  - nginx
  - git
  - curl
```
Dictionaries (Nested Key-value):
```yaml
vars:
  user_info:
    name: devuser
    shell: /bin/bash
```

Creating Playbook:
------------------
Ansible playbook Syntax:
```
- name: My first play
  hosts: myhosts
  tasks:
   - name: Ping my hosts
     ansible.builtin.ping:

   - name: Print message
     ansible.builtin.debug:
       msg: Hello world
```

Task 1: Install packages:
install_package.yaml
```yaml
- name: install nginx on servers
  hosts: all

  tasks:
  - name: Install nginx
    apt:
      name: nginx
      state: present

```
Apply:
```
ansible-playbook install_package.yaml -i /etc/ansible/hosts
```

It failed!!! Due to connection with the host.
10.10.20.104               : ok=0    changed=0    unreachable=1    failed=0    skipped=0    rescued=0    ignored=0

Task 2: Create directory

create_directory.yaml
```yaml
---
- name: Create directory on remote hosts
  hosts: all
  become: true      ## Run as sudo/root

  tasks:
    - name: Ensure directory exists
      file:
        path: "/tmp/mydir"
        state: directory
        mode: '0755'
```
Run playbook for apply changes:

```
ansible-playbook create_directory.yaml -i /etc/ansible/inventory/hosts
```

Managing Tasks using Tags and Variables:
--------------

Tags:

task_tag.yaml
```yaml
tasks:
  - name: Install nginx
    apt:
      name: nginx
      state: present
    tags: install

  - name: Start nginx
    service:
      name: nginx
      state: started
    tags: start
```

How to use:
```
ansible-playbook create_directory.yaml -i /etc/ansible/inventory/hosts --tags start
```
Variables:

1. Static:
create_directory.yaml
```yaml
---
- name: Create directory on remote hosts
  hosts: all
  become: true      ## Run as sudo/root

  vars:
    dir_path: 

  tasks:
    - name: Ensure directory exists
      file:
        path: "{{ dir_path }}"
        state: directory
        mode: '0755'
```
Run playbook for apply changes:

```
ansible-playbook create_directory.yaml -i /etc/ansible/inventory/hosts
```
2. Parameterized:
Dynamic-value.yaml
```yaml
---
- name: Create directory on remote hosts
  hosts: all
  become: true  

  vars:
    dir_path: /tmp/{{VAR}}

  tasks:
    - name: Ensure directory exists
      file:
        path: "{{ dir_path }}"
        state: directory
        mode: '0755'
```
Run playbook
```
ansible-playbook create_directory.yaml -i /etc/ansible/inventory/hosts --extra-vars "VAR=hello"
```

