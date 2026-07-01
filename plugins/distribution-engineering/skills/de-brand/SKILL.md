---
name: "de-brand"
description: >-
  Distribution Engineering — create or maintain BRAND.md, the project's
  positioning, audience, voice, and channel standards. Use when starting a new
  product's distribution, defining brand voice, or when prompts like "set up the
  brand doc", "define our voice", "who are we writing for", or "what's our
  positioning" come up. The foundational doc other de-* skills read as grounding.
triggers:
  - brand doc
  - brand voice
  - define voice
  - positioning
  - who are we for
  - target audience
  - ICP
  - distribution engineering
  - de-brand
  - set up the brand
---

# Distribution Engineering — Brand

**Distribution Engineering** treats getting a product seen and adopted as an
engineered, compounding system — the marketing-side analog of compound
engineering. `de-brand` produces and maintains **`BRAND.md`**, the durable anchor
that every other `de-*` skill reads as grounding.

`BRAND.md` lives at the repo root, a peer of `README.md`. It is **per-project** —
each product defines its own positioning, audience, and voice. It is short by
design: sharp answers to a few questions beat pages of prose.

## Interaction Method

Ask questions using the platform's blocking question tool: `AskUserQuestion` in
Claude Code (call `ToolSearch` with `select:AskUserQuestion` first if its schema
isn't loaded), `request_user_input` in Codex, `ask_user` in Gemini. Fall back to
a numbered list in chat only when no blocking tool exists or the call errors —
not merely because a schema load is required. Never silently skip a question or
auto-fill an answer.

Ask **one question at a time**. Prefer free-form responses for substantive
sections (positioning, audience, voice); reserve single-select for routing
(which section to revisit). Push back on weak, generic, or slop answers before
writing them — a vague brand doc is worse than none.

## Core Principles

1. **Anchor, not campaign.** `BRAND.md` is who you are and who you serve.
   Specific posts and tactics live elsewhere (later `de-*` skills). Keep them out.
2. **Voice is shown, not described.** "Casual and friendly" is useless. Capture
   voice as concrete do/don't rules with real example lines.
3. **Short is a feature.** The template is constrained. Adding sections costs more
   than it looks. Push back on expansion.
4. **Rerunnable.** On a second run, update in place: preserve what works, only
   challenge sections that read stale, generic, or weak.
5. **Self-contained.** This skill depends on no other skill. It reads and writes
   one file.

## Execution Flow

### Phase 0: Route by File State

Read `BRAND.md` at the repo root with the native file-read tool.

- **Does not exist** → first run. Announce "No brand doc yet — let's write it."
  Go to Phase 1.
- **Exists** → announce "Found BRAND.md — let's review and update." Ask which
  section(s) to revisit (or "all"), then run Phase 1 only for those, seeding
  answers from the current file.

### Phase 1: Interview

Run in document order. For each, ask, then pressure-test the answer against the
"reject if" bar before accepting it.

1. **Positioning** — one sentence: what this product is and the single reason it
   wins. *Reject if:* it lists features, hedges with "and also", or could
   describe any competitor.

2. **Who it's for** — the specific person, their situation, and the moment they'd
   reach for this. *Reject if:* "everyone", a demographic with no context, or a
   persona so broad no single post could speak to it.

3. **The wedge** — what this product / you are *known for* that others aren't; the
   angle you own. *Reject if:* generic ("high quality", "easy to use") or not
   actually differentiated.

4. **Voice** — 3–5 concrete rules, each with a one-line example of the voice
   applied and (where useful) its opposite. Probe for what the voice **never**
   does. *Reject if:* adjectives with no example, or rules that contradict.

5. **Channels** — which channels this product shows up on, and the one-line
   standard for each (format, angle, cadence intent). *Reject if:* "all of them"
   or a channel with no stated reason to be there.

Optional, only if the user volunteers substance:

6. **Proof** — the credibility anchors (results, credentials, social proof) posts
   can lean on.
7. **Off-limits** — topics, claims, or tones this brand will not touch.

After each accepted answer, reflect it back in one tightened line and move on.

### Phase 2: Write BRAND.md

Write the file using the exact template below. Fill only what the interview
produced; omit optional sections with no content rather than leaving placeholders.
Keep every entry tight — this doc is read on every run of downstream skills.

```markdown
# Brand — <product name>

**Positioning:** <one sentence>

## Who it's for
<the person, their situation, the moment they reach for this>

## The wedge
<what this is known for that others aren't>

## Voice
- <rule> — e.g. "<example line>" (not "<opposite>")
- <rule> — e.g. "<example line>"
- <rule> — e.g. "<example line>"

**Never:** <what the voice never does>

## Channels
- **<channel>** — <format / angle / cadence intent>
- **<channel>** — <format / angle / cadence intent>

## Proof            <!-- omit if empty -->
- <credibility anchor>

## Off-limits        <!-- omit if empty -->
- <topic / claim / tone to avoid>
```

### Phase 3: Confirm

Show the written path and a two-line summary (positioning + wedge). State that
downstream `de-*` skills will read this as grounding. Do not push further work —
end cleanly.

## Notes for future de-* skills

`BRAND.md` is the read-side contract. Later skills (`de-distribution`,
`de-ideate`, `de-write`, `de-content-review`, `de-compound`) load it for
grounding and voice enforcement. Keep this template stable; if a field is added,
update those readers deliberately.
