# How Pre-cost works

> [!IMPORTANT]
> Pre-cost is not an official Microsoft skill or feature. It is a community
> example — use it as inspiration and adapt it to your own business needs.
> All outputs are estimates, not bills.

Pre-cost runs in 7 steps. The source of truth is [`../skill/SKILL.md`](../skill/SKILL.md);
every number comes from [`../skill/pricing-reference.md`](../skill/pricing-reference.md)
and [`../skill/value-and-routing.md`](../skill/value-and-routing.md).

## The 7 steps

**1. Read the prompt.** Pre-cost reads the task you wrote with `/precost`. It
looks for the outcome (what deliverables, how polished), actions (send,
schedule, post), sources and time window, attachments (names, types and sizes
only), recurrence, and the model and effort if the session shows them. It does
no lookups. If there is no task, it asks you to paste one.

**2. Clarify only if needed.** If something unknown would change the answer, it
asks up to 3 quick questions in one go: what the result should be, how much
material to use, and whether it runs once or repeats. If your prompt already
answers them, this step is skipped.

**3. Estimate.** It picks Light, Medium or Heavy from Microsoft's official bands,
moves it at most one class for a single heavy driver (a heavy input, an
expensive tool, many sources), maps your model to a tier and reads the range from
the lookup table below. Effort sets where it sits in the range. Automations get
a per-run and a per-month number. It also works out a lean option and its
minimum, and the share of your monthly limit.

**4. Value, route and verdict.** Time saved is the sum of typical minutes for the
kinds of work the task touches, valued at your hourly rate (default €75/h). It
checks whether Microsoft 365 Copilot (Researcher, Analyst, the Word, PowerPoint
or Excel agents, and so on) can produce the same outcome without Cowork credits.
Then it picks a verdict.

**5. Show the card.** One visual card with the verdict, class, credits, ≈ USD,
time saved, a comparison chart, the recommended model and effort, the cost
drivers, lean tips and a source link. `/precost lite` replaces the card with a
7-line text summary.

**6. Ask how to proceed.** One question: proceed in Cowork, run it lean (with an
optional credit budget), use Microsoft 365 Copilot instead, or rescope first
(only when the verdict is ⚠️).

**7. Act on your choice.** Cowork runs only after you send **go**. The lean route
lists the adjustments first. The Microsoft 365 Copilot route gives numbered steps
with copy-paste prompts and does not run anything in Cowork. Rescope offers a
tighter rewrite of your prompt. Pre-cost never changes your model; you pick it in
the Cowork picker.

## Lookup table — class × model tier (credits per run)

From [`pricing-reference.md`](../skill/pricing-reference.md) §9. Tiers are a
**directional assumption** of this community skill; Microsoft does not publish
per-model Cowork rates.

| Class | Efficient ×0.6 | Baseline ×1.0 | Premium ×2.0 |
|---|---|---|---|
| Light | 60–180 · ≈ $0.60–1.80 | 100–300 · ≈ $1–3 | 200–600 · ≈ $2–6 |
| Medium | 180–420 · ≈ $1.80–4.20 | 300–700 · ≈ $3–7 | 600–1,400 · ≈ $6–14 |
| Heavy | 420–900 · ≈ $4.20–9 | 700–1,500 · ≈ $7–15 | 1,400–3,000 · ≈ $14–30 |

**Auto** shows Efficient-low to Baseline-high for the class (for example, Medium
on Auto ≈ 180–700). The share of the monthly limit is the upper end ÷ 2,000 (an
assumed limit; `/cost` shows yours).

## Verdict rules

From [`value-and-routing.md`](../skill/value-and-routing.md) §2, checked in this
order:

1. **💡 Use M365 Copilot instead** — a Microsoft 365 Copilot route produces the
   same outcome: no chained actions across apps, at most 2–3 deliverables a
   recipe covers, no partner-system plugins, no browser or app building, and any
   recurrence is a mail, calendar or Teams digest that scheduled prompts can
   handle. Trade-off: a few manual hand-offs between apps.
2. **⚠️ Rescope first** — the upper estimate of a one-off is more than 50% of the
   monthly limit, an automation's monthly projection exceeds it, the task is
   Heavy on a Premium model without a clear need, or the outcome is still vague.
3. **🌱 Cowork, run it lean** — Cowork is the right route and a lean lever cuts
   the upper end by 30% or more (for example, Baseline → Efficient = −40%).
4. **✅ Cowork as written** — Cowork is the right route and it is already
   efficient.

Cowork is the right route when the task needs multi-step work chained across
apps, several deliverables with one consistent design, actions, partner plugins,
browser tasks, app building, or long-running or event-driven automation.
