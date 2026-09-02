# DEK Validation Checklist

This is the checklist DEK has been validated against since 0.1.0; see
`BUILD-REPORT.md` (0.1.0) and `BUILD-REPORT-0.1.1.md` (0.1.1 onward)
for the results. A future change should be checked against the same
list before being considered complete.

- [ ] Directory structure matches `README.md`'s described layout.
- [ ] Every required top-level file exists (`DEK-SPEC.md`, `README.md`,
      `VERSION`, `BUILD-REPORT.md`).
- [ ] Every agent file referenced anywhere (in another agent, a
      workflow, a command) exists in `agents/`.
- [ ] Every skill referenced anywhere exists in `skills/` as
      `skills/<name>/SKILL.md`.
- [ ] Every workflow referenced anywhere exists in `workflows/`.
- [ ] Every rule path referenced anywhere exists under `rules/`.
- [ ] Every template referenced anywhere exists in `templates/`.
- [ ] No duplicate agent/skill/workflow/rule/template names.
- [ ] No two rule files give contradictory instructions for the same
      situation.
- [ ] Naming is consistent (kebab-case files, consistent frontmatter
      keys across all agent files, all skill files).
- [ ] Technology coverage matches `DEK-SPEC.md` §6 (SQL Server,
      C#/.NET/ASP.NET Core/EF Core, React/TypeScript, .NET MAUI,
      Git/GitHub, testing, security, CI/CD) with no unrelated
      language/framework content included.
- [ ] Nothing in `agents/`, `skills/`, `workflows/`, `rules/`,
      `commands/`, or `templates/` assumes a specific LLM provider by
      name (aside from `docs/LLM-PROVIDER-GUIDE.md`, which is
      explicitly provider-specific by design).
- [ ] Every security-relevant skill/rule addresses the categories
      listed in `DEK-SPEC.md` §18.
- [ ] Every stack layer (backend, frontend, mobile, database) has at
      least one dedicated testing skill.
- [ ] No file in the DEK package contains a credential, API key,
      token, or secret of any kind.
- [ ] No `.git` metadata from ECC or any other repository is present
      in the package.
- [ ] The archive `DEK-<current-version>.zip` (e.g. `DEK-0.1.1.zip`)
      contains the complete project, no temporary files or caches, and
      is not nested inside itself.
