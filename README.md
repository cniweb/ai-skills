# ai-skills

Example repository with reusable GitHub Copilot skills.

## Skills overview

All skill definitions are stored in `.github/skills/<skill-name>/SKILL.md`.

| Skill | Description |
| --- | --- |
| `compliance-code-audit-reviewer` | Performs compliance-focused code audits (DORA, VAIT, NIS2, GDPR/DSGVO) with prioritized findings, control mapping, and remediation actions. |
| `github-issue-implementer` | Orchestrates end-to-end GitHub issue delivery: understands requirements, delegates implementation and validation, then summarizes outcomes. |
| `github-issue-implementation-executor` | Subagent focused on minimal, scoped code implementation and test updates for defined GitHub issue requirements. |
| `github-issue-validation-runner` | Subagent that validates issue changes with prioritized checks and reports evidence plus residual risks. |

## Install skills

1. Copy the desired skill folder from this repository (`.github/skills/<skill-name>/`) into your target repository at the same path: `.github/skills/<skill-name>/`.
2. Ensure the file `SKILL.md` exists in the target skill folder.
3. Commit and push the changes to your repository.
4. Restart or refresh Copilot Chat in that repository so the skill is discovered.

## Use skills

1. In Copilot Chat, invoke the skill by name and provide task context.
2. Include required inputs (for example scope, issue URL, acceptance criteria, and constraints).
3. Answer any blocking clarification questions from the skill.
4. Review the result and run follow-up actions (implementation, validation, review) as needed.
