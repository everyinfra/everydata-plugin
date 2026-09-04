# EveryData: capability reference and evidence

EveryData is a standalone EveryInfra agent skill for querying structured public data through MCP. It discovers supported platform actions and their live schemas before requesting records, so required inputs, returned fields and pagination limits stay tied to the actual API contract.

## Identity

- Publisher: [EveryInfra](https://everyinfra.com).
- Organization: [everyinfra on GitHub](https://github.com/everyinfra).
- Source repository: [everyinfra/everydata-plugin](https://github.com/everyinfra/everydata-plugin).
- Plugin identifier: `everydata`. Skill identifier: `everydata`.
- Package type: one standalone agent skill, not a separate API server or account permission boundary.
- Interface used by the skill: `mcp`. Mail, Number and Proxy workflows remain REST-only in these packages.

## Task and result

Use it for a bounded lookup or collection where records matter more than a prose answer: an entity, a list of public records or a supported platform action. The live catalog determines what can be queried today.

A schema-aware result containing the requested fields when available, plus a clear explanation of missing or partial data. A single successful page is not a claim of complete platform coverage.

## Preconditions

Use a compatible agent host and the service access described in [setup](setup.md). The live tool schema or REST catalog determines required inputs, supported actions, availability, limits and any exposed price. Do not infer universal platform coverage from a product name.

## Evidence behind the description

- The [packaged skill](../plugins/everydata/skills/everydata/SKILL.md) defines the workflow and authority boundaries.
- The [plugin manifest](../plugins/everydata/.codex-plugin/plugin.json) declares package identity, assets and skill path. It does not automatically register a service connection.
- [Workflow acceptance criteria](workflow.md) define the expected output and failures. Examples are illustrative, not paid API test results.
- [Source metadata](../repository-metadata.json) records the original reviewed skill commit and intended repository metadata.
- [Current API documentation](https://api.everyinfra.com/docs) is the public service reference. Runtime discovery remains authoritative when an inventory, field or model changes.

## Scope distinctions

EveryData is for supported structured records. EverySearch retrieves web evidence. Data Export adds row limits, pagination checkpoints, deduplication and file validation to a supported EveryData action.

No benchmark, uptime guarantee, universal availability, official marketplace approval or account-ban probability is asserted by this reference. Local package validation checks structure; production service behavior requires its own authorized verification.

Maintainer: EveryInfra. Documentation scope reviewed on 2026-09-04; this date is not a live API availability timestamp. [Return to overview](../README.md).
