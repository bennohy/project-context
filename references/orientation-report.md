# Orientation Report

Use this reference during `CREATE`. The report is a human-facing review artifact and evidence input to the Knowledge Filter. It is not copied wholesale into `PROJECT_CONTEXT.md`.

## Bounded Orientation

1. Establish the active repository boundary before interpreting paths.
2. Check applicable project instructions and existing `PROJECT_CONTEXT.md`, if any, without treating stored context as current evidence.
3. Inspect filenames, authored manifests, entry points, representative source, tests, documentation, and non-secret configuration needed to understand the project.
4. Prune generated or restored output before recursion and follow all sensitive-data exclusions.
5. Prefer focused inspection over reading every file. Sample repeated structures and disclose coverage limits.
6. Use read-only Git evidence when available. Do not build, restore, test, install, format, launch, or otherwise mutate the project merely to orient.

If the repository root is ambiguous, an excluded directory may contain authored source, or a state-changing action appears necessary, stop and request direction or authorization.

## Report Shape

Include only supported and useful sections:

- executive summary;
- scope and repository boundary;
- technology inventory;
- repository map;
- entry points;
- architecture;
- major features;
- representative execution and data flows;
- persistence;
- integrations;
- errors and observability;
- build, test, and delivery definitions;
- risks;
- troubleshooting map;
- unknowns; and
- recommended next steps.

The report may be comprehensive, but it must remain bounded by relevance and evidence. A repository map summarizes major authored areas and responsibilities rather than reproducing a full tree.

## Claim Format

For important claims, use:

```text
Status: Confirmed | Inferred | Unknown
Evidence: path — symbol or configuration key
Notes: reasoning, scope, or limitation
```

- `Confirmed`: directly supported by current repository evidence.
- `Inferred`: a reasoned conclusion from evidence; identify the reasoning.
- `Unknown`: evidence is missing, excluded, contradictory, or insufficient. Unknown is not false.

Keep quoted errors, identifiers, symbols, paths, configuration keys, and commands exact. Separate observed evidence from interpretation. Never promote the existing context file or human assertion to repository-confirmed status without verification.

## Representative Flows

Choose flows that explain the project mental model, especially those crossing significant boundaries such as subsystem, process, persistence, network, trust/security, asynchronous execution, or external integration. Show responsibilities and transitions, with a few evidence anchors where useful.

Do not enumerate ordinary local method chains, every route, every screen, or every dependency. Record gaps when a boundary could not be inspected safely.

## From Report to Proposal

After the report:

1. Apply the Knowledge Filter to each candidate fact.
2. Separate repository-derived, inferred, unknown, and human-provided knowledge.
3. Present a concise persistent-knowledge proposal, including conditional sections and limitations.
4. Invite corrections and business knowledge.
5. Stop for explicit post-orientation approval.

Only approved, filtered knowledge may be written to `PROJECT_CONTEXT.md`. The original request to orient or create context is not the post-orientation approval.
