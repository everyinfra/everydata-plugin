# EveryData source-bound cleanup handoff

> Production exposes the existing EveryData collection tools and two source-bound cleanup tools.
> Always confirm them through live MCP discovery; tool availability does not prove a particular
> account is eligible, activated or end-to-end tested.

## Correct entry point

Cleanup is for an authorized EveryData result that remains readable on EveryInfra. It is not a free
general Gemini endpoint and does not accept detached arbitrary text, custom prompts, model choice,
tools, external URLs or a customer-defined output schema.

Call MCP `tools/list` first and inspect the cleanup tools' live `inputSchema`. The contract has 15 operations:

- Read: `get_entitlement`, `get_source`, `get_source_fields`, `list_recipes`, `preview`, `list_jobs`,
  `find_job`, `get_job`, `list_units`, `get_result`, `export`.
- Action: `activate`, `submit`, `cancel`, `delete_result`.

The initial included benefit is conditional and bounded: a qualifying direct account with at least
CNY 500 in verified net settled recharge principal may explicitly activate one 30-day period, with
1,000 successful units per UTC day, 30,000 total, 5 execute attempts per minute and 5 concurrent
units. The live entitlement response—not this file—determines eligibility, activation, quota and
whether customer charge is zero.

## Discovery and recovery

1. Inspect entitlement without activating it.
2. Resolve the EveryData `source_ref`, read its server-computed `source_version`, and discover bounded
   field paths/types without example values.
3. Discover fixed recipes and preview the selected fields. Field inference is not execution proof.
4. Activation and submit are separate explicit actions. Persist the submit idempotency key.
5. After refresh or an unknown result, use `list_jobs` or `find_job` with the original key. A 404 is
   not proof that the interrupted submit was never accepted; do not automatically resubmit.
6. Read the original job, units and results before export. Partial export, cancel and deletion remain
   separate choices.

If live discovery does not expose cleanup, return the collected EveryData result normally and state
that source-bound cleanup is unavailable. Do not silently send the result through `everyinfra_chat`.
