# Freshness and Repair

Use this reference for `REFRESH` and for targeted `UPDATE` mechanics. Freshness is based on current evidence, not document age.

## Freshness States

- `Verified`: relevant knowledge was checked against current available evidence within the stated scope.
- `Possibly stale`: relevant-looking changes exist, but no contradiction has been established.
- `Stale`: current evidence contradicts persisted repository-derived knowledge.
- `Unknown`: available evidence is insufficient to verify the claim. Unknown is not equivalent to stale.

Classify only the claims or scope actually examined. Do not imply whole-document verification from a targeted check.

## Allowed Signals

Use multiple relevant signals when available:

- stored last-verified repository revision;
- current repository revision, resolved reliably;
- relevant changes between stored and current revisions;
- dirty working-tree changes when they touch the claims being checked;
- current task-relevant source, tests, manifests, and configuration;
- existence and content of relevant authored artifacts when Git evidence is unavailable; and
- known exclusions, missing history, unavailable tools, and other verification limitations.

Time may prompt verification, but time alone must never classify content as stale. A changed revision is also not a stale verdict; determine whether relevant areas changed. A dirty tree is relevant only when its changes can affect the claims under review.

## Revision Comparison and Fallbacks

When both stored and current revisions are reliable:

1. Compare the relevant paths or behavior between them.
2. Distinguish unrelated repository movement from changes that could affect persisted knowledge.
3. Verify relevant current source before declaring a contradiction or updating metadata.

When revision evidence is limited:

- **Non-Git repository:** record that Git revision and history are unavailable; use current authored files and other available evidence.
- **Unborn branch:** record that no commit revision exists; use the current working tree and state that commit-history comparison is unavailable.
- **Unavailable or unreliable history:** record the specific limitation and use current evidence without claiming change-since-revision coverage.
- **Dirty working tree:** inspect only relevant changes when safe and permitted; record that the verified state may not correspond to a commit.

Never fabricate a commit, branch, date-based revision, or placeholder that could be mistaken for a real revision. Do not reuse a revision from another repository or scope.

## Verification Procedure

1. Establish the active repository root and read existing context without treating it as authority.
2. Select claims using the refresh reason, changed areas, stored scope, and current task.
3. Gather bounded current evidence under the safety exclusions.
4. Classify each relevant area and report evidence and limitations.
5. If repair is needed, choose the smallest repair level and present a proposal.
6. Stop for approval unless conservative prior approval is unambiguously valid.
7. After an approved repair, review the diff and update metadata only for the scope actually verified.

## Repair Levels

```text
Localized stale area -> Targeted update
Multiple related stale areas -> Targeted refresh
Foundational mental model unreliable -> Full re-orientation recommended
```

- A targeted update changes one affected knowledge area.
- A targeted refresh may coordinate several related edits, but it is not whole-document regeneration.
- Full re-orientation is a recommendation that requires separate authorization. Never start it automatically.

If the evidence reveals additional possible problems outside the approved scope, report them and stop rather than silently expanding the repair.

## Approval for Writes

Before any `UPDATE` or `REFRESH` repair, present the affected section, current evidence, proposed change, provenance impact, and known limitations.

Prior approval is valid only when explicit authorization remains available in the current task or conversation for the specific context edit or a clearly defined class of edits that unambiguously includes it. Do not infer it from generic source-edit permission, permission to assess or refresh, historical or unrelated tasks, the file's existence, or an ambiguous response. After resume or compaction, ask again if the authorization or scope is no longer explicit.

Do not create persistent approval state. Approval applies only to the proposal it answers.

## Targeted-Update Precision

- Modify only affected knowledge. Preserve unrelated sections byte-for-byte where practical.
- Do not rewrite unrelated prose because of wording preference, template regeneration, section reordering, language translation, formatting, encoding, or line-ending normalization.
- Preserve unaffected evidence anchors and all human-provided content.
- Preserve the existing document language unless translation was explicitly authorized.
- Inspect the before/after diff. Separate substantive edits from incidental churn and undo unauthorized incidental changes.
- Follow repository-local text policy and existing file conventions. Do not claim precision without diff inspection.

Metadata must not overstate coverage. A targeted repair may update the last-verified value and scope only to describe what was actually checked; it does not make every untouched section `Verified`.

## Human-Provided Knowledge

Repository silence or contradiction in implementation does not by itself authorize deleting human-provided business knowledge. Preserve its provenance and verification limitation. If it appears superseded, report the evidence and request user resolution unless the user already supplied an explicit correction or approved authoritative superseding evidence.
