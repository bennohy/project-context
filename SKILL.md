---
name: project-context
description: Create and maintain repository-root PROJECT_CONTEXT.md for durable AI-facing project knowledge. Use when asked to map or understand a repository and preserve context, create or update project context, assess whether completed development materially changed it, or verify and repair possibly stale context. Do not start CREATE or REFRESH for ordinary coding, debugging, explanation, or small refactors merely because a repository is being edited.
---

# Project Context

Maintain a concise project mental model without replacing live repository inspection. This Skill owns four operations: `CREATE`, `ASSESS`, `UPDATE`, and `REFRESH`.

## Authority and Boundaries

- Establish the active repository root before reading or writing `PROJECT_CONTEXT.md`. Prefer a reliably resolved Git top-level; otherwise use an explicit, unambiguous workspace or user-confirmed root. Never transfer context between repositories.
- Current source, tests, manifests, and repository evidence take precedence over repository-derived claims in `PROJECT_CONTEXT.md`. Verify every task-relevant claim before relying on it.
- Treat human-provided knowledge as a distinct provenance class. Missing repository evidence is not proof that it is false.
- Use `PROJECT_CONTEXT.md` for durable knowledge that is difficult or costly to rediscover, not for an inventory, complete call graph, dependency database, route list, or source index.
- Normal development may read relevant existing context while still inspecting current source. Reading context alone does not activate `CREATE`, `UPDATE`, or `REFRESH`.
- This Skill describes intended workflows; its text does not by itself establish that a runtime operation succeeded.

## Select the Operation

Treat a valid explicit request for one of these operations as decisive: explicit `CREATE` selects `CREATE`, explicit `ASSESS` selects `ASSESS`, explicit `UPDATE` selects `UPDATE`, and explicit `REFRESH` selects `REFRESH`. Repository evidence may change the findings, affected scope, or proposed content, but must not silently replace the explicitly requested operation. If the requested operation cannot validly apply, explain the conflict and ask rather than substituting another operation.

When no valid explicit operation is requested, infer one only when the available context is unambiguous:

- `CREATE`: The user asks to create persistent project context, or to understand or map a repository and preserve the resulting AI-facing knowledge. Absence of `PROJECT_CONTEXT.md` by itself does not authorize a write.
- `ASSESS`: Completed development work needs a scoped decision about whether durable project knowledge was materially affected.
- `UPDATE`: The user identifies a known or proposed material context change and wants the affected persistent knowledge changed.
- `REFRESH`: The user wants existing context verified for freshness or trustworthiness before deciding what repair, if any, is needed; or, without an explicit operation, current evidence suggests possible staleness.

An `UPDATE` may verify the specific affected claims before proposing an edit. That verification does not turn `UPDATE` into `REFRESH`.

Ordinary coding, debugging, explanation, and small local refactors are not implicit `CREATE` or `REFRESH` triggers. If the requested operation or repository boundary would materially change the work and cannot be established safely, ask before proceeding.

## Load References Progressively

Load only the references required by the selected operation:

- `CREATE`: read [safety-and-exclusions.md](references/safety-and-exclusions.md), [orientation-report.md](references/orientation-report.md), [knowledge-filter.md](references/knowledge-filter.md), and [context-schema.md](references/context-schema.md). Use [PROJECT_CONTEXT.template.md](assets/PROJECT_CONTEXT.template.md) only after approval to prepare the file.
- `ASSESS`: read [materiality-rubric.md](references/materiality-rubric.md). Read a safety section only when additional repository inspection is needed.
- `UPDATE`: read [context-schema.md](references/context-schema.md) and the repair and diff rules in [freshness-and-repair.md](references/freshness-and-repair.md). Read [materiality-rubric.md](references/materiality-rubric.md) if materiality remains uncertain.
- `REFRESH`: read [freshness-and-repair.md](references/freshness-and-repair.md), [context-schema.md](references/context-schema.md), and [safety-and-exclusions.md](references/safety-and-exclusions.md). Load the orientation and Knowledge Filter references only after separately approved full re-orientation.

## Hard Invariants

- Orientation and freshness inspection are read-only. Do not build, test, lint, format, restore, install, clean, package, sign, launch, migrate, seed, deploy, mutate Git, start background services, or download dependencies unless the user separately authorizes the state-changing action.
- Prune generated and restored output before recursive inspection. Never open or expose secrets, credentials, signing material, private data, production data, or sensitive telemetry. Follow [safety-and-exclusions.md](references/safety-and-exclusions.md).
- New context defaults to English. `UPDATE` and repair during `REFRESH` preserve the existing document language. Translate only with explicit authorization.
- Preserve unrelated sections, wording, evidence anchors, formatting, encoding, and line endings during targeted maintenance. Never regenerate the whole document for a localized change.
- Never delete or rewrite human-provided knowledge merely because the repository cannot verify it.
- Full re-orientation may be recommended but must never begin automatically.

## Approval Rules

`CREATE` always stops after read-only orientation, the human-facing report, and the filtered knowledge proposal. The initial request to create context is not approval to write. Obtain explicit post-orientation approval before creating `PROJECT_CONTEXT.md`.

`UPDATE` and any `REFRESH` repair require a concrete proposal and approval unless prior approval is valid. Prior approval is valid only when the current task or conversation retains explicit authorization for the specific context edit or a clearly defined class of context edits that unambiguously includes it. Never infer approval from unrelated or historical tasks, generic source-edit permission, permission to assess, the existence of the context file, or an ambiguous acknowledgment. If authorization or its scope is unclear after resume or compaction, ask again.

Approval applies only to the proposal and scope it answers. It does not carry forward to later or unrelated changes. Do not create an approval store.

## CREATE

Entry: an explicit request to create persistent context or to preserve an orientation as project context.

1. Establish the repository boundary and apply the safety exclusions.
2. Perform bounded, read-only orientation and produce the human-facing report.
3. Apply the Knowledge Filter and incorporate clearly labeled user corrections or business knowledge.
4. Present the proposed persistent knowledge, including limitations and provenance.
5. Stop and request explicit approval.
6. Only after approval, create repository-root `PROJECT_CONTEXT.md` using the schema and template. Verify the final diff, encoding, line endings, and final newline.

Stop without writing when approval is absent, refused, ambiguous, or narrower than the proposal.

## ASSESS

Entry: development work has completed and its project-context impact must be classified.

Inspect only the completed change, its affected behavior and boundaries, and task-relevant evidence. Do not start a full repository scan. Apply the materiality rubric and return exactly one outcome:

- `No context action needed`
- `Create recommended`
- `Update recommended`
- `Updated with prior approval`

If `PROJECT_CONTEXT.md` is absent, return `Create recommended`; do not automatically launch `CREATE`. Use `Update recommended` when existing context is materially affected but no valid write approval exists. Use `Updated with prior approval` only after a targeted edit was actually completed under explicit, current, scoped prior approval and its diff was reviewed. `ASSESS` permission alone never authorizes an edit.

## UPDATE

Entry: a known material change affects identifiable existing knowledge.

1. Identify the smallest affected context area and verify it against current evidence.
2. Present a concrete proposal that names the affected section and intended correction.
3. Stop for approval unless conservative prior-approval requirements are fully satisfied.
4. Make a targeted edit in the existing language. Preserve human-provided and unrelated content.
5. Inspect the before/after diff for substantive scope and incidental churn; verify text format.

Stop rather than broadening the edit when additional affected knowledge is uncertain or outside the approved scope.

## REFRESH

Entry: freshness verification is requested or evidence gives a reason to question existing context.

1. Compare relevant existing claims with current available evidence and classify them as `Verified`, `Possibly stale`, `Stale`, or `Unknown`.
2. Report the evidence, revision limitations, and affected areas. Time alone is never a stale verdict.
3. If no repair is needed, stop after reporting the result.
4. If repair is needed, present a localized update or targeted-refresh proposal and apply the approval rules before writing.
5. Recommend full re-orientation only when the foundational mental model is unreliable; never start it automatically.
6. After an approved repair, inspect the diff and update metadata only for the scope actually verified.

## Architecture Escalation

Do not independently change the Hybrid Project Intelligence model, four-operation model, approval model, safety or read-only boundaries, authority and evidence model, content contract, Knowledge Filter, human-knowledge protection, `AGENTS.md`/Skill responsibility split, or targeted-maintenance principle.

If an actual Codex capability conflicts with one of those decisions, stop the affected implementation, identify the decision and conflict, provide technically feasible alternatives, and wait for an architecture decision. Do not silently substitute another architecture.
