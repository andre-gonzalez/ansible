# Automated ArchLinux configuration
This is my personal ansible playbook to install and configure my workstation


# Encrypting ssh file
1. Run `ansbile-vault encrypt --vault-password-file [path_to_key_file] id_rsa`
2. To decrypt run `ansbile-vault decrypt --vault-password-file [path_to_key_file] id_rsa`

# How to run it
1. Edit the variables in `group-vars/all.yml`
2. Push the changes to the remote repository
3. Install ansible on the machine you want to configure use `sudo pacman -Syy ansible`
4. Run the following code:
```
ansible-pull --vault-password-file [key file location] --ask-become -t "[full-install|light-install],[samsung-expert|netbook]" -U https://github.com/andre-gonzalez/ansible.git
```
5. Sit back and relax

# Tags structure
The logic here is the existence of groups tags, so it become easier to skip tags with --skip-tags flag. That is why the tags are nested. The structure is shown below
- full-install
  - docker
  - libvirt
  - light-install
    - ansible
    - audio
    - aur
    - aur
    - authy
    - bluetooth
    - brave
    - cron
    - dmenu
    - dwm
    - dwmblocks
    - eureciclo
    - graphic-card
    - keyboard
    - lf
    - locale
    - neovim
    - network
    - nvidia
    - packages
    - preload
    - processor
    - scripts
    - slock
    - ssh
    - st
    - timeshift
    - timezone
    - users
    - xorg
- samsung-expert*
- netbook*

*These tags should always be specified manually because they are specific drivers for specific machines
