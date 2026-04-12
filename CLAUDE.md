# Ansible Project Context

## Purpose
Personal Ansible configuration managing Arch/Debian/Ubuntu workstations and servers for a single user.

## Key Files

| File | Purpose |
|------|---------|
| `local.yml` | **Main playbook** — the only one that runs roles |
| `main.yml` | Handlers only (not an entry point) |
| `hosts.yml` | Inventory — vault-encrypted |
| `ansible.cfg` | Minimal config: vault key file + inventory path |
| `.vault_key` | Vault password file — never print or commit |
| `requirements.yml` | Collections: `community.general`, `community.docker`, `kewlfft.aur` |
| `.config/ansible-lint.yml` | Lint rules (profile: production) |

## Role Execution Order

```
base          → all hosts
light_workstation → light_workstation group
heavy_workstation → heavy_workstation group
work          → work group
samsung_expert → samsung_expert group
nvidia        → nvidia group
server        → server group
```

## Conventions

### Task Naming
All tasks must follow the `{stem} | <description>` pattern (enforced by ansible-lint):
```yaml
- name: Packages | Install base packages
- name: SSH | Configure authorized keys
```
The stem is the task file name without extension (e.g. `Security`, `Packages`, `SSH`).

### Multi-distro Handling
Use `when:` conditions based on `ansible_os_family` or `ansible_distribution`:
```yaml
when: ansible_os_family == "Archlinux"
when: ansible_distribution in ["Debian", "Ubuntu"]
```

### Secrets & Vault
- `hosts.yml` and `roles/*/vars/main.yml` files are vault-encrypted
- Never suggest hardcoding secrets or printing vault key contents
- Decrypt with: `ansible-vault decrypt <file>` (requires `.vault_key` present)

### Tags
Run playbooks with `--tags` for scoped execution. Common tags: `packages`, `ssh`, `security`, `dotfiles`, `cron`.
Check available tags per role before running.

## Linting & CI

- Pre-commit: `ansible-lint` via `.pre-commit-config.yaml`
- CI: `.github/workflows/ansible-lint.yml` — runs on push/PR to main
- CI requires `ANSIBLE_VAULT_PASSWORD` secret in GitHub repository settings

## Roles Overview

| Role | Hosts | Purpose |
|------|-------|---------|
| `base` | all | Core system: packages, users, SSH, security, network, AppArmor, fish, neovim |
| `light_workstation` | light_workstation | DWM desktop, AUR packages, dotfiles, audio, bluetooth, wifi |
| `heavy_workstation` | heavy_workstation | Docker, libvirt, Windows VM, Samba, SMTP |
| `work` | work | AWS, Terraform, Databricks, Slack, neomutt, Cursor |
| `samsung_expert` | samsung_expert | Samsung laptop: drives, Intel graphics, network |
| `nvidia` | nvidia | NVIDIA drivers and utilities |
| `server` | server | SSH hardening, security, process accounting |
| `docker` | (standalone) | Docker installation |
| `pihole` | (standalone) | Pi-hole DNS ad-blocking |
