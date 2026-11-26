# Local Development Reference

## Environment

| Item | Value |
| --- | --- |
| Local site | `http://localhost/school` |
| WordPress root | `C:\xampp\htdocs\school` |
| Workspace | `C:\xampp\htdocs\school\wp-content` |
| PHP executable | `C:\xampp\php\php.exe` |

Run a PHP syntax check:

```powershell
& 'C:\xampp\php\php.exe' -l 'C:\xampp\htdocs\school\wp-content\path\to\file.php'
```

## Existing plugins and themes

| Type | Existing folder | WordPress name | Version |
| --- | --- | --- | --- |
| Plugin | `plugins/sts-school-manager-3.5.1/` | STS School Manager | 3.5.1 |
| Theme | `themes/sts-kollegal/` | STS Kollegal | 1.0.0 |

These are the existing local folders opened by `sts-school.code-workspace`.

## Managed development paths

- Orchestrator: `.` (root folder)
- Plugin: `plugins/sts-school-manager-3.5.1/` (owned by `plugin-engineer`)
- Theme: `themes/sts-kollegal/` (owned by `theme-engineer`)
- Review: `wp-reviewer` audits security, escaping, and separation of concerns
  in the plugin and theme changes, then lints every modified PHP file.

## Coding requirements

- Use `ABSPATH` guards for directly accessible PHP files.
- Escape rendered output, including `esc_html()` for text and `esc_url()` for
  URLs; select the escaping function for the output context.
- Organize PHP into focused modules and omit trailing `?>` closing tags from
  PHP-only files.
- Validate and sanitize input; apply capability and nonce checks to privileged
  operations.

## Git tracking

`wp-content/.gitignore` is allowlist-based. Only the workspace documentation,
`.github/**`, and `sts-school.code-workspace` are intended for tracking.
`plugins/*`, `themes/*`, uploads, and other generated or local files remain
ignored by the orchestrator repository.
