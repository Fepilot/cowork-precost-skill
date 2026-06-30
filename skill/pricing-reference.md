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
| **Microsoft 365 Copilot** (per-seat add-on) | Adds Work IQ, Copilot in Teams & the M365 apps, prebuilt agents (Researcher, Analyst, Facilitator), and **access to Cowork**. | **From $21 user/month, paid yearly** (promo **$18** Jul 1–Sep 30, 2026; annual commitment). Enterprise/market pricing can differ — confirm on the official pricing page. |
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

The multipliers below are a **directional planning device for this pre-check**
(anchored to each tier's relative compute cost — heavier reasoning models cost
more per token). They are **not an official Microsoft per-model price list**.
Multipliers are expressed **relative to the Cowork default, Opus 4.8 = 1.0×**.

| Model | Tier | Credit multiplier (vs Opus 4.8) | Use it for |
|-------|------|---------------------------------|------------|
| **Cowork 1** | Efficiency | **~0.2×** | Fast, simple, high-volume work (cheapest) |
| **Claude Haiku 4.5** | Efficiency | **~0.2×** | Quick summaries / extraction / simple drafts |
| **Claude Sonnet 4.6** | Balanced | **~0.6×** | The balanced default for most tasks |
| **GPT-5.X** | Balanced | **~0.6×** | ≈ Sonnet-tier general work |
| **Sonnet + Opus advisor** | Mixed | **~0.7–0.8×** | Sonnet does the work, Opus reviews |
| **Claude Opus 4.8** | Deep reasoning | **1.0× (baseline)** | Hard reasoning, long agentic runs (Cowork default) |
| **Top-tier reasoning model** | Premium | **~2.0×** | Reserve for the hardest work only |

> If the active model can't be determined, assume the **Cowork default (Opus 4.8,
> 1.0×)** and say so on the card.

---

## 5. Attachment weight — PLANNING ESTIMATE

Attachments are a major part of "context retrieved." **Format drives token/credit
weight far more than file size** — the same content as clean Markdown is cheapest;
PDFs, slides, and images cost multiples more. Weights are relative to `.md = 1×`.

| Attachment | Relative token/credit weight |
|------------|------------------------------|
| `.md` / `.txt` / `.csv` | **1× (lightest)** |
| `.docx` | ~1.2× |
| `.xlsx` (data) | ~1.3× |
| `.html` | ~1.7× |
| `.pdf` (text, no images) | ~2–3× |
| `.pptx` | ~3–4× (slides parsed as text + visuals) |
| images (`.png` / `.jpg`) | high — each image ≈ a block of vision tokens; many images → Heavy |
| scanned / photographed PDF | ~3–5× (heaviest) |

*Rule of thumb:* a text PDF carries roughly **48–70%+ more tokens** than the same
content in `.md`; scanned/image-heavy files are worse. Converting a heavy input to
`.md` first is the single biggest sustainability lever.

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
adjusted_credits ≈ base_credits × model_multiplier × attachment_weight × context/tool load
adjusted_cost_usd ≈ adjusted_credits × $0.01
```

- Apply the **model multiplier** (§4): e.g. Sonnet 0.6× turns a 300–700 base into
  ≈ 180–420 credits; a 2.0× premium model pushes it up.
- **Bump up** for heavy attachments, large context, or expensive tools
  (`ImageGenerate`, `deep-research`, browser automation, subagents).
  **Ease down** for light attachments and cheap tools.
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
- Authoritative rates: **Copilot Credit Guide** + **Cost Management dashboard /
  `/cost`** (per-tenant, real billed figures).

*Last refreshed from sources: 2026-06-30. Re-verify against the pages above if
Microsoft updates pricing.*
