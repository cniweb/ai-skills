# Linter Agent Skill

## Purpose

Automatically lint files after creation or modification
to enforce coding standards. Detect the file type, select
the appropriate linter, ensure it is installed, run it,
and fix reported issues.

## Behavior

1. **Detect file type** by extension or filename.
2. **Check linter availability** using `which <linter>`.
3. **Install missing linters** via `brew install <package>`
   (macOS) or the appropriate package manager.
4. **Run the linter** with the correct command and flags.
5. **Fix errors** automatically when unambiguous.
6. **Ask the user** before fixing convention warnings.
7. **Respect project config** — use existing linter config
   files (`.eslintrc`, `pyproject.toml`, etc.) over defaults.

## Supported Languages and Tools

### Markdown (`.md`)

- Linter: `markdownlint-cli2`
- Install: `brew install markdownlint-cli2`
- Command: `markdownlint-cli2 <file>`
- Standard: CommonMark, consistent formatting

### Shell (`.sh`, `.bash`)

- Linter: `shellcheck`
- Install: `brew install shellcheck`
- Command: `shellcheck <file>`
- Standard: POSIX compliance, best practices

### Python (`.py`)

- Linter: `ruff`
- Install: `brew install ruff`
- Command: `ruff check <file>`
- Standard: PEP 8, pyflakes, isort, pyupgrade

#### Python Formatting

- Command: `ruff format --check <file>`
- Standard: PEP 8 / Black-compatible

#### Python Type Checking

- Linter: `mypy`
- Install: `brew install mypy`
- Command: `mypy <file>`
- Standard: PEP 484 Type Hints

### YAML (`.yml`, `.yaml`)

- Linter: `yamllint`
- Install: `brew install yamllint`
- Command: `yamllint <file>`
- Standard: YAML spec, indentation

### JSON (`.json`)

- Linter: `jq`
- Install: `brew install jq`
- Command: `jq . <file> > /dev/null`
- Standard: Valid JSON

### TypeScript (`.ts`, `.tsx`)

- Linter: `eslint`
- Command: `npx eslint <file>`
- Standard: typescript-eslint recommended

### JavaScript (`.js`, `.jsx`)

- Linter: `eslint`
- Command: `npx eslint <file>`
- Standard: eslint:recommended

### CSS / SCSS (`.css`, `.scss`)

- Linter: `stylelint`
- Command: `npx stylelint <file>`
- Standard: stylelint-standard

### Dockerfile

- Linter: `hadolint`
- Install: `brew install hadolint`
- Command: `hadolint <file>`
- Standard: Dockerfile best practices

### Terraform (`.tf`)

- Linter: `tflint`
- Install: `brew install tflint`
- Command: `tflint`
- Standard: Terraform best practices

### HTML (`.html`)

- Linter: `htmlhint`
- Command: `npx htmlhint <file>`
- Standard: W3C compliance, accessibility

### Go (`.go`)

- Linter: `golangci-lint`
- Install: `brew install golangci-lint`
- Command: `golangci-lint run <file>`
- Standard: Go best practices, vet, staticcheck

### Rust (`.rs`)

- Linter: `clippy`
- Command: `cargo clippy`
- Standard: Rust idioms, performance

### Ruby (`.rb`)

- Linter: `rubocop`
- Install: `brew install rubocop`
- Command: `rubocop <file>`
- Standard: Ruby Style Guide

### XML (`.xml`, `.xsl`)

- Linter: `xmllint`
- Install: `brew install libxml2`
- Command: `xmllint --noout <file>`
- Standard: Well-formedness, schema validation

### SQL (`.sql`)

- Linter: `sqlfluff`
- Install: `brew install sqlfluff`
- Command: `sqlfluff lint <file>`
- Standard: SQL formatting, ANSI compliance

### TOML (`.toml`)

- Linter: `taplo`
- Install: `brew install taplo`
- Command: `taplo check <file>`
- Standard: TOML specification

## Coding Standards Reference

### Python

- PEP 8 formatting
- PEP 484 type hints on all public functions
- Import sorting (isort-compatible)
- No unused imports or variables

### Shell (Bash/POSIX)

- Quote all variables
- Prefer `set -euo pipefail`
- Avoid deprecated constructs (backticks to `$(...)`)

### TypeScript / JavaScript

- Strict mode enabled
- No `any` types in TypeScript
- Consistent semicolons and quote style

### Docker

- Minimal base images
- No `latest` tags in FROM
- Multi-stage builds when beneficial
- Non-root USER directive

### YAML / JSON

- Consistent indentation (2 spaces for YAML)
- No duplicate keys

### SQL

- Keywords in UPPERCASE
- Consistent indentation
- Explicit aliases (`AS`)

### Go

- `gofmt` formatting
- Proper error handling (no ignored errors)
- No variable shadowing

### Rust

- `clippy` clean with no warnings
- Idiomatic patterns

## Workflow

```text
File changed or created
        |
        v
Detect file extension / name
        |
        v
Look up linter in supported list
        |
        v
Check: which <linter>
        |
   +---------+---------+
   | missing           | found
   v                   |
brew install  ---------+
        |
        v
Check for project config
(.eslintrc, pyproject.toml, etc.)
        |
        v
Run linter with project config
or sensible defaults
        |
        v
Parse output
        |
   +----------+------------------+
   | errors   | warnings         |
   v          v                  |
Auto-fix   Ask user before fixing
```

## Rules

- Never override existing project linter configuration.
- Only install tools once per session — cache the check.
- When multiple files changed, run linters in batch where
  supported (e.g., `ruff check src/`).
- For Node-based linters without project config, skip or
  use `--no-eslintrc` with minimal defaults.
- Report a summary of fixed issues and remaining warnings.

## Platform Support

### macOS

- Package Manager: Homebrew
- Install: `brew install <package>`

### Linux

- Package Manager: apt / dnf
- Install: `sudo apt install <package>`

### Windows

- Package Manager: scoop / choco
- Install: `scoop install <package>`

Default: macOS with Homebrew. Adapt commands if a different
platform is detected.
