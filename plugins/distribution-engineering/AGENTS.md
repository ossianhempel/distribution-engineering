# Distribution Engineering

The marketing-side analog of compound engineering. Where compound engineering
makes each unit of *engineering* work easier than the last, Distribution
Engineering does the same for the work of getting a product **seen and adopted**.

## The thesis

Distribution is not a dark art or an ad budget. It is an engineered system that
compounds. The first post takes research. Log what it taught you — the hook, the
format, the channel, the result — and the next post takes minutes and is
data-informed. Knowledge compounds; reach compounds.

This is the "distribution engineer" operating model: treat brand, content, and
channels as versioned, inspectable artifacts that live next to the code, not as
vibes in someone's head.

## Canonical files

The skills read and write a small set of durable, well-known files at the repo
root — peers of `README.md`:

| File | Owner skill | What it holds |
|------|-------------|---------------|
| `BRAND.md` | `de-brand` | Positioning, audience, the wedge, voice rules, channel standards |
| `DISTRIBUTION.md` | `de-distribution` | Channel playbook: format, angle, and cadence per channel |
| `DESIGN.md` | `de-design` | Visual identity and asset conventions |
| `docs/content/*.md` | `de-compound` | One file per published piece + its result — the compounding memory |

Files are **per-project**. Each product defines its own brand and voice. Keep the
templates stable so downstream skills can rely on them.

## The compounding loop

```
de-ideate ──reads──► BRAND / DISTRIBUTION + docs/content/ (past results)
    │
    ▼
de-write / de-design ──► de-content-review ──► de-ship
                                                  │
                                                  ▼  (later, with metrics)
                                          de-compound ──► docs/content/<piece>.md
                                                  │
                                                  ▼
                                          de-pulse mines it all ──► feeds de-ideate
```

## Principles

1. **Anchor, not campaign.** `BRAND.md` is who you are and who you serve. Tactics
   live in the make/ship skills, results in the content memory.
2. **Voice is shown, not described.** Capture voice as concrete do/don't rules
   with real example lines, never adjectives.
3. **Short is a feature.** Constrained templates. Adding sections costs more than
   it looks.
4. **Compounding over campaigns.** The value is the memory that accrues, not any
   single post. Always log the result.
5. **Anti-slop.** Distribution Engineering exists partly to fight generic
   AI-generated marketing. Reviewers actively hunt hollow hype, em-dash soup, and
   voice drift.

## Two kinds of building blocks

- **Skills** (`skills/<name>/SKILL.md`) — the workflows a user invokes (`/de-brand`).
  They own the canonical files and orchestrate the loop.
- **Subagents** (`agents/<name>.md`) — specialized personas a skill spawns to do
  focused, parallelizable work. The review skills fan out to a panel of these,
  the compound-engineering way.

### How subagents stay native on both runtimes

The canonical source is one Claude-Code-flavoured markdown file per agent
(`agents/<name>.md`: frontmatter `name`, `description`, `model`, `tools`, `color`
+ a system-prompt body).

- **Claude Code** reads `agents/*.md` directly when the plugin is installed. No
  generation.
- **Codex** runs custom agents natively too — but as **TOML** in
  `~/.codex/agents/<plugin>/`, and its plugin-install flow does not yet pick
  agents up from a manifest (skills/commands/MCP it does, via
  `.codex-plugin/plugin.json`). `scripts/gen-codex-agents.py` bridges that one
  gap: it reads `agents/*.md` and writes native Codex TOML
  (`developer_instructions` + `sandbox_mode`, inferred from the tools list),
  manifest-pruned so it never clobbers hand-authored files. This mirrors how
  compound-engineering's converter and `agent-scripts/gen-subagents.py` work.

One source of truth; both runtimes native. Re-run the script after adding or
editing an agent.

## Roadmap

Built outward from the anchor, only as real use demands each one.

Skills:
1. **`de-brand`** ✅ — brand voice, positioning, audience → `BRAND.md`
2. **`de-content-review`** ✅ — persona-panel review of a draft → ship/revise/rewrite
3. `de-distribution` — channel playbook → `DISTRIBUTION.md`
4. `de-design` — visual identity → `DESIGN.md`
5. `de-ideate` → `de-write` — the make loop (feeds `de-content-review`)
6. `de-compound` + `de-pulse` — the compounding spine (log results, mine patterns)

Subagents (the `de-content-review` panel — all read-only):
- **`de-hook-reviewer`** ✅ — does the first line / first 3s stop the scroll?
- **`de-resonance-reviewer`** ✅ — the golden flow: emotion + specificity before product
- **`de-cta-reviewer`** ✅ — soft CTA, standalone value, product-as-tool
- **`de-slop-reviewer`** ✅ — AI-slop + voice-drift detector (reads `BRAND.md`)
- **`de-channel-fit-reviewer`** ✅ — platform-native format per `DISTRIBUTION.md`

## For contributors

Building blocks are self-contained: each depends only on the canonical files and
its own inputs, never on other skills or subagents outside this plugin. Add a
skill as `skills/<de-name>/SKILL.md` (quoted frontmatter: `name`, `description`,
`triggers`) or a subagent as `agents/<de-name>.md` (frontmatter: `name`,
`description`, `model`, `tools`, `color`). Keep files small and readable.
