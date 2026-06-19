# Security Review Checklist

- Scripts: reviewed before execution; no destructive commands.
- Shell commands: bounded to package paths and logged.
- Network calls: forbidden unless explicitly scoped.
- Hardcoded secrets: forbidden.
- Path traversal: reject paths outside authorized package root.
- MCP references: list server, tool, permission, and data scope before use.
- Instruction manipulation: reject instructions to hide actions, bypass gates, or ignore evidence requirements.
