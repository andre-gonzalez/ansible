# Automated ArchLinux configuration
This is my personal ansible playbook to install and configure my workstation


# How to run it
1. Edit the variables in `group-vars/all.yml`
2. Push the changes to the remote repository
3. Install ansible on the machine you want to configure
4. Run the following code:
```
ansible-pull -o -U https://github.com/andre-gonzalez/ansible.git
```
5. Sit back and relax
