---
tags:
  - technologies
date: 2023-09-1
---
- Push-based config management tool.
- Uses [[SSH]] or [[WinRM (Windows Remote Management)|WinRM]] to manage remote hosts.
- Can automate:
	- system configs (users, files, packages, services).
	- app deployment
	- orchestration across nodes
- Written in Python with YAML-based `playbooks`.
# Key Components

- `Inventory`: file listing hosts Ansible can manage (e.g. `inventory.ini`)
- `Playbook`: YAML file describing tasks to execute on targets.
- `Module`: units of work (e.g. `copy`, `apt`, `user`, `shell`) - ansible ships with hundreds.
- `Role`: structured way to organize related tasks.
- `Idempotency`: tasks won't change the system if it is already in the desired state.
## Inventory

```ini
[web]
10.0.0.10 ansible_user=root

[db]
10.0.0.11 ansible_user=admin
```
## Playbook

```yaml
- name: Setup web servers
  hosts: web
  become: yes
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
```
# Execution Flow

- Typically run `ansible` or `ansible-playbook`
- Ansible reads the inventory and playbooks.
- Connects via SSH or WinRM.
- Executes modules as Python or raw shell commands on targets.
- Collects results, prints output.
#  Security

- SSH key-based access (or WinRM with passwords).
- Optional `become: true` for privilege escalation.
- Sensitive data can be stored in:
	- `group_vars`, `host_vars` or `vaults`.
- Access controlled by:
	- file permissions.
	- tower (for RBAC/audit in enterprise setups)