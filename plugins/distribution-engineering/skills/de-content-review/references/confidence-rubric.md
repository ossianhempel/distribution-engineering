# Confidence rubric (content review)

Every finding carries a **confidence anchor** — a discrete value, never a range or
float. It gates whether the finding is shown. Severity (P0–P3) is a *separate*
axis: how much the issue hurts the post if real. A P1 can be anchor 50; a P3 can
be anchor 100.

| Anchor | Meaning | Emit? |
|--------|---------|-------|
| **100** | Verifiable from the draft alone — a rule is plainly broken (no hook, hard CTA present, a banned slop phrase, over the channel's length limit). No interpretation. | **Yes** |
| **75** | Highly confident the issue will hurt performance with a real audience, and you can name the concrete consequence (scroll-past, no emotional charge, reads as an ad). | **Yes** |
| **50** | Real but arguable — a judgment call a skilled marketer might defend (tone preference, a hook that's fine-but-not-great). | **No**, unless P0 |
| **25** | Might be an issue but you can't support it from the draft. | **No** (silent) |
| **0** | False positive / not actually a problem. | **No** (silent) |

## Gating

- **Suppress anchors below 75.** Exception: a **P0 at anchor 50+** survives — a
  post-killing risk you're only half-sure of must still be seen.
- **Cross-reviewer agreement promotes.** When two personas independently flag the
  same span, promote its anchor one step (50→75, 75→100). Real problems get caught
  from multiple lenses.

## Severity for content

- **P0 — kills the post.** No hook / scroll-past guaranteed; reads as an ad
  (fails the muted test); off-brand enough to damage the voice; hard-sells with no
  standalone value.
- **P1 — significantly weakens it.** Weak hook, buried emotion, product-first
  instead of problem-first, wrong format for the channel.
- **P2 — leaves reach on the table.** Vague where a number/story would land, soft
  slop phrasing, a CTA that could be softer.
- **P3 — polish.** Minor wording, small tightening.
