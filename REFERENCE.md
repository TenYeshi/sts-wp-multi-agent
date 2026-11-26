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

## STS School Manager plugin

### Source documentation

- [Plugin README](./plugins/sts-school-manager-3.5.1/README.md)
- [Plugin task tracker](./plugins/sts-school-manager-3.5.1/Todo.md)
- [Developer guide](./plugins/sts-school-manager-3.5.1/docs/DEVELOPER-GUIDE.md)
- [User guide](./plugins/sts-school-manager-3.5.1/docs/USER-GUIDE.md)
- [Live-site audit report](./plugins/sts-school-manager-3.5.1/docs/LIVE_SITE_AUDIT_REPORT.md)
- [v3.1 database migration](./plugins/sts-school-manager-3.5.1/sql/db-migration-v3.1.sql)
- [Production database indexes](./plugins/sts-school-manager-3.5.1/sql/db-indexes-production.sql)
- [Composer manifest](./plugins/sts-school-manager-3.5.1/composer.json)
- [npm scripts](./plugins/sts-school-manager-3.5.1/package.json)

### Architecture and interfaces

The plugin is a modular WordPress application for enrollment, staff/class/
subject assignments, exams and CBSE grading, marks entry, result publishing,
report cards, and seating allocation. `sts-school-manager.php` loads shared
helpers and database setup first, followed by models, notifications, PDF and
exam-seating modules, then public result and teacher-portal modules. Admin
menus and views provide CRUD, CSV, exam, marks, results, and report-card
workflows. Teacher access is capability-checked and varies by class-teacher
versus subject-teacher assignments.

The documented bootstrap sequence is `functions-table-fix.php` →
`database.php` → dashboard-stat and CSV handlers → core functions and models
→ integrity helpers → notifications, PDF generator, v3.1 fixes, and exam
seating → public result shortcode and teacher-portal compatibility/redirect
modules. Admin modules register menus and dashboard, student, teacher, class,
exam, marks, results, report-card, and shortcode-manager views.

The developer guide documents these five shortcodes:

| Shortcode | Purpose |
| --- | --- |
| `[sts_login_gate]` | Role-aware staff/student portal and teacher registration |
| `[sts_login_form]` | Staff login form |
| `[sts_teacher_portal]` | Teacher dashboard and marks-entry portal |
| `[sts_display_results]` | Public student results lookup |
| `[sts_shortcuts]` | Teacher navigation shortcuts |

No `register_rest_route()` declarations were found in the plugin PHP files;
the documentation describes WordPress `admin-post.php` and AJAX action
handlers instead. Documented `admin-post.php` actions are
`sts_export_students_csv`, `sts_download_demo_student_csv`,
`sts_download_demo_teacher_csv`, `sts_download_single_pdf`,
`sts_download_class_pdf`, and `sts_clean_orphans`. Documented AJAX actions are
`sts_teacher_marks_entry`, `sts_teacher_roster`, `sts_teacher_exam_mgmt`,
`sts_teacher_exam_schemes`, `sts_teacher_profile`, `sts_export_settings`,
`sts_manual_send_notifications`, and `sts_toggle_result_publication`.

Build entry points are `./build.sh`, `./build.sh --versioned`, `npm run build`,
`npm run build:versioned`, `npm run build:zip`, and `npm run clean`. The
Composer manifest requires PHP `>=7.4`; the primary build uses `git archive`
and validates that development-only files are excluded.

### Database tables

The plugin uses the active WordPress table prefix followed by `sts_` (the
documentation uses `wp_` in examples; replace it if the site prefix differs).

| Table suffix | Purpose |
| --- | --- |
| `sts_classes` | Classes and class-teacher assignment |
| `sts_subjects` | Subjects associated with classes |
| `sts_students` | Student roster, academic year, contact and photo details |
| `sts_teachers` | Teacher-to-WordPress-user mapping and approval status |
| `sts_teacher_assignments` | Teacher/class/subject/year assignments |
| `sts_class_subject_exams` | Exam components, marks limits, weightage, publication |
| `sts_marks` | Student scores by class, subject, exam, and academic year |

The v3.1 migration adds academic-year fields, a student class/roll index, and
teacher approval status. The production index script targets the same seven
tables. Review both SQL files before running them against a database.

### Open plugin tasks

The unchecked v3.6.0 roadmap items are synced to the root [Todo.md](./Todo.md).
Check the plugin's [task tracker](./plugins/sts-school-manager-3.5.1/Todo.md)
for the source of truth and detailed acceptance notes.

## STS Kollegal standalone theme

### Source documentation

- [Theme README](./themes/sts-kollegal/README.md)
- [Standalone theme agent brief](./themes/sts-kollegal/STS-Kollegal-Standalone-Theme-Agent-Brief.md)
- [Theme header and metadata](./themes/sts-kollegal/style.css)
- [Block editor settings and palette](./themes/sts-kollegal/theme.json)

The theme is a standalone institutional presentation layer. Its `functions.php`
loads setup, enqueue, widget, template-function, and customizer modules from
`inc/`. Keep school-management business logic in the plugin.

### Design tokens and template hierarchy

The palette includes maroon `#800000` / deep maroon `#5A0000`, navy `#002B49` /
deep navy `#0E266D`, gold `#D4AF37` / light gold `#FFD84D`, slate `#171A1D`,
soft background `#F8FAFC`, and white `#FFFFFF`. Typography uses system UI,
Manrope headings, Inter/system sans, and Tibetan fallbacks
`'Noto Sans Tibetan', 'Jomolhari', 'Microsoft Himalaya', sans-serif`.
`theme.json` sets a 1200px content width and 1440px wide width. CSS also defines
6/10/16px radius tokens, a pill radius, and small/medium/large shadows.

The current theme root provides `index.php`, `page.php`, `single.php`,
`archive.php`, `search.php`, `404.php`, `header.php`, and `footer.php`, with
`content`, `content-page`, `content-single`, and `content-none` template parts.
It does not currently provide `front-page.php` or `home.php`; rely on the
standard WordPress template hierarchy and preserve Elementor's `the_content()`
rendering. Note: the README's example tree still shows an `sts-kollegal/`
wrapper, while the repository is now flattened with installable theme files
at its root.

### Elementor integration and theme rules

`sts_is_elementor_page( $post_id = null )` uses `get_the_ID()` when no ID is
passed and returns the boolean value of the `_elementor_edit_mode` post meta.
The page template passes the current post ID. Preserve Elementor content and
layouts, and keep the documented `[sts_teacher_portal]` and `[sts_login_gate]`
integrations working.

The standalone-theme brief requires evidence-first, read-only discovery;
local/staging development; explicit user approval before production changes;
verified backup and rollback before any approved production deployment; and
preservation of content, IDs, URLs, media, forms, and existing themes. Do not
delete or regenerate images, move plugin business logic into the theme, or
remove the old parent theme without separate approval. Maintain a change log,
label evidence honestly, and test accessibility, responsive behavior,
Elementor, and plugin integrations.

## Git tracking

`wp-content/.gitignore` is allowlist-based. Only the workspace documentation,
`.github/**`, and `sts-school.code-workspace` are intended for tracking.
`plugins/*`, `themes/*`, uploads, and other generated or local files remain
ignored by the orchestrator repository.
