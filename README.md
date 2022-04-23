# Automated ArchLinux configuration
This is my personal ansible playbook to install and configure my workstation


# Encryting ssh file
1. Run `ansbile-vault encrypt --vault-password-file [path_to_key_file] id_rsa`
2. To decrypt run `ansbile-vault decrypt --vault-password-file [path_to_key_file] id_rsa`

# How to run it
1. Edit the variables in `group-vars/all.yml`
2. Push the changes to the remote repository
3. Install ansible on the machine you want to configure use `sudo pacman -Syy ansible`
4. Run the following code:
```
ansible-pull --vault-password-file [key file location] -o -U https://github.com/andre-gonzalez/ansible.git
```
5. Sit back and relax
