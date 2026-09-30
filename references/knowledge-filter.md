# Knowledge Filter

Use this reference after orientation and whenever new knowledge is proposed for persistence.

## Admission Test

For each candidate, ask:

> Can an agent reliably rediscover this from the current repository, and what is the cost of doing so?

| Rediscoverability | Rediscovery cost | Default action |
| --- | ---: | --- |
| Easy | Low | Do not persist |
| Easy | High | Summarize when valuable |
| Difficult | Low | Decide case by case |
| Difficult | High | Persist |

Also require that the candidate improves the mental model, prevents a meaningful mistake, preserves rationale or business meaning, or materially reduces repeated orientation cost. Persistence is not justified merely because a fact is true.

## Normally Persist

- architecture rationale and non-obvious responsibility boundaries;
- domain terminology and business meaning;
- important cross-boundary workflows;
- project-wide conventions and golden implementation guidance;
- compatibility requirements and operational constraints;
- non-obvious invariants, gotchas, risks, dangerous patterns, and obsolete approaches to avoid;
- decisions whose rationale cannot be reconstructed cheaply; and
- useful human-provided business knowledge with explicit provenance.

## Normally Exclude

- exact dependency versions and version matrices;
- complete file lists, directory trees, route lists, endpoint catalogs, or entry-point inventories;
- function signatures and implementation-level call chains;
- current package or build-output inventories;
- simple commands readily available in maintained manifests or documentation;
- local implementation details that source inspection reveals cheaply; and
- transient task state, work logs, or speculative future design.

## Architecture as a Special Case

Individual architecture facts may be easy to find while the combined mental model is expensive and error-prone to reconstruct. Persist the compact relationship between responsibilities, boundaries, and rationale when that synthesis is valuable. Do not persist the underlying exhaustive evidence set.

Representative paths and symbols may anchor later verification, but they are evidence pointers rather than the content's organizing principle.

## Workflows

Prefer workflows that cross a subsystem, process, network, persistence, trust/security, asynchronous, or external-integration boundary. A local `button -> method -> helper` sequence is normally excluded unless it carries a non-obvious invariant or business constraint.

## Human-Provided Knowledge

Human-provided knowledge may be highly valuable precisely because the repository cannot express it. Preserve it with explicit provenance and verification limitations. Do not reclassify it as repository-confirmed, and do not discard it for lack of source evidence.

When a human statement conflicts with current repository evidence, preserve both the provenance and the conflict in the proposal; ask for resolution instead of silently choosing or rewriting.

## Progressive Disclosure

Keep the stable core concise. Add conditional sections only for admitted knowledge. Summarize high-cost evidence rather than copying the orientation report. Prefer links or evidence anchors for details that can remain in current source.

Reject candidates that would make `PROJECT_CONTEXT.md` a second README, source index, dependency report, call graph, or comprehensive architecture dossier. The artifact should make future live inspection faster and safer, not replace it.
