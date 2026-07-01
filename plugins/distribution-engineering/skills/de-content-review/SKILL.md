---
name: "de-content-review"
description: >-
  Distribution Engineering — review a piece of social/marketing content before
  publishing. Spawns a panel of persona subagents (hook, resonance, CTA/value,
  channel-fit, slop/voice) grounded in BRAND.md and DISTRIBUTION.md, gates their
  findings by confidence, and returns a ship / revise / rewrite verdict. Use for
  "review this post", "is this hook good", "check this before I publish", a
  tweet/thread/TikTok slideshow/LinkedIn/IG draft, or any short-form copy.
triggers:
  - review this post
  - review my content
  - is this hook good
  - check this before I publish
  - content review
  - review this tweet
  - review this thread
  - review this slideshow
  - de-content-review
  - will this go viral
---

# Distribution Engineering — Content Review

The marketing analog of code review. A panel of specialized persona subagents
each read the draft through one lens, findings are gated by confidence and
merged, and you get a clear verdict: **ship**, **revise** (with must-fixes), or
**rewrite**. Grounded in the project's own `BRAND.md` and `DISTRIBUTION.md` so it
enforces *your* voice and channel standards, not generic advice.

The personas encode hard-won organic-marketing principles: the "golden flow"
(scroll-stop → curiosity → emotion → product), the muted-ad test, ≤10-word hooks,
value-standalone content, soft CTAs, and platform-native format.

## Interaction Method

Use the platform's blocking question tool for the few routing questions
(`AskUserQuestion` in Claude Code — load its schema via `ToolSearch` with
`select:AskUserQuestion` if needed; `request_user_input` in Codex). Fall back to
a numbered list only if no blocking tool exists.

## Execution Flow

### Stage 1: Scope the draft

Get three things:
- **The draft** — a pasted block, a file path, or a `docs/content/*.md` piece.
  Support reviewing multiple variants at once (rank them).
- **The channel** — X post / X thread / TikTok slideshow / LinkedIn / IG / other.
  If not stated, ask (single-select). Channel drives channel-fit and which
  conditional personas run.
- **The format/goal** if useful — e.g. "hook test", "full draft", "just the CTA".

### Stage 2: Ground in the brand

Read `BRAND.md` (voice, positioning, audience, the wedge, off-limits) and
`DISTRIBUTION.md` (per-channel standards) at the repo root if they exist. Extract
a 2–3 line **context block** (who this is for, the voice rules, the channel
standard) and pass it verbatim to every persona. If the files are absent, say so
and review against the generic principles only — voice checks will be weaker.

### Stage 3: Select the panel

**Always-on** (every review):
- `de-hook-reviewer` — the first line / first 3 seconds
- `de-resonance-reviewer` — the golden flow, emotion, specificity
- `de-cta-reviewer` — soft CTA, value-standalone, product-as-tool
- `de-slop-reviewer` — AI-slop + voice drift (reads `BRAND.md`)

**Conditional:**
- `de-channel-fit-reviewer` — run whenever a channel is known (nearly always);
  it adapts its checks to the declared channel.

Announce the panel in one line before spawning.

### Stage 4: Spawn the panel in parallel

Dispatch the selected personas concurrently (respect harness concurrency limits).
Pass each: the draft, the channel, the Stage-2 context block, and the confidence
rubric (`references/confidence-rubric.md`). Personas are read-only — they return
findings, they do not edit the draft.

Each finding has: `dimension`, `severity` (P0–P3), `span` (the exact quoted text
it's about), `why` (the concrete consequence, grounded in a principle),
`suggested_rewrite`, and `confidence` (anchor).

### Stage 5: Merge and gate

Read `references/confidence-rubric.md` and apply it:
- **Dedup** findings that target the same span (normalize whitespace/case).
- **Promote on agreement** — two personas on the same span → anchor up one step.
- **Gate** — drop anchors below 75, except a P0 at anchor 50+ survives.
- Sort by severity, then anchor. Assign stable numbers.

### Stage 6: Verdict

Open with one of:
- **SHIP** — no surviving P0/P1. Note any P2/P3 as optional polish.
- **REVISE** — surviving P1s (or P2 clusters). List the must-fixes with their
  suggested rewrites, in priority order.
- **REWRITE** — a surviving P0 (no hook, reads as an ad, off-brand, hard-sell with
  no standalone value). The draft's foundation is wrong; propose a fresh angle.

Then the ranked findings (severity → number → span → why → suggested rewrite).
For multiple variants, end with a ranking and which to ship.

Keep the output tight and quotable. Vague content feedback is itself slop — every
finding names the exact span and the concrete reason it costs reach.

## After shipping

When the piece goes live, log it with `de-compound` (planned) so its result feeds
back into `de-ideate` and future reviews. Review catches problems before publish;
the compounding loop makes the next draft start smarter.
