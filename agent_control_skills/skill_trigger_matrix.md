# Skill Trigger Matrix

- `contract-to-skills`: Convert monolithic agent contracts into bounded skill package specifications. Use when a user asks to split a large deterministic multi-agent contract into small filesystem Agent Skills.
- `execution-trigger-guard`: Decide whether a request authorizes specification-only planning or actual file creation. Use when a task may accidentally mutate files without an explicit run or create instruction.
- `model-reality-boundary`: Separate assistant claims from persisted tool evidence and reject fake PASS states. Use when status, verification, or completion depends on artifacts or command output.
- `role-permission-guard`: Enforce planner, executor, verifier, evaluator, memory, escalation, and release role permissions. Use when one agent role may certify, approve, release, or complete its own work.
- `state-gate-controller`: Control deterministic state transitions using persisted evidence and reject unsupported PASS transitions. Use when work moves between planned, executed, verified, evaluated, gated, or blocked states.
- `artifact-manifest-governor`: Specify artifact manifest records for evidence-bearing outputs. Use when artifacts, checksums, ownership, stage, verifier status, or evaluator status must be tracked.
- `verifier-protocol`: Verify artifacts against structural requirements while rejecting prose-only explanations as evidence. Use when independent artifact checking is required before evaluation.
- `evaluator-protocol`: Evaluate only verifier-approved evidence against contract criteria. Use when pass/fail scoring must be separated from execution and verification.
- `memory-manager`: Record verified package state, in-progress work, blockers, next actions, and known failure patterns. Use when durable project memory is needed without root-file mutation.
- `escalation-manager`: Escalate missing evidence, repeated failure, unavailable tools, invalid state transitions, and authorization gaps. Use when progress is blocked by safety, permissions, or evidence defects.
- `idempotency-checkpointing`: Require idempotency keys and checkpoint records for side effects, artifact writes, tool calls, and state transitions. Use when repeatable execution or recovery is needed.
- `release-gate`: Block final completion claims until verifier PASS, evaluator PASS, required evidence, and zero unresolved escalations are recorded. Use when final handoff or release statements are requested.
- `skill-lifecycle-governance`: Govern skill create, review, test, approve, version, deprecate, rollback, and retire states. Use when skills need enterprise review, risk controls, deployment management, or lifecycle tracking.
- `codex-conflict-safe-build`: Constrain Codex-style agents to build only inside isolated package paths unless root mutation is explicitly authorized. Use when repository root files could collide with generated outputs.
