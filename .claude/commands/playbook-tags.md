List all tags used across the project, grouped by role and task file.

Steps:
1. Read `local.yml` to understand which roles are applied to which host groups.
2. For each role in `roles/`, read all files under `roles/<role>/tasks/` and collect every `tags:` entry.
3. Also check `local.yml` itself for any play-level or task-level tags.

Output format — grouped by role:

```
base
  tasks/Packages.yml       → packages
  tasks/SSH.yml            → ssh
  tasks/Security.yml       → security, apparmor
  ...

light_workstation
  tasks/packages.yml       → packages
  tasks/dotfiles.yml       → dotfiles
  ...
```

After the grouped list, print a deduplicated alphabetical list of all unique tags across the entire project.

Finally, give a usage tip:
- Run a single tag:    `ansible-playbook local.yml --tags <tag>`
- Run multiple tags:   `ansible-playbook local.yml --tags "packages,ssh"`
- Skip a tag:          `ansible-playbook local.yml --skip-tags <tag>`
- Limit to host group: `ansible-playbook local.yml --limit server --tags security`
