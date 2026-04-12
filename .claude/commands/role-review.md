Review an Ansible role for compliance with project conventions and ansible-lint rules.

The user provides the role name as an argument, e.g. `/role-review base`.

Read all task files under `roles/<name>/tasks/` and check for:

1. **Task naming convention** — every task must follow `{stem} | <description>` where stem is the task filename without `.yml`. Flag any task that doesn't match.

2. **No hardcoded secrets** — look for passwords, tokens, API keys, or private paths hardcoded in task files. Flag any findings. Vars files should be vault-encrypted (they will appear as `$ANSIBLE_VAULT;...` — that's correct and expected).

3. **Multi-distro when-conditions** — if the role targets multiple distros, verify that distro-specific tasks use `when: ansible_os_family` or `when: ansible_distribution`. Flag tasks that might silently run on the wrong distro.

4. **Handler references** — for every `notify:` in task files, verify the referenced handler exists in `roles/<name>/handlers/main.yml`. Flag broken references.

5. **Module FQCN** — tasks should use fully-qualified collection names (e.g. `ansible.builtin.copy`, `community.general.pacman`) rather than short names like `copy` or `pacman`.

6. **Tags** — check that tasks use tags where appropriate (packages, ssh, security, etc.). Flag task files with no tags at all.

After reviewing, produce a summary with:
- A pass/fail status for each check
- Specific file:line references for each issue found
- Suggested fixes for any violations
