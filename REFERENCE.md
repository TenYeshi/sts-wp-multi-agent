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

The inventory is limited to the `plugins/` and `themes/` directories in this
local `school/wp-content` folder. Do not edit these existing installations
while working on custom code unless asked.

## Managed development paths

- Plugin: `plugins/sts-custom-plugin/` (owned by `plugin-engineer`)
- Theme: `themes/sts-custom-theme/` (owned by `theme-engineer`)
- Review: `wp-reviewer` audits security, escaping, separation of concerns,
  and PHP syntax across the workspace.

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
`.github/**`, `plugins/sts-custom-plugin/**`, and
`themes/sts-custom-theme/**` are intended for tracking. Existing plugin/theme
installations, uploads, and other generated or local files remain ignored.
