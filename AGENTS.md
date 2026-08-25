# Repository Instructions

## Scope

- This repository contains reusable GitHub Copilot skills, not an application package.
- Skill definitions live under `.github/skills/<skill-name>/SKILL.md`; preserve each file's YAML frontmatter, name, workflow, guardrails, and output format.
- The README lists fewer skills than are currently present; inspect the directory rather than relying on the list.

## Workflow

- Read `README.md` and the complete relevant `SKILL.md` before editing.
- Keep changes limited to the requested skill and directly related documentation or validation material.
- Existing implementation, validation, and compliance skills define a delegated workflow and bilingual German/English output; `devils-advocate` follows the user's language. Preserve those distinctions.
- There is no package manifest, standard test runner, CI workflow, or repository build command. Do not invent `npm`, `pnpm`, or test commands.
- For Markdown-only changes, inspect formatting and links manually unless an explicitly available linter is being used. Do not install tools without a concrete request.

## Safety

- Preserve unrelated working-tree changes.
- Never add credentials, tokens, private keys, or secret values to skills, examples, documentation, or commits.
- Do not claim validation that was not actually run.
