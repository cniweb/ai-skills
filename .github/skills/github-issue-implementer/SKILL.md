---
name: github-issue-implementer
description: "Use when the user asks to read a GitHub issue, understand requirements, implement the fix or feature in code, add tests, and summarize changes with verification steps. Trigger phrases: GitHub issue, issue URL, implement issue, fix issue #123, resolve ticket."
user-invocable: true
---

# GitHub Issue Implementer

## Language / Sprache

- Provide all user-facing outputs in German and English.
- Gib alle nutzerseitigen Ausgaben auf Deutsch und Englisch aus.
- For each major section in summaries, present German first, then English.
- Stelle in jedem Hauptabschnitt von Zusammenfassungen zuerst Deutsch und danach Englisch dar.
- Keep issue terminology aligned across both languages (for example requirement/Anforderung, blocker/Blocker).
- Halte die Issue-Terminologie in beiden Sprachen konsistent (z. B. requirement/Anforderung, blocker/Blocker).

## Goal

Read a GitHub issue, extract actionable requirements, implement the requested behavior in the current workspace, verify with tests or checks, and return a concise implementation summary.

## Inputs You Need

- Issue reference: full URL (preferred) or `owner/repo#number`
- Target branch or constraints (if provided)
- Acceptance criteria (if provided)
- Any environment limits (offline, no credentials, no network)

If key inputs are missing, ask only the minimum clarifying questions required to proceed.

## Prerequisite: Review Project Documentation First

Before mapping requirements or editing code, review project guidance and conventions in:

- `AGENTS.md` (if present)
- `README.md` (if present)
- `/docs/*` files (if present)

Use these sources to align implementation approach, coding conventions, test strategy, and validation commands with the project's documented standards.

## Orchestrator Sequence (Main Skill + Subagents)

Use this mandatory execution order:

1. Main skill (`github-issue-implementer`): parse issue, derive requirements, and map impacted code locations.
2. Subagent skill (`github-issue-implementation-executor`): implement requirements and update tests.
3. Subagent skill (`github-issue-validation-runner`): run prioritized validation checks and report evidence.
4. Main skill (`github-issue-implementer`): consolidate outputs and produce the final bilingual summary.

Handoff requirements between steps:

- Main -> Implementation subagent:
	- Requirements list, acceptance criteria, impacted files/symbols, constraints, assumptions.
- Implementation -> Validation subagent:
	- Changed file list, test changes, implementation assumptions, known risk areas.
- Validation -> Main:
	- Commands executed, pass/fail/skip results, diagnostics, residual risks, skipped checks.

If a subagent returns blockers, stop the sequence at that step, ask only blocking clarifications, then resume from the blocked step.

## Workflow

1. Parse and fetch the issue
- If a URL is provided, read it with available web tools.
- If `owner/repo#number` is provided, build the issue URL and fetch it.
- Collect: title, body, labels, linked tasks, and relevant comments.
- If the issue cannot be fetched (private repo, auth, network), ask the user to paste the issue content and continue.

2. Convert issue text into implementation requirements
- Produce a short requirements list.
- Separate must-have behavior from optional improvements.
- Identify acceptance criteria and edge cases.
- Note ambiguities and resolve only blocking ones with targeted questions.

3. Map requirements to codebase locations
- Search the workspace for entry points, related symbols, tests, and configs.
- Prefer existing architecture and conventions over introducing new patterns.
- Identify the smallest safe set of files to change.

4. Implement changes end-to-end
- Delegate implementation to a dedicated subagent using the separate skill `github-issue-implementation-executor`.
- Skill file: `.github/skills/github-issue-implementation-executor/SKILL.md`
- Subagent inputs: requirements, affected files/symbols, coding constraints, and acceptance criteria.
- Require the subagent to return:
	- List of changed files and rationale.
	- Summary of implementation decisions and assumptions.
	- Any blockers requiring user input.

5. Validate
- Delegate validation to a dedicated subagent using the separate skill `github-issue-validation-runner`.
- Skill file: `.github/skills/github-issue-validation-runner/SKILL.md`
- Subagent inputs: changed files, project toolchain, and required quality checks.
- Require the subagent to return:
	- Commands executed.
	- Pass/fail results with key diagnostics.
	- Remaining risks, skipped checks, and justification.

6. Summarize outcome
- What was implemented.
- Files changed and why.
- Verification performed and results.
- Any residual risks or follow-up tasks.

## Implementation Rules

- Prefer minimal, targeted diffs.
- Preserve public APIs unless the issue explicitly requires a breaking change.
- Keep naming and style consistent with nearby code.
- Add short comments only where logic is not obvious.
- Never fabricate issue details; clearly mark assumptions.
- If the working tree is dirty, do not revert or overwrite unrelated existing changes; limit edits to issue-scoped files and integrate safely with current workspace state.

## Clean Code and Maintainability Requirements

- Write readable code first: choose intention-revealing names for variables, functions, classes, and tests.
- Keep units small and cohesive: each function/class should have one clear responsibility.
- Avoid deep nesting and overly complex conditionals; favor guard clauses and simple control flow.
- Prefer composition and existing abstractions over ad-hoc duplication.
- Do not introduce clever or opaque patterns when a straightforward solution is available.
- Keep side effects explicit and localized; avoid hidden state changes.
- Maintain stable interfaces and contracts unless the issue explicitly requires a change.
- Add or improve tests to cover primary behavior, edge cases, and regressions introduced by the issue.
- Ensure error handling is clear and actionable; fail with meaningful messages where appropriate.
- Leave touched code in a better state: small opportunistic cleanups are allowed if directly adjacent and low risk.

## Output Format

Use this structure in the final response:

1. Issue Understanding
- Problem statement
- Acceptance criteria

2. Changes Implemented
- File-by-file summary

3. Validation
- Commands/checks run
- Results

4. Notes
- Open questions, limitations, or follow-ups

## Failure Handling

- If issue access fails: request pasted issue content and continue.
- If workspace lacks needed code: explain the gap and propose the smallest viable next step.
- If tests are missing: add focused tests where possible and document coverage limits.
