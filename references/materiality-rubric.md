# Materiality Rubric

Use this reference for `ASSESS` and when an `UPDATE` candidate has uncertain scope.

## Mental-Model Test

Ask:

> Does this completed change materially alter the mental model an AI agent should use when working in this repository?

Assess the completed work only. Inspect its changed behavior, affected boundaries, relevant tests or manifests, and the context sections it could affect. Do not perform a full repository scan merely because development occurred.

## Normally Material

- an architecture boundary changes;
- a major subsystem is added, removed, or assigned a new responsibility;
- an important cross-boundary workflow changes;
- an integration, process, persistence, or trust boundary changes;
- the role of a public contract changes;
- authentication or authorization behavior changes at the model level;
- runtime, deployment, or operational topology changes;
- a project-wide convention or compatibility constraint changes;
- important domain meaning, rationale, invariant, gotcha, or risk changes; or
- human-provided knowledge is explicitly corrected or superseded.

## Normally Non-Material

- a local bug fix that preserves the established mental model;
- a private rename or implementation detail;
- a local refactor with unchanged responsibility boundaries;
- formatting, comments, or prose-only cleanup;
- logging-only changes;
- ordinary tests that do not establish a new project-wide rule;
- a patch dependency update; or
- code relocation without a responsibility or boundary change.

These are defaults, not keyword rules. A small diff can be material when it changes a critical invariant; a large mechanical diff can be non-material.

## Ambiguous Cases

When materiality is uncertain:

1. Identify the candidate context claim or section.
2. Compare pre-change and current behavior using task-relevant source, tests, contracts, or configuration.
3. Determine whether a future agent relying on the old mental model would make a meaningful mistake.
4. Label unresolved evidence as `Unknown`; do not expand into full orientation.
5. Prefer `Update recommended` over an unauthorized edit when the impact is plausible and important.

Examples:

| Change | Evidence question | Likely result |
| --- | --- | --- |
| Handler renamed, same responsibility | Did any boundary or convention change? | Non-material |
| Existing adapter now owns retries globally | Does responsibility or operational behavior change? | Material |
| New tests document an existing invariant | Was the invariant already durable and known? | Case by case |
| Package moved between folders | Did ownership or dependency direction change? | Case by case |
| Major redesign spans several subsystems | Is the foundational model still reliable? | Material; full re-orientation may be recommended, never automatic |

## ASSESS Outcomes

Return exactly one of these strings:

- `No context action needed`: existing context is present and the completed work does not materially affect durable knowledge.
- `Create recommended`: repository-root `PROJECT_CONTEXT.md` is absent after the scoped assessment. Do not automatically start `CREATE`.
- `Update recommended`: existing context is materially affected, but no valid, explicit, current, scoped approval authorizes the proposed edit.
- `Updated with prior approval`: a targeted context edit was actually completed under valid prior approval, and the final diff was inspected.

Permission to perform development or `ASSESS` does not authorize context creation or update. If valid prior approval exists, it must cover the specific change or a clearly defined class that unambiguously includes it. Otherwise recommend and stop.

## Scope and Reporting

Name the affected section or knowledge area, summarize the relevant evidence, and state why the change does or does not alter the mental model. Do not use `ASSESS` to refresh unrelated context, normalize language or formatting, or opportunistically repair other sections.
