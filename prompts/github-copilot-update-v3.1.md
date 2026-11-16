# GitHub Copilot prompt — release Pre-cost v3.1

> Paste everything below the line into GitHub Copilot (CLI, VS Code agent mode
> or a Copilot coding-agent task) once the `precost-v3.1-update/` folder is in
> the repository root.

---

Update the public repository **Fepilot/cowork-precost-skill** from **v3** to
**v3.1** of *Pre-cost*, an **unofficial, community-built** Copilot Cowork skill
that estimates a task's credits, cost and value before it runs and recommends
the best route (Cowork, Cowork lean, or Microsoft 365 Copilot).

All new material is in **`precost-v3.1-update/`** at the repo root:

| File in `precost-v3.1-update/` | Goes to |
|---|---|
| `skill/SKILL.md`, `skill/pricing-reference.md`, `skill/value-and-routing.md`, `skill/card-template.md` | `skill/` (replace) |
| `precost-skill-v3.1.zip` | repo root |
| `CHANGELOG.md` | repo root (replace) |
| `docs/how-it-works.md` | `docs/how-it-works.md` (replace) |
| `GITHUB-COPILOT-PROMPT.md` | `prompts/github-copilot-update-v3.1.md` |
| `README-FIRST.md` | delete |

Work on branch **`release/v3.1`** and open a pull request titled
**"Release Pre-cost v3.1 — spend size, your-time comparison, no assumed limits"**.
Do not push to `main`.

## Hard rules

1. **Never present this as a Microsoft product.** Keep this notice near the top
   of README, `docs/how-it-works.md` and `docs/UPGRADE-IDEAS.md`: *"Pre-cost is
   not an official Microsoft skill or feature. It is a community example — use
   it as inspiration and adapt it to your own business needs."*
2. **Copy the skill files byte for byte.** Do not reword, reformat or re-wrap
   anything in `skill/`. The `SKILL.md` frontmatter description must stay under
   1,024 characters (it is 654) — Cowork ignores skills above that.
3. **Do not invent** prices, limits, model names, multipliers or features. Use
   only numbers from the skill files, `CHANGELOG.md` and the official links
   already in the README.
4. **Remove every trace of the old assumed limit.** v3.1 never assumes a
   personal credit limit. After your edits, a bare `MONTHLY_LIMIT` (the new
   optional setting `ORG_MONTHLY_LIMIT` is fine), "2,000 credits",
   "share of a monthly limit" and "÷ 2,000" must not appear outside
   `archive/` and the v3 section of `CHANGELOG.md`.
5. No confidential data, tenant names, internal links or private screenshots.

## 1. Move files

1. `git mv precost-skill-v3.zip archive/v3/precost-skill-v3.zip` and copy the
   current `skill/*.md` (v3) to `archive/v3/skill/` **before** replacing them.
   Add `archive/v3/README.md`: "Pre-cost v3 (Oct 2026), kept for reference.
   Use v3.1 at the repository root."
2. Move the v3.1 files as in the table above, then delete
   `precost-v3.1-update/`.
3. Check what is actually in `archive/` (v1 is there; v2 may not be). Make every
   README/doc sentence about archived versions match what really exists.

## 2. README.md — targeted edits (keep everything else)

- **Version badge / any "v3" label for the current release** → `v3.1`.
- **"What you get"** bullets:
  - Verdict line → `✅ Cowork as written · 🌱 Cowork, run it lean (incl. "Cowork pays back") · 💡 Use M365 Copilot instead · ⚠️ Rescope first (incl. "Big spend") · ⛔ Not enough credits (only when your balance is known)`.
  - Replace "the share of a monthly limit" with: **"spend size (Small · Medium · Large · Very large) — plus your share of credits left only if a `/cost` result is already in the chat"**.
  - Add: **"Your time — hands-on minutes on the Microsoft 365 Copilot route vs. reviewing a Cowork result."**
  - Under the screenshot add the caption: *"v3 card shown — v3.1 adds the spend-size and your-time rows."*
- **Mermaid diagram** — insert one node between the estimate and the card:
  ```
  D --> S[Spend size + caution level<br/>credits left only if /cost is in the chat]
  S --> E
  ```
  (remove the old direct `D --> E` edge). Confirm it renders in the preview.
- **New section** right after "The check itself costs a little", titled
  **"Spend size — no assumed limits"**:
  > Credit limits differ per person, and a skill can't run `/cost` or read your
  > balance. So Pre-cost never asks for it and never assumes one. Every card
  > rates the spend on a fixed scale anchored to Microsoft's task bands:
  >
  > | Spend size | Upper estimate | ≈ cost |
  > |---|---|---|
  > | Small | up to 300 credits | up to $3 |
  > | Medium | 301–700 | up to $7 |
  > | Large | 701–1,500 | up to $15 |
  > | Very large | over 1,500 | over $15 |
  >
  > **Tip:** type `/cost` (free) before `/precost` and the card also shows your
  > share of credits left — the same task is a different decision with 1,800
  > credits left than with 300. Organizations with one known limit can set
  > `ORG_MONTHLY_LIMIT` in `skill/pricing-reference.md` §0.
- **Install** → download link and filename `precost-skill-v3.1.zip`.
- **"What's new in v3"** → rename to **"What's new in v3.1"** with these bullets,
  then keep the old v3 bullets inside `<details><summary>v3 highlights</summary> … </details>`:
  - **Spend size, no assumed limits** — fixed Small / Medium / Large / Very large scale; credits left only when known.
  - **Caution levels** 🟢 normal · 🟡 careful · 🟠 big spend · 🔴 critical, and a ⛔ "Not enough credits" verdict.
  - **Your time on each route** — Microsoft 365 Copilot hands-on minutes vs. reviewing a Cowork result.
  - **"Cowork pays back"** — Cowork lean wins when your time saved is worth ≥ 3× its cost (≥ 5× when careful), or the deliverable needs brand polish.
  - **No double counting** — e.g. web research + one deck is Medium, not Heavy.
  - **Clearer chart** — the Microsoft 365 Copilot bar is labelled "0 Cowork credits".
- **"Where the numbers come from"** table — add three rows (type column in brackets):
  - Spend size · Small ≤ 300 · Medium ≤ 700 · Large ≤ 1,500 · Very large > 1,500 credits · *this skill's scale, anchored to the official bands*
  - Your time per route · e.g. Researcher ≈ 10 min, PowerPoint ≈ 10–15 min, each hand-off + 5 min · *planning estimate*
  - "Cowork pays back" margin · ≥ 3× (🟢) / ≥ 5× (🟡 🟠) the lean Cowork cost · *planning rule of this skill*
- **"Make it yours" → ROI teaser** — add one sentence: *"v3.1 already applies a
  basic version of this rule ("Cowork pays back"); tune the minutes and margins
  in `skill/value-and-routing.md` §1b–§2."*
- **Limitations** — add: *"Your credits left are unknown unless you typed
  `/cost` earlier in the chat — the skill never assumes a personal limit."*
- Fix the "Earlier versions are kept under `archive/` (…)" sentence to list the
  folders that really exist (now including v3).

## 3. docs/UPGRADE-IDEAS.md — two small edits

- **Idea 2** (ROI questions): add at the end — *"v3.1 already includes a basic
  version of this rule ('Cowork pays back'). Tune the hands-on minutes in
  `skill/value-and-routing.md` §1b and the 3× / 5× margins in §2 to your teams."*
- **Idea 3** (your own numbers): replace the bullet about the monthly credit
  limit with — *"**A known org-wide limit**: if everyone has the same monthly
  credit limit, set `ORG_MONTHLY_LIMIT` in `pricing-reference.md` §0. Leave it
  blank when limits differ — the skill then uses spend size and never assumes
  a limit."*

## 4. docs/screenshots.md

Keep the list accurate. Add a note that the current screenshots show the v3
card and that v3.1 adds the spend-size and your-time rows. Leave a commented
placeholder for `screenshots/precost-v3.1-card.png` (do not reference a file
that doesn't exist).

## 5. Release

Create GitHub Release **`v3.1.0`** from the merged commit, attach
`precost-skill-v3.1.zip`, and use the v3.1 section of `CHANGELOG.md` as the
release notes.

## 6. Checklist before opening the PR

- [ ] `skill/*.md` are byte-identical to `precost-v3.1-update/skill/*.md` (compare hashes).
- [ ] `precost-skill-v3.1.zip` contains `precost/SKILL.md` + the 3 companion files.
- [ ] No bare `MONTHLY_LIMIT` (`ORG_MONTHLY_LIMIT` is expected), "2,000 credits", "share of a monthly limit" or "÷ 2,000" outside `archive/` and the v3 changelog section.
- [ ] Disclaimer present in README, `docs/how-it-works.md`, `docs/UPGRADE-IDEAS.md`.
- [ ] All relative links, image paths and the download link resolve; Mermaid renders.
- [ ] `archive/v3/` holds the v3 zip and skill files; `precost-v3.1-update/` is deleted.
- [ ] PR description lists the changes in plain language.
