# Metadata Sidecar Schema (Bedrock KB)

## Overview
Each KB document may include a sidecar file named `<filename>.metadata.json` stored next to the source file. Sidecars enable filtering and targeted retrieval. Bedrock expects metadata under a top-level `metadataAttributes` object.

- Keep sidecars under 10KB.
- Use lower-case strings for stable filtering.
- Use arrays of lower-case strings when a document legitimately applies to multiple scopes (for example, a shared rule that applies to multiple campaign types).
- Only include fields that apply to the file type.

## Base Schema (Minimal)
```json
{
  "metadataAttributes": {
    "brand": "dodo",
    "channel": "edm",
    "doc_type": "rule",
    "campaign_type": "service_notice",
    "product": "internet",
    "module_type": "cta",
    "format": "markdown"
  }
}
```

## Multi-value fields (when applicable)
If a document is valid for multiple scopes, store an array of lower-case strings instead of a single value.

```json
{
  "metadataAttributes": {
    "brand": "dodo",
    "channel": "edm",
    "doc_type": "rule",
    "campaign_type": ["service_notice", "offer"],
    "product": ["internet", "mobile"],
    "format": "markdown"
  }
}
```

## Field Definitions
- **brand**: Always `dodo`.
- **channel**: Content channel, typically `edm` for email.
- **doc_type**: `rule` | `approved_example` | `module`.
- **campaign_type**: `service_notice` | `offer` | `price_change` | `billing` | `outage` | `winback` | `other`. Use a single string or an array of strings if multiple apply.
- **product**: `internet` | `mobile` | `energy` | `other`. Use a single string or an array of strings if multiple apply.
- **module_type** (modules only): `cta` | `support_block` | `pricing_panel` | `info_block` | `footer` | `legal` | `logo` | `other`.
- **format**: `markdown` | `html_snippet`.

## Examples
### Rule document
```json
{
  "metadataAttributes": {
    "brand": "dodo",
    "channel": "edm",
    "doc_type": "rule",
    "campaign_type": "other",
    "product": "other",
    "format": "markdown"
  }
}
```

### Module snippet
```json
{
  "metadataAttributes": {
    "brand": "dodo",
    "channel": "edm",
    "doc_type": "module",
    "campaign_type": "other",
    "product": "other",
    "module_type": "cta",
    "format": "html_snippet"
  }
}
```

### Approved example
```json
{
  "metadataAttributes": {
    "brand": "dodo",
    "channel": "edm",
    "doc_type": "approved_example",
    "campaign_type": "service_notice",
    "product": "internet",
    "format": "markdown"
  }
}
```
