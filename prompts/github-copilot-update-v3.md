# Prompt for GitHub Copilot — publish Pre-cost v3

> How to use: upload the contents of `cowork-precost-skill-v3-github-bundle.zip`
> to the repository root (they land in `skill-v3-incoming/`), open GitHub Copilot
> (Copilot Chat in the repo, or a Copilot coding agent / "Assign to Copilot"
> issue) and paste everything below the line.

---

You are updating the public repository **Fepilot/cowork-precost-skill** to
**v3** of *Pre-cost*, an **unofficial, community-built** Copilot Cowork skill
that estimates a task's credit cost and value before it runs, and recommends
the cheapest good route (Cowork, Cowork lean, or Microsoft 365 Copilot).

Work on a new branch `release/v3` and open a pull request. Do not push to `main`.

## Hard rules

1. **Never present this as a Microsoft product.** Every public page must say,
   near the top: *"Pre-cost is not an official Microsoft skill or feature. It
   is a community example — use it as inspiration and adapt it to your own
   business needs."*
2. **Do not edit the skill files' content** in `skill-v3-incoming/skill/`
   (`SKILL.md`, `pricing-reference.md`, `value-and-routing.md`,
   `card-template.md`). Move them, don't rewrite them. In particular, keep the
   `SKILL.md` frontmatter description under 1,024 characters — Cowork ignores
   skills above that.
3. **Do not invent prices, model names, multipliers or features.** Quote
   numbers only from the skill files, `CHANGELOG.md` or the official links
   listed below.
4. No confidential data, internal links, tenant names or private screenshots.
5. Every image gets meaningful `alt` text. Check every link.

## 1. Restructure the repository

Target layout:

```
README.md                      (rewritten — see §2)
CHANGELOG.md                   (from skill-v3-incoming/)
LICENSE                        (keep MIT, unchanged)
precost-skill-v3.zip           (from skill-v3-incoming/ — the file users upload to Cowork)
skill/                         (v3 files from skill-v3-incoming/skill/)
  SKILL.md
  pricing-reference.md
  value-and-routing.md
  card-template.md
docs/
  UPGRADE-IDEAS.md             (from skill-v3-incoming/docs/)
  screenshots.md               (update to list the new images)
  how-it-works.md              (new — see §3)
screenshots/
  precost-v3-card-heavy-deck.png        (new)
  precost-v3-check-cost-56-credits.png  (new)
  …existing screenshots stay, used only in archive docs if no longer accurate
prompts/
  github-copilot-update-v3.md  (this file)
archive/
  v1/                          (unchanged)
  v2/                          (move the current skill/ files and precost-skill-v2.zip here)
```

Steps:
- `git mv skill archive/v2/skill` and `git mv precost-skill-v2.zip archive/v2/`
  **before** moving the v3 files in. Add `archive/v2/README.md`: "v2 (mid-2026),
  kept for reference. Use v3 at the repository root."
- Move everything from `skill-v3-incoming/` to its target path, then delete
  `skill-v3-incoming/`.
- Note: v2 used `skill/precost.md`; v3 uses `skill/SKILL.md` (the file name
  Cowork expects inside a skill folder). Update every link that pointed at
  `skill/precost.md`.

## 2. Rewrite README.md (easy to scan, visual, public-friendly)

Keep the existing animated screenshot carousel at the top if it still works,
but make the **first static image** `screenshots/precost-v3-card-heavy-deck.png`.
If the carousel only shows v2 screenshots, replace its frames with the v3 image
or remove it.

Use this structure:

1. **Title + one-liner** — "Pre-cost — know what a Cowork task will cost
   *before* you run it." Badges (shields.io, static): `version v3`,
   `license MIT`, `status: community / unofficial`.
2. **Disclaimer callout** (GitHub `> [!IMPORTANT]`): the rule-1 sentence, plus
   "All outputs are estimates, not bills. The real cost depends on the prompt,
   context, documents, tools, model, reasoning effort and runtime — check it
   afterwards with Cowork's free `/cost` command."
3. **What you get** — the v3 card screenshot with a 5-bullet legend: verdict,
   class badge, credits/≈USD/time-saved tiles, comparison chart (as written vs.
   lean vs. Microsoft 365 Copilot), recommended model + effort and source link.
4. **How it works** — a Mermaid flowchart:
   ```mermaid
   flowchart LR
     A[Write your task + /precost] --> B{Outcome clear?}
     B -- no --> C[Up to 3 quick questions]
     B -- yes --> D[Estimate from official bands]
     C --> D
     D --> E[Visual card + verdict + source link]
     E --> F{Your choice}
     F --> G[Proceed in Cowork<br/>recommended model & effort]
     F --> H[Cowork sustainable<br/>lean plan + minimum credits]
     F --> I[Use Microsoft 365 Copilot<br/>step-by-step flow, no Cowork credits]
   ```
   Then one sentence: the skill never starts your task until you choose.
5. **The check itself costs a little** — `> [!NOTE]` callout with
   `screenshots/precost-v3-check-cost-56-credits.png`: "In our test, a full
   pre-check (questions + card) used **56 credits (≈ $0.56)** — about 4–8% of
   the 700–1,500-credit task it evaluated. Your number will vary with model,
   effort and questions asked. Use `/precost lite` for a text-only summary."
6. **Install in 2 minutes**
   1. Download `precost-skill-v3.zip`.
   2. In Cowork: **Customize → Skills → Add → Upload skill** → select the zip
      (or attach it in a new Cowork chat and ask "Install this as my skill
      named precost").
   3. Start a new chat, write a task and add `/precost`.
   Troubleshooting: "Skill not in the `/` list?" → open a new chat or reopen
   Cowork; if you edited the description, keep it under 1,024 characters.
7. **What's new in v3** — 6–8 bullets summarised from `CHANGELOG.md`.
8. **Where the numbers come from** — a small table: Light 100–300 · Medium
   300–700 · Heavy > 700 credits (Copilot Credits Guide); $0.01 per credit
   pay-as-you-go; model tiers are *directional assumptions* of this community
   skill (Microsoft does not publish per-model Cowork rates); the time-saved
   values are planning estimates. Link the official sources below.
9. **Make it yours** — 3–4 sentences + link to `docs/UPGRADE-IDEAS.md`. Show
   two teaser examples: (a) process-discovery questions for automations;
   (b) ROI questions that can flip the verdict to Cowork when the time saved
   outweighs the credits (include the €150/month worked example from the
   upgrade guide).
10. **Limitations** — estimates are directional; the agent decides at runtime;
    model availability depends on the tenant; the budget is a target, not a
    cap (only admin spending limits cap spend); no CO₂ figures.
11. **Contributing** — issues and PRs welcome; never include confidential data
    or private screenshots.
12. **License** — MIT.

Tone: plain English, short sentences, scannable, emoji only in headings or
callouts (max one per heading). Target ≤ 250 lines.

## 3. Add docs/how-it-works.md

Explain the 7 steps from `skill/SKILL.md` in plain language (1 short paragraph
each), the lookup table (class × model tier) from `skill/pricing-reference.md`
§9 as a Markdown table, and the verdict rules from `skill/value-and-routing.md`
§2. Link back to the source files.

## 4. Update docs/screenshots.md

List each image with a one-line caption and its alt text. Remove references
to images that no longer exist.

## 5. Repository metadata (suggest in the PR description — I'll set it manually)

- Description: "Pre-cost v3 — an unofficial Copilot Cowork skill that estimates
  a task's credits, cost and value before you run it, and suggests a leaner or
  no-credit route."
- Topics: `copilot-cowork`, `microsoft-365-copilot`, `copilot-credits`,
  `agent-skills`, `finops`, `prompt-engineering`.
- Create a GitHub Release `v3.0.0` with `precost-skill-v3.zip` attached and
  the v3 section of `CHANGELOG.md` as notes.

## 6. Check before opening the PR

- [ ] Disclaimer appears in README (top), `docs/UPGRADE-IDEAS.md` and `docs/how-it-works.md`.
- [ ] All relative links and image paths resolve on GitHub.
- [ ] Mermaid diagram renders in the GitHub preview.
- [ ] Skill files are byte-identical to the incoming ones (`git diff --stat` shows only moves).
- [ ] `precost-skill-v3.zip` contains `precost/SKILL.md` + 3 companion files.
- [ ] No old v2 numbers left in README (e.g. "Strongly positive", Opus 4.8 as default).

## Official sources to link

- Copilot Credits Guide — https://www.microsoft.com/licensing/guidance/CopilotCreditsGuide
- Usage-based billing & cost management — https://learn.microsoft.com/en-us/microsoft-365/copilot/usage-based-billing-overview-copilot-credits
- Everyday vs. advanced AI (USL vs. UBB) — https://learn.microsoft.com/en-us/microsoft-365/copilot/user-subscription-license-usage-based-billing
- `/cost` command — https://learn.microsoft.com/en-us/microsoft-365/copilot/usage-based-billing-copilot-credits-cost
- Choose a model for Cowork — https://learn.microsoft.com/en-us/microsoft-365/copilot/cowork/cowork-models
- What's new in Cowork — https://learn.microsoft.com/en-us/microsoft-365/copilot/cowork/whats-new
- Microsoft 365 Copilot plans & pricing — https://www.microsoft.com/en-us/microsoft-365-copilot/pricing
