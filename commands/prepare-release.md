# Command: prepare-release

**Invokes:** `devops-engineer` (consuming sign-off from
`code-reviewer`, `security-reviewer`, `qa-engineer`)
**Use when:** a reviewed, tested change is ready to ship.

## Instruction
Run `workflows/deployment.md`: confirm CI is green, deploy to staging,
smoke-check, deploy to production behind explicit approval, record
the release, and confirm a rollback path exists.

## Output
A deployed change with a recorded rollback plan and release notes
handed to `tech-writer`.
