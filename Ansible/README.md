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

Run Task with playbook:

Task 1: Create directory

create_directory.yaml
```yaml
---
- name: Create directory on remote hosts
  hosts: all
  become: true  

  vars:
    dir_path: /tmp/myfolder

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
It failed!!! Due to connection with the host.
10.10.20.104               : ok=0    changed=0    unreachable=1    failed=0    skipped=0    rescued=0    ignored=0


Pass dynamic values to playbook ?
---------------------------------
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

