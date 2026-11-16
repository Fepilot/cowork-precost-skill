# How Pre-cost works (v3.1)

> [!IMPORTANT]
> **Pre-cost is not an official Microsoft skill or feature.** It is a community
> example — use it as inspiration and adapt it to your own business needs. All
> numbers are planning estimates, not bills — check the real cost with Cowork's
> free `/cost` command after the task.

This page summarizes the logic in [`skill/SKILL.md`](../skill/SKILL.md). The
skill files are the source of truth; if this page and a skill file disagree,
the skill file wins.

## The 7 steps

**1. Read the prompt (no lookups).** Pre-cost reads only the task text and the
names, types and sizes of any attachments. It extracts the outcome
(deliverables and quality bar), actions (send, schedule, post, browse), context
sources, recurrence, and the current model and effort if the session shows
them. If a `/cost` result is already in the chat, it also notes your credits
left — otherwise your balance stays **unknown**. It never asks for your balance
and never assumes a personal limit.

**2. Clarify only if it changes the answer.** If something unknown would move
the class, change the route or multiply the cost, it asks up to 3 short
questions in one go: outcome, scope and frequency. If the prompt already
answers them, it skips this step.

**3. Estimate.** It picks Light, Medium or Heavy from Microsoft's official task
bands and applies at most one bump up or down — never for a signal that already
set the class (no double counting: web research + one deck = Medium, not Heavy).
It maps the model to a tier (Efficient, Baseline, Premium or Auto), places the
estimate inside the band by reasoning effort, gives automations a per-run and a
per-month figure, and works out a lean option and its minimum. Finally it rates
the **spend size** and the **caution level** (see below). All numbers come from
[`pricing-reference.md`](../skill/pricing-reference.md).

**4. Value, route and verdict.** It estimates the time saved, checks whether a
Microsoft 365 Copilot route (Researcher, Analyst, the Word / Excel / PowerPoint
agents, scheduled prompts, Copilot Chat) produces the same outcome without
Cowork credits, and compares **your hands-on time** on that route with
reviewing a Cowork result. Then it picks a verdict. See
[`value-and-routing.md`](../skill/value-and-routing.md).

**5. Show one card.** One compact visual card, rendered with the template in
[`card-template.md`](../skill/card-template.md). In lite mode
(`/precost lite`) it replies with a 7-line text summary instead.

**6. Ask how to proceed.** One question with up to four options: Proceed in
Cowork · Cowork — sustainable · Use M365 Copilot instead · Rescope first (only
when the verdict is ⚠️ or ⛔). When the sustainable option is offered it can
also ask for an optional credit budget.

**7. Act on your choice.** Proceed and sustainable wait for you to send **go**
— the skill never changes the model itself. The M365 Copilot choice gives you
numbered steps with copy-paste prompts and stops. Rescope offers a tighter
rewrite of your prompt and a re-check.

## Lookup table — band × model tier (per run)

From `pricing-reference.md` §9. Model tier multipliers are this community
skill's directional assumption — Microsoft does not publish per-model Cowork
rates.

| Class | Efficient ×0.6 | Baseline ×1.0 | Premium ×2.0 |
|---|---|---|---|
| Light | 60–180 · ≈ $0.60–1.80 | 100–300 · ≈ $1–3 | 200–600 · ≈ $2–6 |
| Medium | 180–420 · ≈ $1.80–4.20 | 300–700 · ≈ $3–7 | 600–1,400 · ≈ $6–14 |
| Heavy | 420–900 · ≈ $4.20–9 | 700–1,500 · ≈ $7–15 | 1,400–3,000 · ≈ $14–30 |

Auto shows Efficient-low to Baseline-high for the class (e.g. Medium on Auto
≈ 180–700).

## Spend size & caution level — no assumed limits

Credit limits differ per person and per spending policy, and a skill can't run
`/cost`. So every card rates the spend on a fixed scale anchored to
Microsoft's task bands (`pricing-reference.md` §11), using the upper end of the
estimate:

| Spend size | Upper end | ≈ USD |
|---|---|---|
| Small | ≤ 300 credits | ≤ $3 |
| Medium | 301–700 | ≤ $7 |
| Large | 701–1,500 | ≤ $15 |
| Very large | > 1,500 | > $15 (above Microsoft's own "heavy" example) |

**Credits left are used only when known** — from a `/cost` result already in
the chat, or from `ORG_MONTHLY_LIMIT` if your organization sets one known limit
in `pricing-reference.md` §0. Tip: type `/cost` (free) before `/precost` to add
a budget check.

| Caution level | Balance known: share of what's left | Balance unknown: spend size | Effect |
|---|---|---|---|
| 🟢 Normal | ≤ 25% | Small / Medium | Normal rules. Plenty left near the reset date? Use it — credits don't carry over. |
| 🟡 Careful | 25–60% | Large | Prefer the lean plan; prefer M365 Copilot unless Cowork clearly pays back (≥ 5×). |
| 🟠 Big spend | — | Very large | ⚠️ "Big spend — run lean or split", plus the `/cost` tip. |
| 🔴 Critical | > 60%, or more than is left | — | ⛔ Not enough credits — lean only if it fits, else M365 Copilot, split, wait for the reset or request credits. |

## Verdict rules (first match wins)

From `value-and-routing.md` §2.

0. **⛔ Not enough credits** — caution 🔴 (only possible when your balance is known).
1. **Cowork-only work** → ✅ or 🌱. Cowork is the right route when the task
   needs multi-step work chained across apps, several deliverables with one
   consistent design, actions (send, schedule, post, update records), partner
   plugins, browser tasks, app building, or long-running / event-driven
   automation.
2. **Microsoft 365 Copilot can do it** → decide on *total* cost, not credits alone:
   - **🌱 Cowork pays back** when the value of your time saved is ≥ 3× the lean
     Cowork cost (🟢) or ≥ 5× (🟡 / 🟠), or when a quality need applies (brand
     template, exec-ready polish, generated visuals, several matching
     artifacts) and caution is 🟢.
   - Otherwise **💡 Use M365 Copilot instead**, with the trade-off stated
     ("≈ N min more of your time, 0 Cowork credits").
3. **⚠️ Rescope first** — the outcome is still vague, a Heavy task is set to a
   Premium model without a clear need, or caution is 🟠 Big spend.
4. **🌱 Cowork, run it lean** — a lean lever cuts the upper end by ≥ 30%, or
   caution is 🟡; otherwise **✅ Cowork as written**.

**Worked example** — web research + a polished 10–12 slide deck: Medium; lean
Cowork ≈ 180–420 credits (≈ $1.80–4.20); balance unknown → spend size Medium →
🟢. The M365 route (Researcher → PowerPoint agent) takes ≈ 30–40 min of your
time vs ≈ 10 min to review a Cowork result → 20–30 min ≈ €25–38 ≥ 3 × $4.20 →
**🌱 Cowork pays back**. If a `/cost` result in the chat showed only ~500
credits left, lean 420 would be 84% of it → **⛔ → 💡 Researcher → PowerPoint
agent**.

## Source files

- [`skill/SKILL.md`](../skill/SKILL.md) — the workflow and guardrails
- [`skill/pricing-reference.md`](../skill/pricing-reference.md) — settings, billing facts, bands, tiers, effort, spend size, lookup tables, sources
- [`skill/value-and-routing.md`](../skill/value-and-routing.md) — time saved, your time per route, verdict rules, routing, recipes
- [`skill/card-template.md`](../skill/card-template.md) — the card and the lite-mode summary

[← Back to the README](../README.md)
