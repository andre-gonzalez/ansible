# Automated ArchLinux workstation and server configuration
This is my personal ansible playbook to install and configure my workstation and configure my server.


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
ansible-pull --vault-password-file [key file location] --ask-become -t "[full-install|light-install],[samsung-expert|netbook]" --become-method=[doas|sudo] -U https://github.com/andre-gonzalez/ansible.git
```
5. Sit back and relax

### Ansible Playbook

```
ansible-playbook -t [tag1, tag2] --ask-become local.yml
```

# Scripts ready to run
1. Vault password file on $HOME with tags light-install, netbook and processor-intel
```
bash <(curl -L tinyurl.com/ansible-netbook)
```

2. Vault password file on $HOME with tags full-install, samsung-expert, processor-intel and nvidia
```
bash <(curl -L tinyurl.com/ansible-samsung)
```

# Roles structure
- base
    - This role runs on all machines. It set configurations that should be on every system
- light-workstation
    - This role set a light workstation, without applications that has a high resource usage
- heavy-workstation
    - This role set the high resource usage applications
- work
    - This role configure work related stuff
- server
    - This role configure a server
