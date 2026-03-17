# Changelog

All notable changes to this project will be documented in this file.

## [Unreleased]

### Added
- **Schema catalog index** (`docs/data/schemas.json`): machine-readable JSON catalog listing all available schemas with metadata (id, title, version, description, status, file, notes, externalLinks). Can be fetched programmatically to discover and query available schemas.
- **Interactive schema table** on the landing page: sortable columns (Name, Version, Status), real-time text filter, status badges, and "View Schema" action buttons — all rendered dynamically from `schemas.json`.
- **Machine-readable endpoint notice** on the landing page linking to `schemas.json` for script-friendly consumers.
- **`<noscript>` fallback** directing users without JavaScript to the `schemas.json` catalog.
- **SMS Backup & Restore** schema entry added to the README Available Schemas section.
- **Schema Catalog Index** section in README documenting all `schemas.json` keys with a reference table, example entry, and programmatic usage example.
- **Adding a New Schema** section in README describing the two-step workflow: drop the schema file into `docs/data/` and append an entry to `schemas.json`.
- `CHANGELOG.md` (this file).

### Changed
- **Landing page refactored** from a hardcoded HTML list to a data-driven approach — adding a new schema no longer requires editing `index.html`.
- **README contributing steps** updated to reference the new `schemas.json` registration workflow.
- **README repository structure** updated to include `schemas.json` and `sms-backup-restore.schema.json`.
- **README copyright year** updated to 2025–2026.

### Removed
- Hardcoded schema `<a>` entries and `<noscript>` item list from `index.html` (replaced by data-driven rendering from `schemas.json`).
