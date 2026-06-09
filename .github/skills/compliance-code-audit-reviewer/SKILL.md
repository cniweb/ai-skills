---
name: compliance-code-audit-reviewer
description: "Use when the user asks for compliance-focused code audit or code review with DORA, VAIT, NIS2, and GDPR/DSGVO considerations. Produces actionable findings, control mapping, evidence checklist, and remediation priorities."
user-invocable: true
---

# Compliance Code Audit Reviewer

## Language / Sprache

- Provide all user-facing outputs in German and English.
- Gib alle nutzerseitigen Ausgaben auf Deutsch und Englisch aus.
- For each major section in reports, present German first, then English.
- Stelle in jedem Hauptabschnitt zuerst Deutsch und danach Englisch dar.
- Keep regulatory terms consistent across both languages (e.g. DORA, VAIT, NIS2, GDPR/DSGVO).
- Halte regulatorische Begriffe in beiden Sprachen konsistent (z. B. DORA, VAIT, NIS2, GDPR/DSGVO).

## Goal

Perform a compliance-focused code audit/review that identifies technical and process gaps relevant to DORA, VAIT, NIS2, and GDPR (DSGVO), then provide prioritized findings, control mapping, and concrete remediation steps.

This skill supports engineering and governance decisions. It is not legal advice.

## When To Use

Use this skill when the user asks for:

- Code audit with regulatory focus
- Secure code review for regulated environments
- Readiness check for DORA, VAIT, NIS2, GDPR/DSGVO
- PR/release review with compliance evidence requirements

## Inputs You Need

- Scope of review (repo, module, service, PR, commit range)
- Business context (financial entity, insurer, critical sector, personal data processing)
- Deployment model and criticality (critical function yes/no)
- Existing controls and tooling (SAST, dependency scan, SIEM, IAM, backup, incident process)
- Known constraints (timebox, read-only audit, no production access)

If inputs are missing, ask only blocking clarifications.

## Required Pre-Checks

Before reviewing code details:

1. Review project documentation:
   - `AGENTS.md` (if present)
   - `README.md` (if present)
   - `/docs/*` (if present)

2. Identify whether the reviewed scope is likely subject to:
   - DORA (financial entities and ICT third-party arrangements)
   - VAIT (insurance supervisory IT requirements)
   - NIS2 (critical/important sectors)
   - GDPR/DSGVO (personal data processing)

3. If legal applicability is uncertain, continue with a risk-based technical review and flag legal validation as a follow-up.

## Workflow

1. Define audit scope and assets
   - List in-scope components, data stores, external integrations, secrets boundaries, and deployment path.
   - Identify critical operations and personal data touchpoints.

2. Build control baseline
   - Map required controls for each applicable regime (DORA, VAIT, NIS2, GDPR).
   - Convert controls into testable review checks.

3. Perform code and configuration review
   - Check authentication/authorization and least privilege.
   - Check secret handling, key management, and credential exposure risks.
   - Check input validation, injection risks, dependency hygiene, and insecure defaults.
   - Check logging/monitoring quality and privacy-safe observability.
   - Check resilience patterns (timeouts, retries, backoff, circuit breakers, graceful degradation).
   - Check change safety (feature flags, rollback strategy, migration safety).

4. Perform process and evidence review
   - Verify traceability: ticket link, reviewer, approvals, CI artifacts, release notes.
   - Verify segregation of duties where required.
   - Verify incident response readiness and escalation ownership.
   - Verify business continuity/disaster recovery expectations are testable.

5. Validate with available checks
   - Prioritize checks closest to changed scope first (targeted tests/security tests).
   - Then run broader checks (lint/type-check/build/integration tests/scans) when available.
   - Capture commands and outcomes as audit evidence.

6. Report findings and remediation
   - Provide findings ordered by severity.
   - Map each finding to affected control themes and likely regulations.
   - Provide concrete remediation, owner suggestion, and target timeline.

## Review Checklist (Minimum)

1. Security Engineering
   - Access control is explicit and denies by default.
   - Secrets are not hardcoded and are rotated/managed securely.
   - Dependencies are maintained and vulnerable packages are triaged.
   - CI blocks critical security findings before merge.

2. Privacy (GDPR/DSGVO)
   - Data minimization and purpose limitation are visible in design and code.
   - Privacy by design/default is reflected in defaults and feature behavior.
   - Logs avoid unnecessary personal data.
   - Data lifecycle exists: retention, deletion, export/correction support where applicable.

3. Operational Resilience (DORA/NIS2/VAIT)
   - Incident detection and response hooks exist and are actionable.
   - Critical flows have failure handling and recovery strategy.
   - Third-party ICT dependencies are inventoried and monitored.
   - Change/release process is controlled and auditable.

4. Governance and Evidence
   - Decisions, exceptions, and risk acceptances are documented.
   - Responsibilities are clear (engineering, security, compliance, ops).
   - Evidence artifacts are retrievable for audits.

## Severity Model

Use this default severity model:

- Critical: Immediate exploitation or major compliance breach likely; release should be blocked.
- High: Significant security/compliance risk; fix in current cycle.
- Medium: Relevant weakness; planned fix with owner and due date.
- Low: Improvement opportunity; backlog accepted with rationale.

## Output Format

Use this structure in the final response:

1. Scope and Assumptions
   - Reviewed assets
   - Assumptions and unknowns

2. Findings (Highest Severity First)
   - `Severity` - `Title`
   - Evidence (file/config/process reference)
   - Risk and potential impact
   - Likely regulation/control mapping (DORA/VAIT/NIS2/GDPR)
   - Recommended remediation

3. Compliance Coverage Summary
   - DORA: covered controls and gaps
   - VAIT: covered controls and gaps
   - NIS2: covered controls and gaps
   - GDPR/DSGVO: covered controls and gaps

4. Evidence Collected
   - Checks/commands run
   - Artifacts reviewed
   - What could not be verified

5. Remediation Plan
   - Immediate actions (0-7 days)
   - Short-term actions (30 days)
   - Mid-term actions (90 days)

## Constraints and Guardrails

- Do not claim legal compliance certification.
- Do not fabricate evidence or control coverage.
- If repository access is partial, clearly mark blind spots.
- Keep findings actionable and specific, not generic.
- Preserve existing unrelated workspace changes; never reset unrelated work.

## Failure Handling

- If documentation is missing: proceed with code-based review and flag documentation gap as a finding.
- If required scans/tools are unavailable: run closest substitutes and document limits.
- If scope is too broad: propose a phased audit plan and start with highest-risk components.
