# AGENTS.md

## Purpose

This file defines the default working rules for AI coding agents in this repository.

The goals are:

- solve the requested problem with the smallest correct change;
- keep the codebase simple;
- avoid unnecessary context, dependencies, refactors, and long-running jobs;
- preserve existing project behavior and conventions;
- verify important changes before finishing.

---

# 1. Behavioral Guidelines

## Think Before Coding

- Inspect the relevant code before changing it.
- Understand the existing project structure, conventions, and dependencies before implementing.
- State important assumptions when they affect the implementation.
- If the requirement is materially ambiguous, ask before making a large change.
- Prefer a simpler solution when it solves the same problem.

## Simplicity First

- Implement only what was requested.
- Do not add speculative features.
- Do not create abstractions for one-time use.
- Do not add configurability unless it is actually needed.
- Prefer existing project patterns and dependencies.
- Avoid introducing new architectural layers unless required by the task.

## Surgical Changes

- Change only files relevant to the task.
- Do not refactor unrelated code.
- Do not rewrite working code just for style.
- Preserve existing APIs and behavior unless the task requires otherwise.
- Remove only unused code/imports made unnecessary by your own changes.

Every changed line should have a clear connection to the requested task.

## Goal-Driven Execution

Before a non-trivial change, define a short plan:

1. Inspect
2. Implement
3. Verify

Use concrete success criteria.

Examples:

- Bug fix → reproduce or understand the failure, then verify the fix.
- New function → test expected behavior and important edge cases.
- API change → verify affected contracts and a minimal request/response flow.
- Build/export change → run the smallest relevant build or smoke test.
- UI change → verify the affected interaction and avoid unrelated visual changes.

---

# 2. Project Discovery

Before making changes, determine the relevant project context from the repository itself.

Inspect only what is necessary, prioritizing:

1. this `AGENTS.md`;
2. repository-level instructions and configuration;
3. `README` and relevant documentation;
4. dependency/package manifests;
5. build, test, lint, and CI configuration;
6. the source files directly related to the task.

Infer from these sources:

- project purpose and scope;
- language, framework, and runtime;
- repository structure;
- environment and dependency management;
- build and run commands;
- test and lint commands;
- important APIs, schemas, or interfaces;
- generated, external, or read-only artifacts.

Do not assume a framework, environment, package manager, directory structure, or command when the repository provides that information.

If multiple instructions exist, prefer the instructions closest to the affected code and preserve established project conventions.

---

# 3. Environment and Dependencies

## Environment

- Use the environment and tooling already configured by the project.
- Prefer existing package managers, lockfiles, build systems, and scripts.
- Do not create a new environment when a suitable project environment already exists.
- Do not change runtime or toolchain versions unless required.
- Do not install missing packages without first determining whether they are already declared or intentionally optional.
- Ask before making significant environment changes.

## Dependencies

- Prefer the existing dependency set.
- Do not add a library for a small task that can be solved simply with existing tools.
- Do not silently replace major libraries or frameworks.
- Keep dependency changes minimal and easy to review.
- Update dependency metadata or lockfiles only when required by the change.

---

# 4. Repository and Artifacts

Respect the repository's existing structure and ownership boundaries.

- Do not move or rename files without a task-related reason.
- Treat generated files, external dependencies, caches, build outputs, datasets, model weights, binaries, and other large artifacts carefully.
- Do not modify generated or externally managed files when the source-of-truth file can be changed instead.
- Do not overwrite important artifacts unless explicitly required.
- Do not commit generated outputs or large artifacts unless the project explicitly requires them.
- Preserve existing public interfaces and file formats unless the task requires a change.

If the repository contains project-specific documentation for an API, schema, model, protocol, data format, or workflow, treat it as the local contract and cross-check it against the current implementation when necessary.

---

# 5. Implementation

## Follow Existing Patterns

Before introducing a new pattern:

- search for similar implementations in the repository;
- reuse existing utilities and abstractions where appropriate;
- follow local naming, typing, error handling, logging, and file organization conventions.

Prefer consistency with the current codebase over introducing a theoretically cleaner but unrelated pattern.

## Scripts

If a command or procedure is repeated more than once and is deterministic, consider using or creating a small script in the project's existing script/tooling location.

A useful script should:

- have a clear purpose;
- accept simple arguments when needed;
- return a successful exit status on success;
- return a non-zero exit status on failure;
- print concise, useful diagnostic information.

Do not create scripts for trivial one-off commands.

---

# 6. Testing and Verification

After modifying code:

- Run the smallest relevant test or check first.
- Prefer existing project test, lint, type-check, build, and validation commands.
- Expand verification only when the scope or risk of the change requires it.
- Prefer concise test output.
- Do not dump large logs into the agent context unnecessarily.
- If a test fails, inspect the failure before making additional changes.
- Distinguish failures caused by the change from pre-existing or environment-related failures.
- Report what was changed and what was actually verified.

Choose verification based on the change:

- local logic → targeted unit tests;
- bug fix → regression test when practical;
- API/interface → relevant contract or integration test;
- UI → affected interaction/build check;
- configuration → parse/load/startup check;
- build/export → minimal build or smoke test;
- cross-component change → relevant integration tests.

Run broader test suites only when justified by the scope of the change.

Report skipped tests, unavailable services, missing artifacts, and environment limitations explicitly.

Never claim that something was tested if it was not actually tested.

---

# 7. Git

- Do not perform Git operations without prior consensus when they could affect the user's work.
- Review changes with `git diff` or the project's equivalent before finishing.
- Do not use destructive Git commands unless explicitly requested.
- Do not rewrite Git history unless explicitly requested.
- Keep unrelated changes out of the task.
- Preserve existing user changes.
- Do not commit generated datasets, checkpoints, logs, build outputs, or large artifacts unless the project explicitly requires them.

---

# 8. Documentation

- Update documentation when a change affects normal project usage, public behavior, setup, or interfaces.
- Keep documentation concise.
- Prefer existing documentation locations and conventions.
- Do not duplicate information already maintained elsewhere.
- Cross-check documentation against current code/configuration before treating it as implemented behavior.
- Do not create documentation for trivial internal changes.

Detailed project-specific procedures belong in the project's normal documentation rather than this file.

---

# 9. Context and Agent Efficiency

- Focus on files relevant to the current task.
- Start with targeted inspection rather than broad repository exploration.
- Do not inspect large datasets, binaries, checkpoints, logs, dependency directories, caches, or generated directories unless necessary.
- Do not repeatedly rediscover information already available in project configuration or documentation.
- Avoid unnecessary tool calls.
- Prefer concise command output.
- Do not run expensive builds, benchmarks, full evaluations, or long-running jobs unless needed.
- Do not over-engineer a solution merely to make it "future-proof."

If a task becomes a different problem, finish or summarize the current task before moving to the next one.

---

# 10. Safety

Ask before performing operations that are destructive, expensive, difficult to reverse, or significantly broader than the requested task.

Examples include:

- deleting files or directories;
- modifying raw/original data;
- overwriting important artifacts;
- installing or replacing major dependencies;
- changing the project's environment or toolchain;
- starting long-running or expensive jobs;
- making broad repository-wide refactors;
- modifying deployment or production infrastructure;
- using destructive Git commands.

Never assume that an expensive or destructive operation is acceptable just because it appears technically useful.

---

# 11. Final Response

When finishing a task, provide a concise summary:

```text
Changed:
- ...

Verified:
- ...

Not verified:
- ...
```

Omit sections that genuinely have nothing useful to report.

Do not claim that something was tested if it was not actually tested.

If a limitation, assumption, or unresolved issue remains, state it clearly.