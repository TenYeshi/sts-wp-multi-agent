# Local WordPress Development

This workspace supports development for **STS Kollegal School**, served at
[`http://localhost/school`](http://localhost/school).

## Local environment

- WordPress folder: `C:\xampp\htdocs\school`
- Content workspace: `C:\xampp\htdocs\school\wp-content`
- PHP CLI: `C:\xampp\php\php.exe`
- Run PHP syntax checks with `C:\xampp\php\php.exe -l <file.php>`.

## Plugin and theme workspace roots

- Plugin: `plugins/sts-school-manager-3.5.1/` — **STS School Manager**, version
  3.5.1.
- Theme: `themes/sts-kollegal/` — **STS Kollegal**, version 1.0.0.

The [sts-school.code-workspace](./sts-school.code-workspace) opens these
alongside the orchestrator root (`.`). The plugin and theme agents work only
in their respective folders. Their files remain ignored by the orchestrator
repository so the plugin and theme can be versioned independently. No nested
`.git` repositories are currently present in those folders.

Agent instructions are in `.github/agents/`. The orchestrator repository
allowlist includes this workspace file, documentation, and `.github/**`;
`plugins/*`, `themes/*`, uploads, and other local content remain ignored.

Follow `AGENTS.md` for coding rules and `REFERENCE.md` for paths and commands.
