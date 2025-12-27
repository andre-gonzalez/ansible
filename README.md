# Automated ArchLinux workstation and server configuration
This is my personal ansible playbook to install and configure my workstation and configure my server.

# GitHub Actions CI/CD Setup
For the ansible-lint validation pipeline to work in GitHub Actions, you need to configure a repository secret:
1. Go to your GitHub repository Settings → Secrets and variables → Actions
2. Click "New repository secret"
3. Name: `ANSIBLE_VAULT_PASSWORD`
4. Value: Your Ansible vault password
5. Click "Add secret"

The workflow will use this secret to create the `.vault_key` file needed by `ansible.cfg` during CI runs.

# Encrypting ssh file
1. Run `ansible-vault encrypt --vault-password-file [path_to_key_file] id_rsa`
2. To decrypt run `ansible-vault decrypt --vault-password-file [path_to_key_file] id_rsa`

# How to run it
### Ansible pull
1. Edit the variables in `group-vars/all.yml`
2. Push the changes to the remote repository
3. Install ansible on the machine you want to configure use `sudo pacman -Syy ansible`
4. Run the following code:
```
ansible-pull --vault-password-file [key file location] --ask-become -t "[light_workstation|heavy_workstation],[samsung_expert],[nvidia]" -U https://github.com/andre-gonzalez/ansible.git
```
5. Sit back and relax

### Ansible Playbook

```
ansible-playbook -t [tag1, tag2] --ask-become local.yml
```

# Scripts ready to run
1. Light_workstation role install
```
curl -L tinyurl.com/ansible-netbook | bash
```

2. Samsung-workstation role install
```
curl -L tinyurl.com/ansible-samsung | bash
```

# Roles structure
### base
- This role runs on all machines. It set configurations that should be on every system
### light_workstation
- This role set a light workstation, without applications that has a high resource usage
### heavy_workstation
- This role set the high resource usage applications
### work
- This role configure work related stuff
### server
- This role configure a server
