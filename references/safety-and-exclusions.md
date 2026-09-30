# Safety and Exclusions

Apply this reference before repository orientation or freshness inspection. Prune excluded areas before recursive listing, searching, counting, or content scanning; do not scan them first and filter later.

## Allowed Read-Only Activities

- bounded directory and filename inventory;
- reading authored source, tests, documentation, manifests, project definitions, and non-secret configuration;
- read-only Git status, diff, branch, tag, and bounded history inspection;
- reading dependency and build definitions without restoring dependencies; and
- side-effect-free tool-version inspection when relevant.

Prefer focused inspection and representative samples. Read-only orientation does not authorize changes merely because the workspace is writable.

## Prohibited Without Separate Authorization

Do not independently:

- build, test, lint, format, restore, install, clean, package, or sign;
- launch an application, browser workflow, server, container, emulator, simulator, or device;
- start a background process;
- migrate or seed a database;
- deploy, publish, or release;
- mutate Git state, including checkout, reset, restore, clean, stash, commit, branch, tag, or push operations;
- download dependencies or external data merely for orientation; or
- create or modify `PROJECT_CONTEXT.md` before the operation's approval gate is satisfied.

When a state-changing action is necessary, stop, explain the purpose and impact, and obtain authorization for that specific action.

## Prune Before Recursion

Exclude generated, restored, cached, packaged, and compiled content at any depth, including:

```text
bin/
obj/
build/
out/
artifacts/
TestResults/
.vs/
.gradle/
.kotlin/
.cxx/
.externalNativeBuild/
captures/
node_modules/
generated caches
restored dependencies
compiled binaries and symbols
packaged applications
```

Also honor project-declared build and output directories. Use case-insensitive directory matching on case-insensitive filesystems.

If an excluded-name directory appears to contain authored source or essential build scripts, do not recurse automatically. Disclose the ambiguity and ask the user whether to include that exact area.

## Sensitive and Personal Data

Do not open, print, copy, summarize, or persist:

- `.env` and live secret files;
- secret stores, credentials, tokens, cookies, or credential-bearing profiles;
- private keys, certificates, signing material, PFX, P12, KEY, PEM, KEYSTORE, or JKS content;
- production databases, dumps, user exports, or personal data;
- crash dumps, sensitive telemetry, or large logs that may contain private data; or
- suspicious values that appear to be live credentials even when found in an otherwise readable file.

Sample configuration may be read only when it describes structure without live values. Record a redacted conclusion and safe file reference when sensitive evidence affects the result; never reproduce the value.

## Scope and Repository Boundary

Resolve task-relevant paths inside the active repository. Do not follow a path, symlink, junction, submodule assumption, or nested-repository relationship into another project without establishing that it is in scope. Never reuse context from a parent, child, sibling, or previous repository.

When root selection is ambiguous, stop and ask rather than writing context to a guessed location.

## Validation Fixtures

Later safety tests must use synthetic placeholders that cannot function as real credentials or personal data. Never use live secrets to prove that exclusions work. Phase 1 source review does not establish real-world exclusion compliance; that remains E2E work.
