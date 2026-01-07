# dodo-bedrock-kb

Dodo-only knowledge base pack for AWS Bedrock Knowledge Bases. This repository exists to produce a **PII-safe**, **RAG-optimised** content pack that can be synced to **S3** and ingested by **Bedrock Knowledge Bases**.

## Purpose
- Provide **authoritative Dodo EDM guidance** (voice, formatting, terminology, CTA/support rules).
- Provide **approved, sanitised examples** of Dodo EDM copy for retrieval and generation grounding.
- Provide **reusable HTML module snippets** (buttons, support blocks, pricing panels, info blocks, legal/footer) for reliable assembly.
- Provide **metadata sidecars** that enable Bedrock filtering and high-precision retrieval.
- Provide **local tools** to sanitise inputs and convert raw HTML into copy extracts.

## What gets ingested by Bedrock
Only content under `kb/` is intended for ingestion and should be synced to S3.

- `kb/rules/`: source-of-truth guidance derived from the style guide.
- `kb/examples/copy_extract/`: approved, sanitised EDM copy extracts.
- `kb/modules/html_snippets/`: reusable HTML modules.
- `kb/modules/docs/`: usage guidance for modules.

Everything outside `kb/` is support material and should **not** be ingested.

## Key folders
- `kb/`        : content intended for Bedrock ingestion (sync this to S3)
- `intake/`    : raw inputs (NOT committed by default)
- `tools/`     : local scripts to generate/sanitise kb/ content
- `templates/` : templates for consistent authoring
- `eval/`      : test prompts + expected characteristics
- `docs/`      : design notes + conventions (e.g., metadata schema)

## Metadata sidecars
Each ingestible file can include a sidecar JSON file named `<filename>.metadata.json` placed next to the content file. These sidecars are used for Bedrock filtering (e.g., `doc_type`, `campaign_type`, `product`).

See `docs/metadata_schema.md` for the schema and examples.

## Safety and PII policy (non-negotiable)
- **No PII** is allowed in committed files or in any content synced to S3.
- All examples **must** use placeholders like `<FIRSTNAME>`, `<EMAIL>`, `<MOBILE>`, `<ACCOUNT_ID>`, `<ADDRESS>`, `<PLAN_NAME>`, `<AMOUNT>`, `<DATE>`, `<LINK>`.
- Raw HTML with PII must stay in `intake/` and be sanitised before conversion.

## Typical workflow
1. **Add inputs** to `intake/` (raw HTML or text). Do not commit.
2. **Sanitise** inputs using `tools/sanitize_text.py`.
3. **Convert** HTML to copy extracts using `tools/html_to_copy_extract.py`.
4. **Place results** under `kb/examples/copy_extract/` and add metadata sidecars.
5. **Update rules** under `kb/rules/` when new approved guidance is provided.
6. **Sync `kb/` to S3** and run a Bedrock KB ingestion job.

## Sync to S3 (example)
```bash
aws s3 sync kb/ s3://<your-bucket>/<your-prefix>/kb/
```

## Validation
Use `eval/prompts.md` to test retrieval and generation behaviours after ingestion.

## Ownership constraints
- **Dodo-only** content. No other brands.
- Avoid assumptions about Bedrock console settings; focus on producing clean, structured KB content.
