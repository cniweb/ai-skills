---
name: github-issue-implementation-executor
description: "Subagent skill for implementing GitHub issue requirements in code with minimal scoped changes and tests."
user-invocable: true
---

# GitHub Issue Implementation Executor

## Language / Sprache

- Provide all user-facing outputs in German and English.
- Gib alle nutzerseitigen Ausgaben auf Deutsch und Englisch aus.
- For each major section in summaries, present German first, then English.
- Stelle in jedem Hauptabschnitt von Zusammenfassungen zuerst Deutsch und danach Englisch dar.

## Goal

Implement the approved GitHub issue requirements in the smallest safe set of files and add/update tests.

Implementiere die freigegebenen GitHub-Issue-Anforderungen im kleinsten sicheren Dateiumfang und ergaenze/aktualisiere Tests.

## Inputs You Need

- Requirements list and acceptance criteria.
- Betroffene Dateien/Symbole und Architekturhinweise.
- Coding constraints and branch constraints.
- Test expectations for changed behavior.

## Workflow

1. Confirm scope and assumptions.
- Confirm exact must-have behaviors and non-goals.
- Klaere blockierende Unklarheiten gezielt.

2. Create implementation plan.
- Map requirement to concrete code locations.
- Choose smallest safe diff set.

3. Execute code changes.
- Keep edits scoped to issue behavior.
- Preserve existing APIs unless explicitly required.
- Do not revert unrelated workspace changes.

4. Add/update tests.
- Cover primary behavior and relevant edge cases.
- Add regression test for issue scenario.

5. Self-check before handoff.
- Review touched files for readability and low complexity.
- Note assumptions and potential risks.

## Output Format

1. Implementation Summary
- What changed and why

2. Changed Files
- File-by-file rationale

3. Tests Updated
- Added/modified tests and covered behavior

4. Assumptions and Risks
- Open points requiring user input

## Guardrails

- Prefer minimal diffs.
- Avoid unrelated refactors.
- Never fabricate issue details.
- If blocked by missing context, return precise blocker questions.
