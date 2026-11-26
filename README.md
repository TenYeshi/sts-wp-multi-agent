# Local WordPress Development

This workspace supports development for **STS Kollegal School**, served at
[`http://localhost/school`](http://localhost/school).

## Local environment

- WordPress folder: `C:\xampp\htdocs\school`
- Content workspace: `C:\xampp\htdocs\school\wp-content`
- PHP CLI: `C:\xampp\php\php.exe`
- Run PHP syntax checks with `C:\xampp\php\php.exe -l <file.php>`.

## Existing installations (inspected before setup)

- Plugin: `plugins/sts-school-manager-3.5.1/` — **STS School Manager**, version
  3.5.1.
- Theme: `themes/sts-kollegal/` — **STS Kollegal**, version 1.0.0.

These are existing installations, not the new custom development targets.
Leave them unchanged unless specifically requested.

## Custom development

- Custom plugin: `plugins/sts-custom-plugin/`
- Custom theme: `themes/sts-custom-theme/`
- Agent instructions: `.github/agents/`

Git ignores all of `wp-content` by default, then allows only the workspace
documents, `.github/**`, and the two custom code paths. Existing third-party
code, uploads, and other local content remain untracked.

Follow `AGENTS.md` for coding rules and `REFERENCE.md` for paths and commands.
