# Distribution Engineering

**The marketing-side analog of [compound engineering](https://github.com/EveryInc/compound-engineering-plugin).**

Compound engineering makes each unit of *engineering* work easier than the last.
Distribution Engineering does the same for the work of getting a product **seen
and adopted** — brand, content, and channels treated as an engineered system that
compounds with every post.

> Distribution is not a dark art or an ad budget. It's a system. The first post
> takes research. Log what it taught you, and the next takes minutes and is
> data-informed. Knowledge compounds; reach compounds.

A plugin of AI-agent skills (Claude Code · Codex · Cursor) that scaffold and
maintain a small set of durable files next to your code, then run a compounding
loop over them.

## Canonical files

Each is a per-project artifact at your repo root — a peer of `README.md`:

| File | Skill | Holds |
|------|-------|-------|
| `BRAND.md` | `de-brand` | Positioning, audience, the wedge, voice rules, channels |
| `DISTRIBUTION.md` | `de-distribution` | Channel playbook: format, angle, cadence |
| `DESIGN.md` | `de-design` | Visual identity and asset conventions |
| `docs/content/*.md` | `de-compound` | One file per published piece + its result |

## The compounding loop

```
de-ideate → de-write / de-design → de-content-review → de-ship
                                                          │
                                                  de-compound (log result)
                                                          │
                                                  de-pulse (mine patterns) ──► feeds de-ideate
```

After ~30 logged posts, ideation stops giving generic advice and starts telling
you which hooks land for *your* audience.

## Status

Early. Built outward from the anchor, one skill at a time, as real use demands it.

- [x] **`de-brand`** (skill) — brand voice, positioning, audience → `BRAND.md`
- [x] **`de-content-review`** (skill) — persona-panel review → ship/revise/rewrite
- [x] **Review panel** (5 subagents) — hook · resonance · CTA/value · slop/voice · channel-fit
- [ ] `de-distribution` — channel playbook → `DISTRIBUTION.md`
- [ ] `de-design` — visual identity → `DESIGN.md`
- [ ] `de-ideate` / `de-write` — the make loop (feeds the review)
- [ ] `de-compound` / `de-pulse` — the compounding spine

## Install

**Codex** (skills/commands install natively; one extra step installs subagents):

```
codex plugin marketplace add ossianhempel/distribution-engineering
codex plugin install distribution-engineering@distribution-engineering
# subagents — Codex runs them natively but doesn't yet auto-install them from a plugin:
python3 <plugin>/scripts/gen-codex-agents.py
```

**Claude Code** (skills and subagents both native, no extra step):

```
/plugin marketplace add ossianhempel/distribution-engineering
/plugin install distribution-engineering@distribution-engineering
```

Then, in any project:

```
/de-brand
```

## How it's built

A marketplace repo (`.claude-plugin/marketplace.json`) wrapping a single plugin
under `plugins/distribution-engineering/`, with `.claude` / `.codex` / `.cursor`
manifests so the same building blocks work across agents.

- **Skills** live in `skills/<name>/SKILL.md` — the workflows you invoke.
- **Subagents** live in `agents/<name>.md` — specialized personas skills spawn
  (e.g. the `de-content-review` panel). One canonical markdown file per agent:
  Claude Code reads it directly; `scripts/gen-codex-agents.py` generates the
  native Codex TOML (`~/.codex/agents/`). Both runtimes run subagents natively.

See [`plugins/distribution-engineering/AGENTS.md`](plugins/distribution-engineering/AGENTS.md)
for the operating philosophy and contributor notes.

## License

MIT
