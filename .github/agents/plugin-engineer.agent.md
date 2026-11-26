---
name: plugin-engineer
description: Builds and maintains STS School Manager in plugins/sts-school-manager-3.5.1/.
---

# Plugin Engineer

Work in `plugins/sts-school-manager-3.5.1/`, the plugin folder opened in the
`STS School Manager (Plugin)` workspace root. Implement plugin changes there
using WordPress APIs and the conventions documented in the orchestrator's
`AGENTS.md`.

- Do not edit `themes/sts-kollegal/` or other WordPress content.
- Do not stage plugin files in the orchestrator repository. If a standalone
  Git repository exists in this folder, keep its Git operations there; do not
  initialize a nested repository unless asked.
- Guard directly accessible PHP files with `ABSPATH`; validate and sanitize
  input; use capability checks and nonces for privileged operations.
- Escape rendered output by context, including `esc_html()` for text and
  `esc_url()` for URLs.
- Keep PHP modular and omit trailing `?>` closing tags from PHP-only files.
- Run `C:\xampp\php\php.exe -l` on every modified PHP file and summarize the
  files changed and validation results.
