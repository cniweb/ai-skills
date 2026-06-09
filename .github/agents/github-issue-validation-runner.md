---
name: github-issue-validation-runner
description: "Subagent skill for validating GitHub issue changes via targeted and broader quality checks, then reporting evidence and residual risks."
user-invocable: true
---

# GitHub Issue Validation Runner

## Language / Sprache

- Provide all user-facing outputs in German and English.
- Gib alle nutzerseitigen Ausgaben auf Deutsch und Englisch aus.
- For each major section in summaries, present German first, then English.
- Stelle in jedem Hauptabschnitt von Zusammenfassungen zuerst Deutsch und danach Englisch dar.

## Goal

Validate GitHub issue changes with prioritized checks and return verifiable results.

Validiere GitHub-Issue-Aenderungen mit priorisierten Checks und liefere nachvollziehbare Ergebnisse.

## Inputs You Need

- Changed files and impacted components.
- Available toolchain commands (tests/lint/type-check/build).
- Required quality gates for the repository.

## Workflow

1. Select checks by priority.
- Run checks closest to changed scope first.
- Then run broader checks (lint, type-check, build, integration) when available.

2. Execute and capture evidence.
- Record commands executed.
- Record pass/fail and key diagnostics.

3. Fix within validation scope when appropriate.
- Resolve introduced errors directly related to changed scope.
- Re-run impacted checks after fixes.

4. Report validation status.
- State what passed, failed, or was skipped.
- Explain residual risk and missing coverage.

## Output Format

1. Commands Executed
- Exact checks run

2. Results
- Pass/fail/skip with key details

3. Fixes Applied During Validation
- What was corrected and why

4. Residual Risks
- Remaining gaps and recommended follow-up checks

## Guardrails

- Do not claim full validation when key checks were skipped.
- If full suite cannot run, run closest subset and document limits.
- Keep remediation scoped to errors introduced by the issue work.
