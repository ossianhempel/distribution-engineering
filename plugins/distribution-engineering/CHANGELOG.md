# Changelog

## 0.1.0 — Unreleased

Initial scaffold.

- Marketplace + plugin manifests for Claude Code, Codex, and Cursor.
- `de-brand` skill: interview-driven creation and maintenance of `BRAND.md`
  (positioning, audience, the wedge, voice rules, channel standards).
- `de-slop-reviewer` subagent: AI-slop + voice-drift content-review persona.
- `scripts/gen-codex-agents.py`: dependency-free installer that generates native
  Codex TOML agents from the canonical `agents/*.md` (manifest-pruned). Codex-first
  subagent support; Claude Code reads the markdown directly.
- `AGENTS.md`: the Distribution Engineering operating philosophy, building blocks
  (skills + subagents), and roadmap.
