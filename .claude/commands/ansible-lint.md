Run `ansible-lint` against the entire project from the repository root.

Steps:
1. Verify `.vault_key` exists at the project root. If it does not, tell the user and stop — ansible-lint will fail without it.
2. Run `ansible-lint` using the Bash tool from the project root directory.
3. Report all errors and warnings grouped by file, including the rule ID and line number so the user can navigate directly to the issue.
4. If there are no issues, confirm the project is lint-clean.

Do not auto-fix anything unless the user explicitly asks. Surface every finding and explain what rule was violated and why.
