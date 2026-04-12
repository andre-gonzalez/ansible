Run a syntax check and optional dry-run against `local.yml`.

The user may optionally pass arguments, for example:
- `/ansible-check` — syntax check only
- `/ansible-check --tags security` — syntax check scoped to a tag
- `/ansible-check --check --tags packages` — dry-run with a tag
- `/ansible-check --limit server` — scoped to a host group

Steps:
1. Verify `.vault_key` exists. If not, tell the user and stop.
2. Always run `ansible-playbook local.yml --syntax-check` first. Report any syntax errors immediately and stop if found.
3. If `--check` was requested, run `ansible-playbook local.yml --check` with any extra args the user provided.
4. Summarize the output — highlight any tasks that would change, any errors, and confirm if the run would succeed.

Never actually apply changes (`--check` is a dry-run; do not run without it unless the user explicitly says to run for real).
