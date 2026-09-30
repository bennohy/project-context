# PROJECT_CONTEXT.md Schema

Use this schema for `CREATE` and for schema-sensitive `UPDATE` or `REFRESH` work. The artifact is concise AI-facing project knowledge, not an authoritative instruction file or repository index.

## Stable Core

Every new document contains these sections:

```markdown
# Project Context

## Context Metadata
## Project Purpose
## System Boundaries
## Architecture
## Agent Guidance
## Unknowns
```

Required sections must contain useful, repository-specific content. Do not leave fabricated facts or generic filler. `Unknowns` may state `None identified within the verification scope` when that conclusion is supported.

## Conditional Sections

Add a conditional section only when supported content passes the Knowledge Filter:

- `## Domain Knowledge`
- `## Important Workflows`
- `## Project Conventions`
- `## Constraints & Invariants`
- `## Decisions & Rationale`
- `## Gotchas & Known Risks`

Omit empty sections. Do not materialize a complete optional-section skeleton for future use. Additional headings may be used when they express valuable project-specific knowledge without turning the document into an inventory.

## Context Metadata

Keep metadata coarse and useful:

- `Last verified`: the date or timestamp of the verification actually performed.
- `Repository revision`: a reliably resolved revision when available.
- `Verification scope`: the repository areas, claims, or operation covered.
- `Known limitations`: missing history, unavailable evidence, excluded areas, or other limits.

When Git is unavailable, the branch is unborn, history cannot be read reliably, or another limitation prevents a trustworthy revision, record the revision as unavailable and explain the limitation. Never guess, synthesize, shorten ambiguously, or copy an unrelated revision. A dirty tree is a limitation or relevance signal, not itself a revision.

Do not add a version matrix, dependency inventory, full technology inventory, per-section commit hashes, or provenance database to metadata.

## Mental Model, Not Inventory

Describe responsibilities, boundaries, relationships, rationale, and representative flows. Prefer a compact model such as:

```text
Presentation -> Application -> Domain -> Infrastructure
```

Representative paths, symbols, or configuration keys may serve as evidence anchors, but avoid full directory trees, exhaustive entry-point lists, complete call graphs, route catalogs, function signatures, or current package-version tables.

An important workflow is normally eligible when it crosses a subsystem, process, network, persistence, trust/security, asynchronous execution, or external-integration boundary. Exclude ordinary local call chains unless they carry a non-obvious constraint.

## Evidence and Claim Labels

Confirmed knowledge does not need a label on every sentence. Add a concise evidence anchor when it materially reduces later verification cost:

```text
Evidence: path/to/file — SymbolName or configuration key
```

Explicitly label:

- `Inferred`: supported reasoning that is not directly established.
- `Unknown`: insufficient evidence; do not present it as stale or false.
- `Human-provided`: knowledge supplied by a person rather than derived from the repository.
- verification limitations that affect trust or coverage.

For human-provided knowledge that the repository cannot establish, preserve semantics equivalent to:

```text
Provenance: Human-provided
Verification: Not derivable from repository
```

Do not delete, weaken, or silently rewrite that knowledge because repository evidence is absent. It may be superseded only by user correction, explicit superseding information, or sufficiently authoritative external evidence supplied or approved by the user.

## Language and Maintenance

- `CREATE`: write new documents in English by default.
- `UPDATE` and `REFRESH`: preserve the existing document language.
- Translation: require explicit authorization.

During targeted maintenance, preserve unrelated sections, order, wording, labels, evidence anchors, encoding, and line endings. Do not reapply the template or normalize prose across the document.
