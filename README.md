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

# Tags structure
The logic here is to work well with tags inheritance, so it become easier to run a whole script using less tags. That is why the tags are nested. The structure is shown below:
- full-install
  - docker
  - libvirt
  - light-install
    - ansible
    - apparmor
    - audio
    - auto-adjust-brightness
    - aur
    - authy
    - aws
    - bluetooth
    - brave
    - cron
    - databricks
    - dbeaver
    - dmenu
    - dotfiles
    - drives
    - dwm
    - dwmblocks
    - eureciclo
    - fail2ban
    - gcloud
    - grub
    - keyboard
    - lf
    - locale
    - neovim
    - network
    - packages
    - pipewire
    - powertop
    - preload
    - pulseaudio
    - python
    - rsync
    - samba
    - save-battery
    - security
    - scripts
    - slock
    - ssh
    - st
    - systemd
    - terraform
    - timeshift
    - timezone
    - tlp
    - ufw
    - users
- samsung-expert*
- netbook*
- nvidia*
- opensmtpd*
- windows-vm

*These tags should always be specified manually because they are specific drivers for specific machines
