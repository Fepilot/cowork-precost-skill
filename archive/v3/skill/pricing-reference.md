# precost — Pricing & estimation reference

> Companion to `SKILL.md`, read at Step 3. Cheap local Read — never web-search
> at runtime. **OFFICIAL** = published by Microsoft (link in §11).
> **PLANNING** = this community skill's directional assumption, shown as "≈"
> with the disclaimer. Last verified: **2026-10-29**. Re-check §11 links when
> Microsoft updates pricing.

---

## 0. Your settings — edit me

| Setting | Default | Notes |
|---|---|---|
| `HOURLY_RATE` | €75 / hour (= €1.25 / minute) | Blended knowledge-worker rate for "value". Change to yours. |
| `CURRENCY` | € | Value currency. Cost is always USD (credits are USD-denominated). |
| `MONTHLY_LIMIT` | 2,000 credits / user / month | PLANNING assumption: Microsoft asks admins to set at least 2,000 credits per user per month in a spending policy. Your org may set more — the user sees their real limit and balance with `/cost`. |
| `CREDIT_PRICE` | $0.01 / credit | OFFICIAL pay-as-you-go rate. Pre-purchase (P3) is up to 20% cheaper, so prepaid customers sit at or below the $ shown. |

---

## 1. How Copilot is billed now — OFFICIAL

- **Two budgets (since 25 Sep 2026).** *Everyday AI* (chat, summaries, drafts,
  analysis in Word/Excel/PowerPoint/Outlook/Teams, Researcher, Analyst,
  Facilitator, app agents) is covered by the per-user Copilot license (USL).
  *Advanced AI* — **Cowork, Code, Autopilot, Work IQ APIs, advanced SharePoint
  work and the newest frontier models (e.g. Astra, Fable)** — is usage-based
  (UBB), metered in Copilot Credits.
- **Inside the license:** Auto (default; weighs accuracy, speed and cost per
  request), some models with fair use (e.g. GPT 5.6, Sonnet) and others with
  limits (e.g. Opus). Heavy use may hit a limit → user can continue on credits
  or reroute to Auto.
- **Cowork:** requires the Copilot license **and** credits; the license
  includes no Cowork usage. Admins must create a spending policy first.
- **What drives a Cowork task's credits (4 buckets):** model, runtime
  (orchestration, long-running work), context (emails, files, meetings, past
  interactions) and tools (actions taken). Higher reasoning effort is slower and
  uses more credits.
- **Buying credits:** pay-as-you-go $0.01/credit · Pre-Purchase Plan (P3), 5–20%
  discount by tier, expires after 1 year · prepaid capacity packs of 25,000
  credits/month. Credits are pooled per tenant across Cowork, Copilot Studio,
  Dynamics 365, Power Platform AI and Work IQ API.
- **User limits:** each user has a monthly credit limit; credits reset monthly
  and do not carry over; users can request more from their admin.
- **`/cost`:** free; shows the open task's approximate credits so far and the
  month's remaining balance. It cannot estimate a task **before** it runs —
  that gap is what this skill fills.
- **Admin controls:** Cost Management in the Microsoft 365 admin center —
  spending policies, per-user/group limits, alerts, credit requests,
  consumption by user/service/agent; Cost Management API in Microsoft Graph.

---

## 2. Official task bands — OFFICIAL (Copilot Credits Guide)

| Class | Shape | Example (Microsoft) | Credits | ≈ USD |
|---|---|---|---|---|
| **Light** | Few sources · light reasoning · ≤ 1 output | Weekly status update with priorities and key meetings from my calendar | **100–300** | $1–3 |
| **Medium** | Many sources over varying timeframes · structured reasoning · 2+ outputs | Customer-meeting prep: emails, calendar, files → briefing doc + Excel overview + client deck | **300–700** | $3–7 |
| **Heavy** | Broad aggregation over long timeframes · deep reasoning · many outputs | Analyze 6 months of product-usage data, classify prompts, leadership-ready report | **> 700** | > $7 |

Microsoft labels these "rough planning estimates". Its GA-time illustrative
ranges (Opus 4.8) were 70–200 / 400–600 / > 1,500 — so **Heavy is open-ended**:
this skill reads Heavy as **700–1,500 and flags "may exceed 1,500"** for long,
multi-source or Max-effort runs.

---

## 3. One-level bump rules — PLANNING

Move the class **at most one level**, by the single heaviest driver:

- **Up** if any: a heavy input (§6 ≥ ~2×: `.pptx`, scanned/photographed PDF,
  several images, very large files) · an expensive tool (§7) · many sources or
  a long time window beyond the class's shape · exec-ready polish with several
  revision passes requested up front.
- **Down** if: one trivial read on a light input (`.md`/`.txt`/`.csv`), no
  actions, no extra tools.
- Already Heavy → stay Heavy and read the top end / "may exceed".

---

## 4. Model tiers — PLANNING multipliers (vs. Opus-class = 1.0×)

Microsoft does not publish a per-model credit table for Cowork. Its estimator
defaults assume an Opus-class model, so **Baseline = 1.0×**. The other tiers
are derived from public list prices per million tokens (Sonnet-class ≈ 0.4× of
Opus; Fable-class ≈ 2×) and tempered by independent same-task tests where the
gap was smaller (Sonnet ≈ 0.8× of Opus) or larger (a GPT model ≈ 2.2×). Hence:

| Tier | Multiplier (range) | Models in the Cowork picker (Oct 2026 — names change often) | Use for |
|---|---|---|---|
| **Efficient** | **×0.6** (0.4–0.85) | Claude Sonnet 5 / 5.5 · GPT 5.6 Terra | Drafting, summaries, extraction, classification, standard docs/decks from a brief, trigger checks |
| **Baseline** | **×1.0** | Opus 5 / Opus 4.8 · GPT 5.6 Sol / GPT 6.1 Sol · Grok 4.7 (unverified) | Complex, high-stakes, multi-source synthesis, long agentic runs |
| **Premium / frontier** | **×2.0** (1.5–2.5) | Claude Fable 5.1 · GPT 6 Astra | Only the hardest, most ambitious work where max capability pays for itself |
| **Auto** (default) | ×0.6–1.0 | Cowork picks from your org's enabled models | Most work; safe default when unsure |

Rules:
- Unknown model → Baseline, and say "assumed".
- New name in the picker → map it by its picker label: "everyday / fast / efficient"
  → Efficient; "complex / high-stakes / hard work" → Baseline; "most advanced /
  ambitious / tough problems" → Premium. Say "tier inferred".
- Availability is tenant-specific (admins can turn model families off; some
  frontier models are off by default and may require data retention by the
  provider). Always say "if it appears in your model picker".
- Cheapest model is task-dependent: a stronger model can finish in fewer steps.
  Recommend Efficient for routine work, Baseline for judgment-heavy work,
  Premium only with a clear reason, **Auto** when unsure.

---

## 5. Reasoning effort — where to read inside the band

| Effort (picker dropdown) | Read the band at | Recommend for |
|---|---|---|
| Light | low end | routine, well-scoped work |
| Medium (default) | middle | everyday work |
| High / Extra High | top end | deeper analysis, complex reasoning |
| Max | top end + flag "may exceed" | the hardest work only |

OFFICIAL: higher effort is more thorough but slower and uses more credits; the
selected level persists across future tasks until changed — remind users to
set it back.

---

## 6. Attachment weight — PLANNING (decides the bump only)

| Input | Weight vs `.md` |
|---|---|
| `.md` / `.txt` / `.csv` | 1× |
| `.docx` | ~1.2× |
| `.xlsx` | ~1.3× |
| `.html` | ~1.7× |
| text `.pdf` | ~2–3× |
| `.pptx` | ~3–4× |
| images (`.png`/`.jpg`) | high — several images → bump |
| scanned / photographed PDF | ~3–5× |

Converting a heavy PDF/deck to `.md` (or pasting only the relevant section) is
the single biggest input lever. Weights are guides for the bump, never extra
multipliers on the band.

---

## 7. Tools, plugins & connectors — cost drivers

| Cheap | Moderate | Expensive (→ bump one class) |
|---|---|---|
| One read (a mail, an event, a file) · one short draft · no deliverable | Multi-source M365 search · one Office deliverable · editing an existing Office file · a few actions (send, schedule, post) · one plugin/connector lookup (e.g. Dynamics 365, Fabric IQ, Jira, Salesforce, ServiceNow, SAP, Workday, Zendesk) | Image generation · local browser use (multi-page web tasks) · building an app (App skill / Code — building consumes credits; hosted apps also meter run-time on the Copilot Managed Runtime) · subagents / parallel workstreams · large multi-file passes · many plugin calls · broad web research |

Plugins from partners may also need that system's own license — outside this
estimate.

---

## 8. Automations — per run × runs per month

Scheduled and event-driven Cowork tasks bill **every run**. Show both numbers.

| Frequency | Runs / month (≈) | Light (100–300) | Medium (300–700) | Heavy (700–1,500) |
|---|---|---|---|---|
| Weekly | 4 | 400–1,200 | 1,200–2,800 | 2,800–6,000 |
| Every weekday | 22 | 2,200–6,600 | 6,600–15,400 | 15,400–33,000 |
| Daily (7 days) | 30 | 3,000–9,000 | 9,000–21,000 | 21,000–45,000 |

Baseline tier shown; scale by §4. Event-driven ("on every matching email"):
ask the expected matches per month, or show "per run" and warn it scales with
volume. Lean levers for automations: lower frequency, a tight trigger filter,
"stop and post nothing if there is nothing new", Efficient model + Light effort.

---

## 9. Lookup table — band × model tier (per run)

| Class | Efficient ×0.6 | Baseline ×1.0 | Premium ×2.0 |
|---|---|---|---|
| Light | 60–180 · ≈ $0.60–1.80 | 100–300 · ≈ $1–3 | 200–600 · ≈ $2–6 |
| Medium | 180–420 · ≈ $1.80–4.20 | 300–700 · ≈ $3–7 | 600–1,400 · ≈ $6–14 |
| Heavy | 420–900 · ≈ $4.20–9 | 700–1,500 · ≈ $7–15 | 1,400–3,000 · ≈ $14–30 |

Auto → show Efficient-low to Baseline-high for that class (e.g. Medium on Auto
≈ 180–700). Share of monthly limit = upper end ÷ `MONTHLY_LIMIT` (2,000):
300 → 15% · 420 → 21% · 600 → 30% · 700 → 35% · 900 → 45% · 1,400 → 70% ·
1,500 → 75% · above 2,000 → "exceeds a 2,000 limit".

---

## 10. The lean ("sustainable") option

Apply only levers that keep the same outcome:
1. **Right-size the model** → Efficient tier or Auto for routine work.
2. **Right-size effort** → Light/Medium unless deep reasoning is needed.
3. **Narrow scope** → shorter time window, named sources/folders/people.
4. **Lighter inputs** → `.md` instead of PDF/PPTX/images; only the relevant pages.
5. **Fewer outputs per run** → one deliverable first; add others only if needed.
6. **Skip optional expensive tools** → no images, browser or subagents unless essential.
7. **Specify format up front** → template, length, audience, so fewer revision rounds
   (every follow-up in the same task re-reads context and adds credits).
8. **Automations** → lower frequency, tight trigger, "skip if nothing new".

Lean band = the §9 cell after levers (tier change, and one class down only when
scope or outputs really shrink). **Lean minimum** = its lower bound. If no lever
applies, say "already efficient" and drop the lean option.

---

## 11. Sources (public)

- Copilot Credits Guide (bands, buckets, P3, estimators) — https://www.microsoft.com/licensing/guidance/CopilotCreditsGuide
- USL vs. usage-based billing (everyday vs. advanced AI, included models) — https://learn.microsoft.com/en-us/microsoft-365/copilot/user-subscription-license-usage-based-billing
- Usage-based billing & Cost Management (services, estimator) — https://learn.microsoft.com/en-us/microsoft-365/copilot/usage-based-billing-overview-copilot-credits
- Spending policies (2,000 credits/user minimum) — https://learn.microsoft.com/en-us/microsoft-365/copilot/usage-based-billing-manage-copilot-credits
- `/cost` command — https://learn.microsoft.com/en-us/microsoft-365/copilot/usage-based-billing-copilot-credits-cost
- Choose a model for Cowork (models, Auto, reasoning effort) — https://learn.microsoft.com/en-us/microsoft-365/copilot/cowork/cowork-models
- What's new in Cowork (models, automations, browser, App skill) — https://learn.microsoft.com/en-us/microsoft-365/copilot/cowork/whats-new
- Copilot plans & pricing (what's usage-based) — https://www.microsoft.com/en-us/microsoft-365-copilot/pricing
- Public per-token list prices used for tier ratios — https://docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing
- Independent same-task model test (directional) — https://www.danielanderson.io/articles/copilot-cowork-models/
