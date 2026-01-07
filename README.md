# dodo-bedrock-kb

Dodo-only knowledge base pack for AWS Bedrock Knowledge Bases.

## Key folders
- kb/        : content intended for Bedrock ingestion (sync this to S3)
- intake/    : raw inputs (NOT committed by default)
- tools/     : local scripts to generate/sanitise kb/ content
- templates/ : templates for consistent authoring
- eval/      : test prompts + expected characteristics
- docs/      : design notes + conventions

## Safety
No PII should be committed into this repo or uploaded to the KB.
Use placeholders in examples (e.g., <FIRSTNAME>, <EMAIL>, <MOBILE>, <ACCOUNT_ID>, <ADDRESS>).
