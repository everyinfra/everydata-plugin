# EveryData workflow and acceptance criteria

## Intended outcome

A schema-aware result containing the requested fields when available, plus a clear explanation of missing or partial data. A single successful page is not a claim of complete platform coverage.

## Execution contract

1. Use everyinfra_list_capabilities to identify the applicable platform and action.
2. Read the live action schema and any returned availability, max_limit and price fields.
3. Match the user request to required parameters; ask for genuinely missing inputs instead of inventing them.
4. Use everyinfra_call_api for the authorized query, respecting its current pagination contract.
5. Return the useful structured fields and disclose partial results, omitted fields and observed billing.

## Post-collection cleanup handoff

When the requested outcome continues from collection into model-assisted cleanup, keep the
EveryData result bound to its server-issued source reference. Call MCP `tools/list`; if source-bound
cleanup is absent, report it unavailable and do not fall back to general chat. If it is present,
read the live schemas, inspect entitlement, discover the source version and inferred fields, list
fixed recipes, and preview before any explicit activation or submission.

After a refresh or unknown submit result, preserve the original idempotency key and use the live
task list or original-task lookup. Then inspect task, unit and result state. Do not create a new task
because lookup returns 404, and do not automatically choose partial export, cancellation or result
deletion.

## Failure handling

If discovery or catalog access fails, stop before a paid action. Read required fields from the current schema instead of copying a remembered payload. Report unavailable capabilities and denied account scopes as distinct conditions. Do not broaden keys, repeatedly retry a permanent error or substitute an unrelated mechanism without disclosure.

- No hard-coded platform inventory or promise of fields absent from the live schema.
- No guarantee of historical completeness, private records or unrestricted platform access.
- This product-level skill does not promise a validated CSV artifact; use the export workflow when a file is the deliverable.

## Worked request boundaries

### Scenario 1

> Find the current public-data capability for this platform and list the required inputs before making any paid request.

Accepted behavior: preserve the stated scope; discover the required contract and stop at the explicit no-action boundary. Any broader operation requires new authority.

### Scenario 2

> Retrieve one authorized page of public records using the largest useful page size within the live limit. Report unavailable fields explicitly.

Accepted behavior: preserve the stated scope; discover the required contract and stop at the explicit no-action boundary. Any broader operation requires new authority.

### Scenario 3

> Inspect this result for partial or empty data. Do not treat HTTP success as proof of a complete collection.

Accepted behavior: preserve the stated scope; discover the required contract and stop at the explicit no-action boundary. Any broader operation requires new authority.


These are illustrative prompts, not captured API responses or claims of successful live execution. They deliberately avoid guessed JSON payloads and fabricated prices. See [prompt acceptance fixtures](../examples/acceptance.json) for the offline safety assertions.

## Result review

A schema-aware result containing the requested fields when available, plus a clear explanation of missing or partial data. A single successful page is not a claim of complete platform coverage.

Check original results rather than relying on the agent's summary alone. Preserve response status and evidence only to the extent safe; redact personal or secret fields. If billing is absent from the response, say it is not observable there rather than inferring a charge from HTTP success.

## Related decision

EveryData is for supported structured records. EverySearch retrieves web evidence. Data Export adds row limits, pagination checkpoints, deduplication and file validation to a supported EveryData action.

Return to [README](../README.md) or [setup](setup.md).
