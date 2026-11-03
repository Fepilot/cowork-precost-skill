# Changelog

> Pre-cost is not an official Microsoft skill or feature. It is a community
> example — use it as inspiration and adapt it to your own business needs.

## v3.0.0 — 2026-10-29

Download: [`precost-skill-v3.zip`](precost-skill-v3.zip?raw=1) ·
Update an installed copy: [`prompts/cowork-update-to-v3.md`](prompts/cowork-update-to-v3.md)

### Added
- **Clarifying questions** — up to 3 (outcome, scope, frequency), asked only
  when the answer would move the class, change the route or multiply the cost.
- **Model tiers** — Efficient ×0.6, Baseline ×1.0 (Opus-class), Premium ×2.0
  and Auto, with a band × tier lookup table (`pricing-reference.md` §4, §9).
- **Reasoning effort** — places the estimate inside the band and is part of the
  recommendation (`pricing-reference.md` §5).
- **Automations** — scheduled and event-driven tasks are priced per run and per
  month (`pricing-reference.md` §8).
- **Cowork — sustainable** route — a lean band, a lean minimum and an optional
  credit budget, with check-ins before steps likely to push past it.
- **Microsoft 365 Copilot recipes** — step-by-step flows with copy-paste prompts
  for Researcher, Analyst, the Word / PowerPoint / Excel agents, Outlook, Teams,
  Notebooks and scheduled prompts (`value-and-routing.md` §4–§5).
- **Share of monthly limit** — against an editable `MONTHLY_LIMIT` (default
  2,000 credits, an assumption).
- **`/precost lite`** — a 7-line text summary instead of the card.
- **Editable settings** — hourly rate, currency, monthly limit and credit price
  in one table (`pricing-reference.md` §0).
- Card: comparison bar chart (as written · lean · M365 Copilot), source links
  and a note that the pre-check itself uses a few credits.

### Changed
- Main file renamed `skill/precost.md` → `skill/SKILL.md` (the name Cowork
  expects). Frontmatter `cowork:` → `metadata:`.
- Skill description shortened to 641 characters (Cowork ignores descriptions
  over 1,024).
- Verdicts are now ✅ Cowork as written · 🌱 Cowork, run it lean · 💡 Use M365
  Copilot instead · ⚠️ Rescope first. They replace "Strongly positive" and
  "Marginal".
- Unknown model → Baseline tier, labelled "assumed" (no fixed default model).
- Billing facts updated for everyday vs. advanced AI (since 25 Sep 2026), the
  four credit buckets, pre-purchase plans and `/cost`. Last verified 2026-10-29.
- Runs only when asked (`/precost`, "cost check", "estimate this task"…), not
  at the start of every new task.
- Stricter cost guardrails: no web, mail, calendar, file-content or SharePoint
  lookups, no subagents, one card and at most two question prompts.

### Repository
- v2 skill files and `precost-skill-v2.zip` moved to [`archive/v2/`](archive/v2/),
  with the v2-era docs and system prompt.
- New [`docs/how-it-works.md`](docs/how-it-works.md) and v3 screenshots.

## v2 — mid-2026

Corrected cost formula (one-level class bump plus model multiplier), corrected
seat-price note, Adaptive Card output. See [`archive/v2/`](archive/v2/).

## v1

First release. See [`archive/v1/`](archive/v1/).
