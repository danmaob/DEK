# Using DEK with Different LLM Providers

DEK's content (`agents/`, `skills/`, `workflows/`, `rules/`,
`commands/`, `templates/`) is plain Markdown with no provider-specific
syntax. The notes below cover only how to *load* that content into
each provider's interface — the content itself never changes.

## Claude (claude.ai, Claude Code, API)
- **Chat-only:** paste the relevant `agents/<name>.md` file as your
  first message or as a Project/Custom Instructions field, followed by
  the skill(s) the current workflow stage names.
- **Claude Code / subagent-capable tools:** `agents/*.md` files can be
  used directly as subagent definitions (they already use YAML
  frontmatter); place the skills a given agent needs alongside it if
  your tool supports a skills directory.

## ChatGPT / Codex
- **Chat-only:** paste the agent file as a system-style instruction at
  the start of a conversation (or into a saved custom GPT's
  instructions field), then the relevant skill file(s).
- **Codex CLI/app:** the agent + skill content can be placed in an
  `AGENTS.md`-style project instruction file if your Codex setup reads
  one; otherwise use it as chat-pasted instructions per session.

## Gemini
- Paste the agent file into a Gemini system-instruction field (Gemini
  API's `system_instruction`, or the persona/instructions field in
  Gemini's chat UI), then the relevant skill file(s) as the first
  user turn.

## Qwen and other capable models
- Any model that accepts a system prompt or an initial instruction
  turn can use DEK the same way: agent file first, then the 1–3
  relevant skill files, then the actual task.

## General notes for any provider
- Load one agent per turn/session — do not paste the entire `DEK/`
  tree.
- Re-paste the agent + skills at the start of a new session; do not
  assume a new session remembers a previous one's chat history — that
  is exactly why workflow outputs are saved as files (see
  `skills/free-tier-llm-operating-model/SKILL.md`).
- If a provider supports a persistent "custom instructions" or
  "project instructions" feature, `rules/common/*.md` is a reasonable
  default to keep loaded there, since those rules apply regardless of
  task.
