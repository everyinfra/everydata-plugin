# Changelog

## 0.3.0 — 2026-10-10

- The data cleanup tools were retired on 2026-10-09. To clean, label or summarize collected records,
  use EveryAI (`everyinfra_chat`), the OpenAI-compatible AI API, free for accounts that have topped up.
- Remove the cleanup handoff guide and cleanup examples; update the skill, README files, manifests
  and repository metadata to match.
- Use neutral wording for request parameters and returned data in the skill.
- Replace the plain-text terminology check in `scripts/validate.py` with a hashed blocklist that also
  covers JSON and YAML files.

## 0.2.0 — 2026-09-06

- Add the cleanup handoff for authorized EveryData results (retired in 0.3.0).
- Document all 15 cleanup operations, entitlement and bounded included-use limits.
- Add inferred field discovery, task listing and original-task recovery by idempotency key.
- Keep collection results bound to server-issued source references and versions.

## 0.1.0 — 2026-09-05

- Standalone packaging for `everydata`.
- Focused English and Chinese README, setup, workflow, examples and repository discovery metadata.
- Imported the reviewed skill and H2 brand assets from the source commit in `repository-metadata.json`.
- Release scope is GitHub source distribution; marketplace approval and live paid-operation tests remain separate.
