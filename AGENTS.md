# WordPress Development Guidance

This workspace is `C:\xampp\htdocs\school\wp-content`, for the local site at
`http://localhost/school`. Use `C:\xampp\php\php.exe` for PHP commands.

## Managed code boundaries

- The plugin agent works only in `plugins/sts-school-manager-3.5.1/`.
- The theme agent works only in `themes/sts-kollegal/`.
- The reviewer checks changes in those two paths and lints modified PHP files.
- Keep plugin and theme changes and Git operations within their respective
  directories. Do not stage their files in the orchestrator repository.
- Other installed plugins, themes, `uploads/`, and generated/local WordPress
  files are intentionally ignored by the orchestrator Git repository. Never
  add them to its tracking without explicit direction.

## Required project documentation

Before proposing or editing code, read `REFERENCE.md` and the documentation for
the project in scope:

- **Plugin work:** read
  `plugins/sts-school-manager-3.5.1/README.md`,
  `plugins/sts-school-manager-3.5.1/Todo.md`, and all project documentation in
  its `docs/` and `sql/` directories.
- **Theme work:** read `themes/sts-kollegal/README.md`,
  `themes/sts-kollegal/STS-Kollegal-Standalone-Theme-Agent-Brief.md`,
  `themes/sts-kollegal/style.css`, and `themes/sts-kollegal/theme.json`.
- **Cross-project review:** read both projects' documentation listed above,
  plus `REFERENCE.md`, before proposing findings.

Follow the standalone-theme brief's production approval, backup, preservation,
and evidence-labeling rules for any theme-related work.

## Coordinated agent workflow

Use the `orchestrator` agent to plan cross-project work. It delegates plugin
implementation to `plugin-engineer` and theme implementation to
`theme-engineer`; require `wp-reviewer` to complete the security review and PHP
lint checks before declaring implementation tasks complete.

## PHP and WordPress standards

- Guard directly accessible PHP files against direct access with an
  `ABSPATH` check and `exit`.
- Escape output for its context. Use `esc_html()` for HTML text and
  `esc_url()` for URLs; use the corresponding WordPress escaping function for
  other contexts.
- Sanitize and validate input, verify capabilities and nonces for privileged
  actions, and use WordPress APIs and prepared database queries.
- Keep PHP modular, with focused files and functions. Do not include a
  trailing `?>` closing tag in PHP-only files.
- Preserve existing behavior and follow the conventions in the managed code
  area. Keep changes minimal and report validation performed.

See `README.md`, `Todo.md`, and `REFERENCE.md` for workspace details and
project documentation links.
