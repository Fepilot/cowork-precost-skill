# Cowork & Copilot Pricing Reference

> Companion reference for the **precost** skill. Loaded on demand by `SKILL.md`
> when the pre-check needs cost mechanics (model multipliers, attachment weights,
> base credit bands, the adjustment formula). Reading this file is a **cheap local
> Read** — it is fully compatible with the skill's "fast, local-only" rule. Do
> **not** web-search for pricing at runtime; use this file.

**Sourcing & safety note.** Everything here is built from **public, customer-facing
Microsoft sources** (Microsoft Learn, the Microsoft 365 Copilot pricing page, and
Microsoft's GA announcement coverage) — see **Sources** at the bottom. It contains
**no internal, confidential, or pre-release Microsoft pricing**. Two kinds of
content are clearly separated:

- **OFFICIAL** — published by Microsoft. Safe to state to a customer as fact.
- **PLANNING ESTIMATE** — directional figures this pre-check uses to produce a
  *band* (never a bill). Not an official price list. Always presented as "≈" and
  paired with the disclaimer.

The authoritative, real numbers are always the **Copilot Credit Guide** and the
**Cost Management dashboard** (`/cost`) — point the user there for exact figures.

---

## 1. The products and what they cost (seat pricing) — OFFICIAL

| Product | What it is | Seat cost |
|---------|-----------|-----------|
| **Microsoft 365 Copilot Chat** | Web-grounded AI chat, included with eligible Microsoft 365 plans. Custom/agent usage is metered. | **Included — no additional cost** |
| **Microsoft 365 Copilot** (per-seat add-on) | Adds Work IQ, Copilot in Teams & the M365 apps, prebuilt agents (Researcher, Analyst, Facilitator), and **access to Cowork**. | **Paid per-seat add-on** — enterprise list price around **$30 user/month**; SMB and other segments differ, and promotions change, so confirm current pricing on the official Microsoft 365 Copilot pricing page. |
| **Copilot Cowork** | The agentic system (this product). Runs long, multi-step tasks across M365. | **No separate seat fee — requires the Microsoft 365 Copilot license, and *all Cowork usage is metered* via Copilot Credits** (see §2). |

**Key rule:** A Microsoft 365 Copilot license is the *entry ticket* to Cowork; the
actual Cowork work is billed **on top**, by usage, in Copilot Credits.

---

## 2. How Cowork is billed — OFFICIAL

- **Currency:** **Copilot Credits** — the common usage-based-billing currency
  across eligible Microsoft AI services (Cowork, Work IQ API, Copilot Studio
  agents, SharePoint agents, Copilot Chat agents).
- **What drives a task's cost — the four factors:** the **AI model used**, the
  **amount of context retrieved**, the **tools called**, and the **runtime
  (compute time)**. (This pre-check adds a fifth practical signal — **attachment
  weight** — because attachments are a big part of "context retrieved.")
- **Credits measure** the time and effort the agent needs to retrieve
  information, respond, and use tools — so **more complex tasks cost more
  credits**.
- **How customers buy credits (three routes):**
  - **Pay-as-you-go** — billed monthly through an Azure subscription for the
    actual credits used; no upfront commitment.
  - **Copilot Credit Pre-Purchase Plan (P3) / Commit Units (CCCUs)** — a one-year
    prepaid pool, **discounted** vs. pay-as-you-go, usable across eligible
    products.
  - **Prepaid capacity packs** — fixed packs of **25,000 Copilot Credits per
    month per pack**.
- **No rollover:** purchased monthly capacity is enforced monthly; **unused
  credits do not carry over**.
- **Spend control (admin):** budgets and spending limits at **tenant, group, or
  user** level, automated **alerts**, and **hard caps** — all in the **Microsoft
  365 admin center → Cost Management dashboard**. This pre-check is **advisory
  only**; it does not enforce spend.
- **Forecasting:** Microsoft provides a **Customer Cowork Estimator** to model
  expected credit usage before committing.
- **Transition:** Cowork left preview (GA **June 17, 2026**); preview usage began
  billing **July 1, 2026**.

---

## 3. Credit → dollar conversion — PLANNING ESTIMATE

This pre-check converts credits to dollars with a single, transparent planning
rate so the card can show a $ band:

```
1 Copilot Credit ≈ $0.01   (planning rate for the estimate only)
```

- This is the **pay-as-you-go reference rate** this skill uses; **prepaid packs /
  P3 are cheaper per credit** (volume discount), so a customer on prepaid is at
  the **low end or below** any band shown.
- Credits are **USD-denominated**. If the user's value is in another currency
  (e.g. €), **do not invent an FX rate** — show cost (USD) and value side by side
  and give the verdict qualitatively.
- The **authoritative** per-meter rate is in the **Copilot Credit Guide** and the
  **Cost Management dashboard** — always defer to those for a real number.

---

## 4. Model cost multipliers — PLANNING ESTIMATE

Cowork is **multi-model**: the user picks a model by quality/speed/cost trade-off.
Officially confirmed Cowork models today: **Claude Opus 4.8** (deep reasoning,
the Cowork default), **Claude Sonnet 4.6** (balanced), and **Cowork 1** (a new
efficiency-optimized model). Other models may appear in the picker over time.

**Officially listed Cowork models (Microsoft Learn, "Choose a model for Copilot
Cowork", updated 2026-09-14):** Auto (default) · **GPT 5.5** (Frontier, medium
effort) · **GPT 5.6 Sol** (hard work) · **GPT 5.6 Terra** (balanced, common tasks) ·
**GPT 6 Astra** (latest, tough problems) · **Claude Opus 5** (complex, high-stakes) ·
**Claude Sonnet 5** (everyday, fast) · **Claude Fable 5.1** (most advanced, ambitious
work).

Changes since the last refresh (Learn "What's new in Copilot Cowork"):
- **Sonnet 5 replaced Sonnet 4.6** at GA (June 2026).
- **Fable 5.1 replaced Fable 5** (Sept 2026); **GPT 6 Astra** added (Sept 2026).
- **Opus 4.8** shipped at GA but is **no longer in the current model list** (Opus 5
  is). It stays the **cost baseline** here because §6 bands are anchored to it, and
  Opus 5 has the same per-token price.
- **Cowork 1** (cost-optimized model) was announced as "upcoming / rolling out" but
  is **not in the official model list yet** — treat as unconfirmed.
- The **Sonnet + Opus advisor** mode and **Haiku** are **not in the current list**.
- **New cost lever — reasoning effort:** Light / Medium (default) / High / Extra
  High / Max. Microsoft states higher effort "is slower and uses more credits."

The multipliers below are a **directional planning device for this pre-check**,
derived from each model's **public per-token list price** (GitHub Copilot model
pricing, input/output per 1M tokens) relative to Opus 4.8 ($5 / $25). They are
**not an official Microsoft per-model Cowork price list** — Cowork credits also
depend on context, tools, runtime and orchestration. Multipliers are expressed
**relative to Opus 4.8 = 1.0×**.

| Model | Tier | Public token price (in / out per 1M) | Credit multiplier (vs Opus 4.8) | Use it for |
|-------|------|--------------------------------------|---------------------------------|------------|
| **Auto** | Router | varies | **~0.7×** (observed) | Default; skews to cheaper models for routine work |
| **Claude Sonnet 5** | Efficient | $2 / $10 | **~0.4×** | Everyday drafting, lookups, summaries (cheapest listed) |
| **GPT 5.6 Terra** | Balanced | $2 / $12 | **~0.4–0.5×** | Common tasks, balanced effort |
| **GPT 5.6 Sol** | Powerful | $4 / $20 | **~0.8×** | Hard work, efficient for its class |
| **Claude Opus 4.8** | Deep reasoning | $5 / $25 | **1.0× (baseline)** | Baseline for §6 bands |
| **Claude Opus 5** | Deep reasoning | $5 / $25 | **~1.0×** | Complex, high-stakes work |
| **GPT 5.5** (Frontier) | Powerful | $5 / $30 | **~1.0–1.2×** list; **up to ~4× observed** | Medium-effort work; avoid for deck building (see note) |
| **Claude Fable 5.1** | Premium | $10 / $50 | **~2.0×** | Most ambitious work only; admin-enabled, data retention applies |
| **GPT 6 Astra** | Premium | $10 / $50 | **~2.0×** | Toughest problems only |
| **Cowork 1** *(unconfirmed)* | Efficiency | n/a | **~0.2× (assumption)** | Only if it appears in the picker |

**Field evidence (independent, same prompt — a PowerPoint deck):** Opus 4.8 ≈ 326
credits, Auto ≈ 228 credits (~0.7×), GPT 5.5 ≈ 1,291 credits (~4× — long runtime),
Sonnet 5 lowest of all (reported as probably under-metered). Runtime and tool loops
can outweigh token price, so treat list-price ratios as a floor for slow models.

**Reasoning effort adjustment (assumption, no official ratio):** Light ≈ −20–30%,
Medium = as above, High / Extra High ≈ +25–50%, Max ≈ up to 2×. State it on the
card as an assumption.

> If the active model can't be determined, assume **Auto ≈ 0.7×** for routine tasks
> or **Opus-class 1.0×** for deep-reasoning tasks, and say so on the card.

---

## 5. Attachment weight — PLANNING ESTIMATE

Attachments are a major part of "context retrieved." **Format drives token/credit
weight far more than file size** — the same content as clean Markdown is cheapest;
PDFs, slides, and images cost multiples more. Weights are relative to `.md = 1×`.

Use these weights to decide **whether an input is heavy enough to bump the task up one
class** in §7 (rule of thumb: **≥ ~2× is a heavy input** — `.pptx`, scanned/image PDFs,
several images). They are a **guide for the class bump, not a literal multiplier** on
the base band (see §7 for why).

| Attachment | Relative token/credit weight | Note |
|------------|------------------------------|------|
| `.md` / `.txt` / `.csv` | **1× (lightest)** | Near the token floor; structure parses natively |
| `.docx` | ~1.2× | Unchanged (no new public data) |
| `.xlsx` (data) | ~1.3× | Unchanged (no new public data) |
| `.html` | ~1.7× | Raw HTML carries markup noise |
| `.pdf` — born-digital, clean text | **~1.1×** | Clean extraction is roughly a wash vs `.md` |
| `.pdf` — text, noisy layout (headers/footers, multi-column) | **~2–3×** | Extraction noise; up to ~70% savings when converted |
| `.pdf` — read as page images | **~3–5×+** | Some pipelines bill page image **and** extracted text |
| `.pptx` | ~3–4× | Slides parsed as text + visuals (no new public data) |
| images (`.png` / `.jpg`) | **≈1,000–1,400 tokens per ~1024×1024 image**; large photos ≈2,500–6,600 | Several images → Heavy |
| scanned / photographed PDF | **~5×** (heaviest) | ~765 tokens/page as pixels; 10-page scan ≈7,600 vs ≈1,500 as text |

*Rule of thumb (revised):* the old "PDF = 48–70%+ more tokens" figure only holds for
**noisy extraction or page-image paths**. A clean, born-digital PDF is close to `.md`
(~5% difference in one measurement), so converting it is about **structure and
accuracy**, not tokens. The big savings are on **scanned / image-heavy files and
multi-image inputs** — converting those to `.md` first remains the single biggest
sustainability lever.

---

## 6. Base task bands (Light / Medium / Heavy) — PLANNING ESTIMATE

Set the **base** credit band from the task's sources, reasoning depth, and
deliverables. Cost then scales with the model, context, tools, and runtime.

| Class | Sources / context | Reasoning | Deliverables | Base credits | Base cost (USD) |
|-------|-------------------|-----------|--------------|--------------|-----------------|
| **Light** | A few knowledge sources | Light (e.g. a summary) | 1 or fewer | **100–300** | **$1–3** |
| **Medium** | Many sources, varying timeframes | Structured | 2+ | **300–700** | **$3–7** |
| **Heavy** | Broad aggregation, long timeframes | Deep | Many | **700+** | **$7+** |

Pick the class by the **heaviest signal present**:
- *Light* — one short summary from one email.
- *Medium* — "pull emails + calendar + files into a briefing doc, an Excel
  overview, and a client-ready deck."
- *Heavy* — "analyze 6 months of data, classify it, and produce a leadership
  report vs. the prior period."

---

## 7. Putting it together — the adjustment formula — PLANNING ESTIMATE

```
adjusted_credits ≈ base_band(effective_class) × model_multiplier
adjusted_cost_usd ≈ adjusted_credits × $0.01
```

Only **two** things scale the base band, so the estimate stays reproducible and the
**badge always matches the number**:

1. **effective_class** — start from the Step 2 class, then move it **at most one
   level**:
   - **Up one level** (Light→Medium, Medium→Heavy) if a **heavy input** is attached
     (`.pptx`, scanned/photographed PDF, or several images — see §5) **or** the task
     needs an **expensive tool** (`ImageGenerate`, `deep-research`, browser
     automation, subagents). Move by the single heaviest driver — don't stack bumps.
     Heavy is open-ended, so if you're already Heavy, stay Heavy and read the upper end.
   - **Down one level** if it's a single trivial read on a light input
     (`.md` / `.txt` / `.csv`) with no extra tools.
   - Otherwise keep the Step 2 class.
2. **model_multiplier** (§4) — the base bands are anchored to **Opus 4.8 = 1.0×**, so
   Opus is a no-op; e.g. **Sonnet 0.6×** turns a 300–700 band into ≈ 180–420 credits,
   and a 2.0× premium model pushes it up.

- **Why not multiply by attachment weight and a context/tool factor directly?** The
  class already prices context, runtime, tools and deliverables (Step 2). Multiplying
  the whole base *again* by a 2–4× attachment weight would (a) double-count those
  signals and (b) detach the number from the badge — a "Light" task could read
  350–1,050 credits. The **one-level class bump** captures "format and tools matter"
  without either problem. The §5 weight table now tells you **whether an input is heavy
  enough to bump the class** — it is no longer a literal multiplier on the base.
- Keep the result a **band**, never a single false-precise number. Round to clean
  ranges, e.g. **"≈ 200–450 credits · ≈ $2–4.50 (Sonnet 4.6)."**

---

## Sources (public, customer-facing)

- **Usage-based billing & cost management for Copilot Credits (covers Cowork)** —
  https://learn.microsoft.com/en-us/microsoft-365/copilot/usage-based-billing-overview-copilot-credits
- **Microsoft 365 Copilot plans & pricing** —
  https://www.microsoft.com/en-us/microsoft-365-copilot/pricing
- **Copilot Studio licensing & Copilot Credits** —
  https://learn.microsoft.com/en-us/microsoft-copilot-studio/billing-licensing
- **Prepaid capacity packs vs pay-as-you-go (25,000-credit packs)** —
  https://learn.microsoft.com/en-us/microsoft-365/copilot/pay-as-you-go/copilot-capacity-packs
- **Copilot Cowork GA — cost model, budgeting & model choice** (press coverage of
  Microsoft's announcement) —
  https://www.heise.de/en/news/From-Chat-to-Agent-Copilot-Cowork-for-Microsoft-365-is-here-11335714.html
- **Choose a model for Copilot Cowork** (current model list, reasoning effort) —
  https://learn.microsoft.com/en-us/microsoft-365/copilot/cowork/cowork-models
- **What's new in Copilot Cowork** (model replacements Jun–Sep 2026) —
  https://learn.microsoft.com/en-us/microsoft-365/copilot/cowork/whats-new
- **Public per-token model prices** (basis for §4 ratios) —
  https://docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing
- **Same prompt, different models — Cowork cost comparison** (field evidence) —
  https://futurework.blog/2026/07/01/same-prompt-different-models-cowork-model-outcome-and-cost-comparison/
- **Attachment token data** (§5) —
  https://markdownconverters.com/blog/pdf-vs-markdown-ai-tokens ·
  https://mdisbetter.com/blog/token-count-pdf-vs-markdown-real-comparison ·
  https://www.miinideck.com/blog/how-many-tokens-image-pdf-llm-2026
- Authoritative rates: **Copilot Credit Guide** + **Cost Management dashboard /
  `/cost`** (per-tenant, real billed figures).

*Last refreshed from sources: 2026-10-09 (§4–§5); other sections 2026-06-30. Re-verify against the pages above if
Microsoft updates pricing.*

*Last refreshed from sources: 2026-06-30. Re-verify against the pages above if
Microsoft updates pricing.*
