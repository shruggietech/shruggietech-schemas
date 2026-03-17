# ShruggieTech Schemas

Official schema storage and validation definitions for Shruggie LLC applications and infrastructure.

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![Website](https://img.shields.io/badge/schemas-schemas.shruggie.tech-green)](https://schemas.shruggie.tech/)

## Overview

This repository hosts JSON Schema definitions used across ShruggieTech projects. All schemas are publicly accessible at `https://schemas.shruggie.tech/` and designed for easy integration into validation pipelines, IDEs, and automated workflows.

## How It Works

The `docs/` directory is the root for [GitHub Pages](https://pages.github.com/), served at **[schemas.shruggie.tech](https://schemas.shruggie.tech/)**. The landing page (`docs/index.html`) is fully data-driven — it dynamically renders the schema catalog by loading `docs/data/schemas.json` at runtime. Schema files live alongside the catalog in `docs/data/`. Adding or updating a schema never requires changes to the HTML.

## Schema Catalog

Browse all available schemas on the live catalog at **[schemas.shruggie.tech](https://schemas.shruggie.tech/)**.

A machine-readable catalog is also available for programmatic discovery:

**URL:** `https://schemas.shruggie.tech/data/schemas.json`

```bash
# List all current schema URLs
curl -s https://schemas.shruggie.tech/data/schemas.json | \
  jq -r '.[] | select(.status == "current") | "https://schemas.shruggie.tech/data/" + .file'
```

## Integration

### VS Code

Add schema associations to your `settings.json` or workspace configuration:

```json
{
  "json.schemas": [
    {
      "fileMatch": ["*_meta2.json", "*_directorymeta2.json"],
      "url": "https://schemas.shruggie.tech/data/shruggie-indexer-v2.schema.json"
    },
    {
      "fileMatch": ["manifest.json", "*.webmanifest"],
      "url": "https://schemas.shruggie.tech/data/web-manifest.schema.json"
    }
  ]
}
```

### JetBrains IDEs

1. Open Settings → Languages & Frameworks → Schemas and DTDs → JSON Schema Mappings
2. Add new mapping with schema URL and file pattern

### Command Line Validation

**Using ajv-cli:**
```bash
npm install -g ajv-cli
ajv validate -s <schema-url> -d <data-file>
```

**Using Python jsonschema:**
```bash
pip install jsonschema requests
python -c "
import json, requests, jsonschema
schema = requests.get('<schema-url>').json()
data = json.load(open('<data-file>'))
jsonschema.validate(data, schema)
"
```

**Using PowerShell:**
```powershell
# Requires Newtonsoft.Json.Schema NuGet package
$schema = Invoke-RestMethod -Uri '<schema-url>'
$data = Get-Content '<data-file>' | ConvertFrom-Json
# Validation logic here
```

## Schema Versioning

Schemas follow semantic versioning principles:
- **Major version changes** (v1 → v2): Breaking changes to structure or required fields
- **Minor additions**: New optional fields or definitions (maintain backward compatibility)
- **Patches**: Documentation updates, constraint clarifications

Deprecated schemas remain available but are marked as such. Update to latest versions when possible.

## Repository Structure

```
shruggietech-schemas/
├── docs/                              # GitHub Pages root (schemas.shruggie.tech)
│   ├── data/                          # Schema definitions & catalog
│   │   ├── schemas.json               # Machine-readable schema catalog index
│   │   └── *.schema.json              # Schema definition files
│   ├── assets/                        # CSS, JS, fonts, brand images
│   └── index.html                     # Public schema catalog (data-driven)
├── .gitignore
├── LICENSE                            # Apache 2.0
├── README.md
└── shruggie-schemas.code-workspace    # VS Code workspace config
```

## Contributing

Contributions are welcome. When proposing new schemas or modifications:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b schema/new-feature`)
3. **Add or edit the schema file** in `docs/data/` and **register it** in `docs/data/schemas.json`
4. **Validate** your schema against JSON Schema Draft 7 specifications
5. **Test** with sample data files
6. **Submit** a pull request with clear description

### Adding a New Schema

Adding a schema is a two-step process:

1. **Place the schema file** in `docs/data/` following the naming convention `shruggie-[product]-v[version].schema.json` (or an appropriate descriptive name for third-party/external schemas).

2. **Append an entry to `docs/data/schemas.json`** with the required catalog keys. The landing page is fully data-driven — no HTML changes are needed.

**Example — adding a hypothetical `shruggie-config-v1` schema:**

```jsonc
// Add this object to the array in docs/data/schemas.json
{
    "id": "shruggie-config-v1",
    "title": "shruggie-config schema",
    "version": "v1",
    "description": "A JSON Schema for validating shruggie application configuration files.",
    "status": "current",
    "file": "shruggie-config-v1.schema.json",
    "notes": [],
    "externalLinks": []
}
```

### Schema Design Guidelines

- Use JSON Schema Draft 7 (`"$schema": "http://json-schema.org/draft-07/schema#"`)
- Include clear `description` values for all properties
- Define `required` fields explicitly
- Provide examples in schema descriptions where helpful
- Set `$id` to the full public URL (e.g. `https://schemas.shruggie.tech/data/<filename>`)
- Add validation patterns for string formats (e.g. hex hashes, ISO timestamps)
- Reuse established definitions (`HashSet`, `NameObject`) when applicable — see existing schemas for patterns
- Consider forward compatibility when adding fields

## License

Licensed under the Apache License, Version 2.0. See [LICENSE](LICENSE) for full text.

## Resources

- **Schema Catalog:** [schemas.shruggie.tech](https://schemas.shruggie.tech/)
- **GitHub Repository:** [github.com/shruggietech/shruggietech-schemas](https://github.com/shruggietech/shruggietech-schemas)
- **JSON Schema Specification:** [json-schema.org](https://json-schema.org/)
- **ShruggieTech:** [shruggie.tech](https://shruggie.tech/)

## Support

For issues, questions, or feature requests, open an issue on GitHub.

---

**© 2025-2026 Shruggie LLC. All rights reserved.**
