# How Pre-cost works

> **Pre-cost is not an official Microsoft skill or feature. It is a community
> example — use it as inspiration and adapt it to your own business needs.**
> All numbers are planning estimates, not bills — check the real cost with the
> free `/cost` command after the task.

This page summarizes the logic in [`skill/SKILL.md`](../skill/SKILL.md). The
skill files are the source of truth; if this page and a skill file disagree,
the skill file wins.

## The 7 steps

**1. Read the prompt (no lookups).** Pre-cost reads only the task text and the
names, types and sizes of any attachments. It extracts the outcome
(deliverables and quality bar), actions (send, schedule, post, browse), context
sources, recurrence, and the current model and effort if the session shows them.

**2. Clarify only if it changes the answer.** If something unknown would move
the class, change the route or multiply the cost, it asks up to 3 short
questions in one go: outcome, scope and frequency. If the prompt already
answers them, it skips this step.

**3. Estimate.** It picks Light, Medium or Heavy from Microsoft's official task
bands, applies at most one bump up or down, maps the model to a tier
(Efficient, Baseline, Premium or Auto) and places the estimate inside the band
by reasoning effort. Automations get a per-run and a per-month figure. It also
works out a lean option and its minimum, and the share of a monthly credit
limit. All numbers come from
[`pricing-reference.md`](../skill/pricing-reference.md).

**4. Value, route and verdict.** It estimates the time saved, checks whether a
Microsoft 365 Copilot route (Researcher, Analyst, the Word / Excel / PowerPoint
agents, scheduled prompts, Copilot Chat) produces the same outcome without
Cowork credits, and picks a verdict. See
[`value-and-routing.md`](../skill/value-and-routing.md).

**5. Show one card.** One compact visual card, rendered with the template in
[`card-template.md`](../skill/card-template.md). In lite mode
(`/precost lite`) it replies with a 7-line text summary instead.

**6. Ask how to proceed.** One question with up to four options: Proceed in
Cowork · Cowork — sustainable · Use M365 Copilot instead · Rescope first (only
when the verdict is ⚠️). When the sustainable option is offered it can also ask
for an optional credit budget.

**7. Act on your choice.** Proceed and sustainable wait for you to send
**go** — the skill never changes the model itself. The M365 Copilot choice
gives you numbered steps with copy-paste prompts and stops. Rescope offers a
tighter rewrite of your prompt and a re-check.

## Lookup table — band × model tier (per run)

From [`pricing-reference.md` §9](../skill/pricing-reference.md). Model tier
multipliers are this community skill's directional assumption — Microsoft does
not publish per-model Cowork rates.

| Class | Efficient ×0.6 | Baseline ×1.0 | Premium ×2.0 |
|---|---|---|---|
| Light | 60–180 · ≈ $0.60–1.80 | 100–300 · ≈ $1–3 | 200–600 · ≈ $2–6 |
| Medium | 180–420 · ≈ $1.80–4.20 | 300–700 · ≈ $3–7 | 600–1,400 · ≈ $6–14 |
| Heavy | 420–900 · ≈ $4.20–9 | 700–1,500 · ≈ $7–15 | 1,400–3,000 · ≈ $14–30 |

- **Auto** shows Efficient-low to Baseline-high for the class (e.g. Medium on
  Auto ≈ 180–700).
- **Share of monthly limit** = upper end ÷ 2,000 credits (the default
  `MONTHLY_LIMIT`; change it in §0 of the pricing reference).

## Verdict rules (checked in this order)

From [`value-and-routing.md` §2](../skill/value-and-routing.md).

1. **💡 Use M365 Copilot instead** — a Microsoft 365 Copilot route produces the
   same outcome: no chained actions across apps, at most 2–3 deliverables a
   recipe covers, no partner-system plugins, no browser or app building, and any
   recurrence is a mail / calendar / Teams digest that scheduled prompts can
   handle.
2. **⚠️ Rescope first** — a one-off's upper estimate is more than 50% of the
   monthly limit, an automation's monthly projection exceeds it, the task is
   Heavy on a Premium model without a clear need, or the outcome is still vague.
3. **🌱 Cowork, run it lean** — Cowork is the right route and a lean lever cuts
   the upper end by 30% or more.
4. **✅ Cowork as written** — Cowork is the right route and it is already
   efficient.

## Source files

- [`skill/SKILL.md`](../skill/SKILL.md) — the workflow and guardrails
- [`skill/pricing-reference.md`](../skill/pricing-reference.md) — settings, billing facts, bands, tiers, effort, lookup tables, sources
- [`skill/value-and-routing.md`](../skill/value-and-routing.md) — time saved, verdict rules, routing, recipes
- [`skill/card-template.md`](../skill/card-template.md) — the card and the lite-mode summary

[← Back to the README](../README.md)
