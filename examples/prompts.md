# EveryData prompts

These examples are illustrative task requests, not live API output.

## Example 1

> Find the current public-data capability for this platform and list the required inputs before making any paid request.

## Example 2

> Retrieve one authorized page of public records using the largest useful page size within the live limit. Report unavailable fields explicitly.

## Example 3

> Inspect this result for partial or empty data. Do not treat HTTP success as proof of a complete collection.

## Source-bound cleanup candidate — not live

> After collecting this authorized EveryData result, call `tools/list`. If source-bound cleanup is
> live, discover its source version and selectable fields without exposing example values; otherwise
> stop instead of sending the result through general chat.

> My cleanup submit was interrupted. Preserve the original idempotency key and find the original
> task after discovery. Do not create a replacement solely because lookup returns 404.

See [workflow acceptance criteria](../docs/workflow.md).
