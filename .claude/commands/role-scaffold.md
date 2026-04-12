Scaffold a new Ansible role under `roles/` following project conventions.

The user must provide the role name as an argument, e.g. `/role-scaffold my-role`.

Create the following files:

**`roles/<name>/tasks/main.yml`**
```yaml
---
# Role: <name>
# Description: <ask the user for a one-line description if not provided>
```

**`roles/<name>/tasks/<name>.yml`** (main task file, stem matches directory name)
```yaml
---
- name: <Name> | Install packages
  # Example task — replace with actual content
  ansible.builtin.package:
    name: []
    state: present
  tags:
    - packages

# Add distro-specific stubs if the role needs multi-distro support:
# when: ansible_os_family == "Archlinux"
# when: ansible_distribution in ["Debian", "Ubuntu"]
```

**`roles/<name>/handlers/main.yml`**
```yaml
---
# Handlers for <name> role
```

**`roles/<name>/vars/main.yml`**
```yaml
---
# Variables for <name> role
# IMPORTANT: encrypt this file with ansible-vault if it contains secrets:
#   ansible-vault encrypt roles/<name>/vars/main.yml
```

After creating the files:
1. Show the user a tree of what was created.
2. Remind them to add the role to `local.yml` under the appropriate host group.
3. If the role needs vault-encrypted vars, remind them to run `ansible-vault encrypt roles/<name>/vars/main.yml`.
4. Remind them of the task naming convention: `{stem} | <description>` (stem = task filename without `.yml`).
