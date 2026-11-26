# WordPress Development Guidance

This workspace is `C:\xampp\htdocs\school\wp-content`, for the local site at
`http://localhost/school`. Use `C:\xampp\php\php.exe` for PHP commands.

## Managed code boundaries

- The custom plugin agent owns only `plugins/sts-custom-plugin/`.
- The custom theme agent owns only `themes/sts-custom-theme/`.
- Do not modify the existing `plugins/sts-school-manager-3.5.1/` plugin or
  `themes/sts-kollegal/` theme unless explicitly asked.
- Other installed plugins, themes, `uploads/`, and generated/local WordPress
  files are intentionally ignored by Git. Never add them to tracking without
  explicit direction.

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

See `README.md`, `Todo.md`, and `REFERENCE.md` for workspace details.
