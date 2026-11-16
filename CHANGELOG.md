# Changelog

All versions of **Pre-cost**, an unofficial, community-built Copilot Cowork skill.
Not an official Microsoft skill.

## v3.1 — 2026-11-16

### Added
- **Spend size — no assumed limits.** Every card shows the spend size on an absolute scale anchored to Microsoft's task bands (Small ≤ 300 · Medium ≤ 700 · Large ≤ 1,500 · Very large > 1,500 credits). It never asks for your balance and never assumes a personal limit, because limits differ per person.
- **Credits left, only when known.** If a `/cost` result is already in the chat (or your org sets one known limit in `ORG_MONTHLY_LIMIT`), the card adds "% of what's left". A skill can't run `/cost`, and the per-user balance API in Microsoft Graph is beta and admin-only.
- **Caution levels** 🟢 normal · 🟡 careful · 🟠 big spend (from spend size) · 🔴 critical (only with a known balance), plus a ⛔ "Not enough credits" verdict with alternatives (lean, M365 Copilot route, split, wait for the reset, request credits).
- **Your time on each route.** Hands-on minutes for the M365 Copilot flow vs. reviewing a Cowork result, shown on the card.
- **"Cowork pays back" rule.** When the time saved is worth ≥ 3× the lean Cowork cost (≥ 5× when the caution level is 🟡 careful or 🟠 big spend), or the task needs brand-polished / matching deliverables, Cowork lean wins even if M365 Copilot could do it.
- Reset-date logic: credits don't carry over, so plenty left near the reset is a reason to use them.

### Fixed
- **No double counting** in the size class: a signal that sets the base class can't also bump it (e.g. web research + one deck = Medium, not Heavy).
- The M365 Copilot bar on the chart is labelled "0 Cowork credits" instead of looking empty.

## v3 — 2026-10-29

**Rebuilt for the October 2026 Copilot pricing model and the current Cowork model picker.**

### Added
- **Clarify-first flow.** The skill reviews the prompt and asks up to 3 quick questions (outcome, scope, frequency) only when the answer would change the estimate.
- **Visual card v3.** Verdict banner, Light/Medium/Heavy badge, three KPI tiles (credits, ≈ USD, time saved), a comparison bar chart (Cowork as written vs. Cowork lean vs. Microsoft 365 Copilot route), recommended model + reasoning effort, cost drivers, lean minimum, share of a monthly limit, and a clickable link to the official source.
- **Three-way decision.** Proceed in Cowork (with a recommended model and effort) · Cowork *sustainable* (lean plan, minimum credits and an optional credit budget) · use Microsoft 365 Copilot instead (step-by-step flow with Researcher, Analyst, Word / Excel / PowerPoint agents, Outlook, Teams, Notebooks, scheduled prompts).
- **Reasoning effort** (Light → Max) as a cost lever.
- **Automations.** Scheduled and event-driven Cowork tasks show cost per run and per month.
- **Lite mode.** `/precost lite` returns a 7-line text summary instead of a card, for the lowest possible check cost.
- **"Make it yours" settings block** (hourly rate, currency, monthly limit, credit price) in `pricing-reference.md` §0.
- **Community-skill notice** on every card.

### Changed
- **Opt-in only.** Runs when the user types `/precost` (or a trigger phrase), no longer at the start of every new task.
- **Never starts the task by itself.** It waits for the user's choice and a "go".
- **Model guidance** moved from fixed model names to tiers (Efficient / Baseline / Premium / Auto) mapped to today's picker; Auto is the safe default.
- **Bands** aligned to the Copilot Credits Guide (Light 100–300, Medium 300–700, Heavy > 700; Heavy read as 700–1,500 with a "may exceed" flag).
- **Billing facts** updated for the split between everyday AI (included in the license) and advanced AI (Copilot Credits).
- Main instruction file renamed to `SKILL.md` (the name Cowork expects inside a skill folder); frontmatter moved to the spec-valid `metadata:` block; description kept under 1,024 characters so the skill loads.

### Removed
- Retired models from the table (Cowork 1, Haiku 4.5, Opus 4.8 as default).
- Any CO₂ / energy claims — "sustainable" now means *same outcome, fewer credits*.

## v2 — mid-2026
Light / Medium / Heavy bands, model multipliers, attachment weights, one-level class bump, value estimate, sustainability levers. Archived under `archive/v2/`.

## v1
First public version. Archived under `archive/v1/`.
