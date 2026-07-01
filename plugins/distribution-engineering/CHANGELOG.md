# Changelog

## 0.2.0 — Unreleased

- `de-content-review` skill: spawns a panel of persona subagents, grounds them in
  `BRAND.md` + `DISTRIBUTION.md`, gates findings by an anchored confidence rubric,
  and returns a ship / revise / rewrite verdict.
- Review panel subagents (read-only), grounded in organic-marketing principles
  (the golden flow, the muted-ad test, ≤10-word hooks, value-standalone, soft CTAs,
  platform-native format): `de-hook-reviewer`, `de-resonance-reviewer`,
  `de-cta-reviewer`, `de-channel-fit-reviewer` (joining `de-slop-reviewer`).
- `skills/de-content-review/references/confidence-rubric.md`: shared gating rubric.

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
