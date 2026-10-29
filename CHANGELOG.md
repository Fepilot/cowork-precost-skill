# Changelog

All versions of **Pre-cost**, an unofficial, community-built Copilot Cowork skill.
Not an official Microsoft skill.

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
