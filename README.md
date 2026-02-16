# ShruggieTech Schemas

Official schema storage and validation definitions for ShruggieTech LLC applications and infrastructure.

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![Website](https://img.shields.io/badge/schemas-schemas.shruggie.tech-green)](https://schemas.shruggie.tech/)

## Overview

This repository hosts JSON Schema definitions used across ShruggieTech projects. All schemas are publicly accessible at `https://schemas.shruggie.tech/` and designed for easy integration into validation pipelines, IDEs, and automated workflows.

## Available Schemas

### Data Schemas

#### Shruggie Indexer v2 (Current)
**URL:** `https://schemas.shruggie.tech/data/shruggie-indexer-v2.schema.json`

Comprehensive file and directory metadata schema with support for:
- Content-addressable identity using MD5/SHA256/SHA512 hashes
- Hierarchical directory structures with recursive nesting
- Filesystem attributes (timestamps, size, MIME types)
- Metadata entries (generated and sidecar)
- Reversal operations for MetaMergeDelete workflows

**Use cases:**
- File indexing and cataloging systems
- Content-addressable storage implementations
- Metadata aggregation and preservation
- Filesystem analysis and reporting

**Validation example:**
```bash
# Using ajv-cli
ajv validate -s https://schemas.shruggie.tech/data/shruggie-indexer-v2.schema.json -d your-index-file.json

# Using Python jsonschema
python -c "
import json, requests, jsonschema
schema = requests.get('https://schemas.shruggie.tech/data/shruggie-indexer-v2.schema.json').json()
data = json.load(open('your-index-file.json'))
jsonschema.validate(data, schema)
print('Valid')
"
```

#### Shruggie Indexer v1 (Deprecated)
**URL:** `https://schemas.shruggie.tech/data/shruggie-indexer-v1.schema.json`

Legacy schema for shruggie-indexer outputs. Use v2 for new implementations.

#### Web Manifest
**URL:** `https://schemas.shruggie.tech/data/web-manifest.schema.json`

JSON Schema for validating Progressive Web App (PWA) manifest files according to W3C specifications.

**Supported features:**
- Application metadata (name, description, theme colors)
- Icon definitions with purpose and sizes
- Display modes and orientation preferences
- Shortcuts and related applications
- Scope and start URL configuration

**Validation example:**
```bash
ajv validate -s https://schemas.shruggie.tech/data/web-manifest.schema.json -d manifest.json
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

## Repository Structure

```
shruggietech-schemas/
├── docs/
│   ├── data/                          # Schema definitions
│   │   ├── shruggie-indexer-v1.schema.json
│   │   ├── shruggie-indexer-v2.schema.json
│   │   └── web-manifest.schema.json
│   └── index.html                     # Public schema catalog
├── .gitignore
├── LICENSE                            # Apache 2.0
├── README.md
└── shruggie-schemas.code-workspace    # VS Code workspace config
```

## Schema Versioning

Schemas follow semantic versioning principles:
- **Major version changes** (v1 → v2): Breaking changes to structure or required fields
- **Minor additions**: New optional fields or definitions (maintain backward compatibility)
- **Patches**: Documentation updates, constraint clarifications

Deprecated schemas remain available but are marked as such. Update to latest versions when possible.

## Contributing

Contributions are welcome. When proposing new schemas or modifications:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b schema/new-feature`)
3. **Document** the schema purpose and usage in comments
4. **Validate** your schema against JSON Schema Draft 7 specifications
5. **Test** with sample data files
6. **Submit** a pull request with clear description

### Schema Design Guidelines

- Use JSON Schema Draft 7 or later
- Include clear descriptions for all properties
- Define required fields explicitly
- Provide examples in schema descriptions where helpful
- Use `$id` with full schema URL
- Add validation patterns for string formats
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

**© 2025 ShruggieTech LLC. All rights reserved.**
