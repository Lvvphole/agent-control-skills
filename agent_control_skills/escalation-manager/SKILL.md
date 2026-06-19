---
name: escalation-manager
description: Escalate missing evidence, repeated failure, unavailable tools, invalid state transitions, and authorization gaps. Use when progress is blocked by safety, permissions, or evidence defects.
---

# escalation-manager

## Required Escalations
Escalate missing evidence, repeated failure, unavailable tools, invalid state transitions, and authorization gaps.

## Scope
- Allowed: operate only on this skill capability and its declared package artifacts.
- Forbidden: modify root `README.md`, `pyproject.toml`, `.gitignore`, or `project_memory.md` unless the user explicitly authorizes root mutation.
- Forbidden: deploy, run destructive commands, hide actions, hardcode credentials, or access paths outside the target package without explicit authorization.

## Workflow
1. Confirm the trigger matches this skill description.
2. Identify input artifacts and required output evidence.
3. Perform only the allowed bounded action for this skill.
4. Persist evidence in the declared artifact path; do not accept prose as evidence.
5. Send work to the required downstream gate instead of claiming final completion.

## Evidence Required
- Persisted artifact path.
- Artifact owner and stage.
- Verifier status and evaluator status when applicable.
- Escalation record for any missing authorization, missing evidence, scope overlap, or tool limitation.

## When Not To Use
Do not use when another skill owns the requested action, when root mutation is requested without explicit approval, or when the request asks for deployment or destructive operations.

## Stop Conditions
Stop when required evidence is missing, the action would exceed scope, a PASS state lacks persisted evidence, or an escalation condition is met.

## Escalation Conditions
Escalate missing evidence, repeated failure, unavailable tools, invalid state transitions, authorization gaps, unclear script permissions, network requirements, secrets requirements, MCP ambiguity, or scope overlap.

## References
- See `../root_conflict_guard.md` for conflict-safe path rules.
- See `../security_review_checklist.md` for security checks.
- See `../skill_boundary_matrix.csv` for role boundaries.
