# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## `[Unreleased]`

### Added
- **`reference-mapping.schema.json`** — new schema for validating reference mapping entries that track old-to-new value migrations across documentation scopes, with support for exact, regex, and contextual match modes.
- **`shruggie-indexer-v4.schema.json`** — new current schema for shruggie-indexer and metadexer outputs, replacing v3.
- **`shruggie-indexer-v3.schema.json`** — intermediate schema version for shruggie-indexer (now deprecated by v4).
- **`shruggie-fetcher.schema.json`** — new schema for validating shruggie-fetcher target definitions and runtime request conditions.
- Schema catalog entries in `schemas.json` for reference-mapping, shruggie-fetcher, shruggie-indexer v3, and shruggie-indexer v4.
- **"How It Works" section** in README explaining the GitHub Pages architecture, data-driven landing page, and schema addition workflow.
- **"Schema Catalog" section** in README replacing per-schema listings with a pointer to the live catalog and machine-readable endpoint.
- `assets/` directory entry in README repository structure tree.
- Established definition reuse guidance (`HashSet`, `NameObject`) and explicit `$schema` URI in README Schema Design Guidelines.

### Changed
- **shruggie-indexer v3 deprecated** in schema catalog in favor of v4.
- **shruggie-indexer v2 deprecated** in schema catalog in favor of v4.
- Updated workspace configuration for shruggie-indexer v3 and v4 schema references.
- **README overhauled** to remove all hard-coded schema descriptions, URLs, use-cases, and inline validation examples. The live catalog at `schemas.shruggie.tech` is now the single source of truth for schema details.
- **README "Schema Catalog Index" section** slimmed down from a full field-by-field reference table to a concise catalog pointer with programmatic usage example.
- **README "Adding a New Schema" and "Contributing" sections** merged into a single "Contributing" section with "Adding a New Schema" and "Schema Design Guidelines" as subsections.
- **README "Repository Structure" tree** genericized — specific schema filenames replaced with `*.schema.json` wildcard pattern.
- **Corporate name corrected** from "ShruggieTech LLC" to "Shruggie LLC" across README, `docs/index.html`, and `.github/copilot-instructions.md`.

### Fixed
- Corrected example User-Agent string in `shruggie-fetcher.schema.json`.

### Removed
- Hard-coded "Available Schemas" section from README (4 schema entries with descriptions, URLs, feature lists, use-cases, and validation examples).
- Full `schemas.json` field reference table and example JSON entry from README "Schema Catalog Index" section.
- Individual schema filenames from README repository structure tree.
