# Copilot Instructions for shruggietech-schemas

This repository manages standard JSON schemas for ShruggieTech LLC products. It is configured to serve these schemas via GitHub Pages from the `docs/` directory.

## Repository Structure

- **Web Root**: `docs/` is the root for GitHub Pages.
- **Schemas**: stored in `docs/data/`.
- **Assets**: `docs/assets/` contains CSS, JS, Fonts, and Brand images.
- **Landing Page**: `docs/index.html` is the entry point.

## Schema Development Standards

When working with JSON schemas in this repository:

1.  **Schema Version**: Always use JSON Schema Draft 7 (`"http://json-schema.org/draft-07/schema#"`).
2.  **Naming Convention**: Files should be named `shruggie-[product]-v[version].schema.json`.
3.  **Common Definitions**: Reuse existing patterns seen in `shruggie-indexer-v2.schema.json`, specifically:
    - `HashSet`: Object containing `md5` (32 hex), `sha256` (64 hex), and optional `sha512` (128 hex).
    - `NameObject`: Object containing `text` (string/null) and `hashes` (HashSet/null).
4.  **Verification**: Ensure all regex patterns for hashes match the specific hex length requirements.

## Web/Documentation Standards

When modifying the documentation site:

1.  **Framework**: The site uses Bootstrap 5 (loaded via `assets/css/bootstrap.min.css`).
2.  **Typography**: Use "Space Grotesk" font for headers and branding.
3.  **Pathing**: All asset links in `index.html` should be absolute URLs pointing to `https://schemas.shruggie.tech/` or relative paths that resolve correctly on the deployed site.
4.  **Meta Visuals**: Maintain the extensive favicon and apple-touch-icon definitions in the `<head>` for brand consistency.

## Workflow

- **New Schemas**: When adding a new schema, verify it is valid JSON and placed in `docs/data/`.
- **Validation**: Schema changes should be backwards compatible where possible. If breaking changes are needed, increment the version number in the filename.
