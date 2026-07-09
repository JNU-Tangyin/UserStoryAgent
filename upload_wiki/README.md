# Upload Wiki Knowledge Base

This folder contains a public-safe Markdown derivative of the original PDF Wiki knowledge base. It is designed for RAG grounding in the user-story quality-assurance workflow.

## Contents

- `docs/`:Source documents are sanitized based on risk levels using the following two modes:
  * High-risk documents (summary_only_public_context) : Only a public-safe summary and topic outline are retained.
  * Other documents (sanitized_topic_outline): Converted to a public-safe topic outline, preserving the logical framework rather than a full procedural manual.
- `module_overview.md`: module-level index and content summary.
- `glossary.md`: public-safe terminology for MES/user-story interpretation.

## Important Limitations

This folder is not a complete copy of the original Wiki. It intentionally excludes detailed internal technical configuration, credentials, endpoint/network information, account/person details, raw screenshots, field-level setup procedures, and any evaluation labels or gold rewritten answers.
