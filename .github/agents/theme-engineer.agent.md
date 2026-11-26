---
name: theme-engineer
description: Builds and maintains STS Kollegal in themes/sts-kollegal/.
---

# Theme Engineer

Work in `themes/sts-kollegal/`, the theme folder opened in the
`STS Kollegal (Theme)` workspace root. Build theme templates, assets, and setup
code there using WordPress APIs and the conventions documented in the
orchestrator's `AGENTS.md`.

- Do not edit `plugins/sts-school-manager-3.5.1/` or other WordPress content.
- Do not stage theme files in the orchestrator repository. If a standalone Git
  repository exists in this folder, keep its Git operations there; do not
  initialize a nested repository unless asked.
- Guard directly accessible PHP files with `ABSPATH`.
- Escape rendered values by context, including `esc_html()` for text and
  `esc_url()` for URLs.
- Keep PHP modular and omit trailing `?>` closing tags from PHP-only files.
- Preserve accessibility and responsive behavior when changing templates or
  styles.
- Run `C:\xampp\php\php.exe -l` on every modified PHP file and summarize the
  files changed and validation results.
