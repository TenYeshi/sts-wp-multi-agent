# Development TODO

- [ ] Define the first feature for `plugins/sts-school-manager-3.5.1/`.
- [ ] Define the first feature for `themes/sts-kollegal/`.
- [ ] Before merging PHP changes, run the PHP syntax check using
  `C:\xampp\php\php.exe -l` on the changed files.
- [ ] For review, audit security, context-appropriate escaping, and separation
  of concerns; lint each modified PHP file.

## STS School Manager open roadmap

Synced from
[`plugins/sts-school-manager-3.5.1/Todo.md`](./plugins/sts-school-manager-3.5.1/Todo.md)
(`v3.6.0`); completed/released checklist items are intentionally omitted.

- [ ] **WhatsApp and SMS result dispatching**
  - [ ] Integrate Twilio or Meta WhatsApp Cloud API for alerts to
    `parent_name` / `whatsapp_no`.
  - [ ] Use pre-approved templates for academic-term results.
- [ ] **Bulk student photo ZIP uploader**
  - [ ] Accept a ZIP of `{roll_no}.jpg` photos and attach them to student records.
- [ ] **Bilingual report cards (Tibetan and English)**
  - [ ] Embed licensed Qomolangma/Monlam Tibetan fonts in Dompdf.
  - [ ] Add an English-only versus bilingual layout toggle.
- [ ] **CBSE term-weightage customizer**
  - [ ] Configure component weightages and apply up to 5 grace marks per
    subject for borderline passes.
- [ ] **Database health and backup utility**
  - [ ] Export STS schema/data as SQL or JSON.
  - [ ] Schedule weekly cleanup of unlinked or draft records.
- [ ] **Automated test suite**
  - [ ] Add PHPUnit coverage for CBSE grades A1 through E.
  - [ ] Add integration tests for teacher status transitions and permissions.
