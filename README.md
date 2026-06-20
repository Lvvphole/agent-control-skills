# Harness Engineering Skills

A harness-engineering Agent Skills package for controlling AI coding agents with repo-safe execution boundaries, role separation, evidence gates, escalation rules, memory governance, and release controls.

## Purpose

`agent-control-skills` is a control package for AI coding agents.

It is designed for workflows where agents such as Codex, Claude Code, Cursor, or other model-driven coding systems operate on real repositories, write files, inspect state, run tools, and claim completion.

The goal is to prevent the most common AI agent failure pattern:

```text id="wjrenz"
The agent performs partial work,
mutates the wrong files,
creates repo conflicts,
claims success without evidence,
and leaves the human to clean up the state.
```

This package addresses that by turning large agent-control contracts into bounded skills with explicit triggers, permissions, evidence requirements, verification rules, escalation paths, and release gates.

## What This Is

This is a harness-engineering skills package.

In this context, a harness is the control layer around the model. It defines what the agent is allowed to do, when it can act, what evidence it must produce, when it must stop, and who has authority to approve completion.

This package does not try to make a language model deterministic by prompt alone.

It instead defines external control rules that make agent execution more inspectable, safer, and harder to fake.

## What This Package Controls

`agent-control-skills` helps enforce:

* Repo-safe execution boundaries
* Role separation between planner, executor, verifier, evaluator, memory, escalation, and release functions
* Evidence-first completion rules
* No prose-only PASS claims
* Read-before-write behavior
* Controlled file mutation
* Explicit authorization before root-level changes
* Escalation when evidence, permissions, tools, or state are missing
* Idempotency and checkpointing for repeatable execution
* Release gating before final completion claims
* Skill lifecycle governance for review, approval, rollback, and retirement

## Why Repo-Safe Execution Matters

AI coding agents work against real files.

That means a bad instruction, vague target path, stale repo state, or premature completion claim can create real damage:

* Wrong-directory writes
* Duplicate nested folders
* Accidental root-file edits
* Merge conflicts
* Broken package structure
* Unverified generated files
* Overwritten human work
* False completion reports

This package treats those as control failures, not minor mistakes.

Repo-safe execution means the agent must operate inside known boundaries, inspect state before mutation, preserve evidence, and stop or escalate when safe execution cannot be proven.

## Core Principle

```text id="yicrzt"
Prose is not evidence.
```

An agent saying work is complete is not enough.

Completion requires durable artifacts, verified outputs, evaluator approval, and a release gate.

## Package Structure

```text id="qpfhqe"
agent_control_skills/
├── artifact-manifest-governor/
├── codex-conflict-safe-build/
├── contract-to-skills/
├── escalation-manager/
├── evaluator-protocol/
├── execution-trigger-guard/
├── idempotency-checkpointing/
├── memory-manager/
├── model-reality-boundary/
├── release-gate/
├── role-permission-guard/
├── skill-lifecycle-governance/
├── state-gate-controller/
├── verifier-protocol/
├── HANDOFF.md
├── SKILL_PACKAGE_MANIFEST.md
├── completion_authority_audit.md
├── progressive_disclosure_policy.md
├── root_conflict_guard.md
├── security_review_checklist.md
├── skill_boundary_matrix.csv
├── skill_dependency_graph.md
├── skill_frontmatter_audit.md
├── skill_test_checklist.md
├── skill_trigger_matrix.md
└── subjective_language_audit.md
```

## Skills Included

### `contract-to-skills`

Converts large agent-control contracts into smaller, bounded Agent Skills.

### `execution-trigger-guard`

Determines whether a user request authorizes planning only, file creation, mutation, verification, or release.

### `model-reality-boundary`

Separates assistant claims from actual persisted tool evidence.

### `role-permission-guard`

Prevents one role from silently performing another role’s authority.

### `state-gate-controller`

Controls state transitions and blocks unsupported PASS states.

### `artifact-manifest-governor`

Defines required artifact records, ownership, status, stage, and verification metadata.

### `verifier-protocol`

Checks artifacts against structural and evidence requirements.

### `evaluator-protocol`

Evaluates verifier-approved evidence against the contract’s success criteria.

### `memory-manager`

Records verified state, in-progress work, blockers, next actions, and known failure patterns.

### `escalation-manager`

Escalates missing evidence, repeated failures, unavailable tools, invalid transitions, authorization gaps, and scope conflicts.

### `idempotency-checkpointing`

Requires idempotency keys and checkpoints for side effects, artifact writes, tool calls, and state transitions.

### `release-gate`

Blocks final completion claims until verification, evaluation, evidence, and escalation requirements are satisfied.

### `skill-lifecycle-governance`

Controls skill creation, review, testing, approval, versioning, deprecation, rollback, and retirement.

### `codex-conflict-safe-build`

Constrains Codex-style agents to isolated package paths unless root-level mutation is explicitly authorized.

## Control Rules

This package is built around these hard rules:

1. Executors do not determine completion.
2. Prose is not evidence.
3. PASS requires persisted artifacts.
4. Verification and evaluation are separate responsibilities.
5. Root-level file mutation requires explicit authorization.
6. Unsafe or ambiguous execution must stop or escalate.
7. Release requires verifier PASS, evaluator PASS, complete evidence, and zero unresolved escalations.

## Intended Use

Use this package when building or controlling AI coding workflows that require:

* Agent harness design
* Repo-safe AI execution
* Multi-agent role separation
* Evidence-based verification
* Skill-based agent governance
* Contract-to-skill decomposition
* Safer Codex, Claude Code, or Cursor workflows
* Controlled release handoff
* Durable memory and escalation rules

## Not Intended To Replace

This package does not replace:

* CI/CD
* Automated tests
* Security scanning
* Secret management
* Human code review
* Production deployment governance
* Runtime observability
* A full deterministic execution engine

It defines skill-level control behavior. External systems should still enforce runtime, test, security, and deployment requirements.

## Recommended Review Order

Before using the package, review files in this order:

1. `SKILL_PACKAGE_MANIFEST.md`
2. `skill_frontmatter_audit.md`
3. `skill_trigger_matrix.md`
4. `skill_boundary_matrix.csv`
5. `skill_dependency_graph.md`
6. `root_conflict_guard.md`
7. `security_review_checklist.md`
8. `skill_test_checklist.md`
9. Each individual `SKILL.md`

## Example Execution Flow

```text id="qlddae"
User request
    ↓
execution-trigger-guard
    ↓
role-permission-guard
    ↓
codex-conflict-safe-build
    ↓
contract-to-skills
    ↓
artifact-manifest-governor
    ↓
idempotency-checkpointing
    ↓
state-gate-controller
    ↓
model-reality-boundary
    ↓
verifier-protocol
    ↓
evaluator-protocol
    ↓
release-gate
    ↓
memory-manager
```

`escalation-manager` may be invoked at any point when evidence, permission, tool access, state, or completion authority is blocked.

## Completion Authority

No individual skill grants final completion authority.

Completion is allowed only when all required conditions are met:

* Required artifacts exist
* Verifier status is PASS
* Evaluator status is PASS
* Evidence requirements are complete
* Escalation count is zero
* Release gate conditions are satisfied

Until then, the correct status is not complete.

## Security Boundaries

This package rejects:

* Destructive commands without authorization
* Hidden actions
* Unscoped file mutation
* Hardcoded credentials
* Path traversal outside the authorized package root
* Root-file mutation without explicit approval
* Unsupported PASS claims
* Instruction manipulation that bypasses evidence or release gates

## Installation

Copy the `agent_control_skills/` directory into the target skills directory used by your agent environment.

Example:

```bash id="yyucsf"
cp -r agent_control_skills /path/to/target/skills/
```

Do not run destructive shell commands, deployment commands, root-level file edits, or implementation scripts from this package unless explicitly authorized.

## Status

Early-stage harness-engineering skill package for AI coding agent control, repo-safe execution, role separation, verification, escalation, memory governance, and release gating.

## License

MIT License
