# Examples

Three worked examples showing how Pre-cost routes different tasks. Figures are
illustrative estimates (bands, not bills) using the default €75/hr value rate.

---

## Example 1 — A quick email rewrite → do it in Copilot

**Task:** "Rewrite this paragraph in a more professional tone for a reply to a
customer."

**Pre-check:**

```
Cowork task pre-check
LIGHT

Task:            Rewrite one paragraph in a professional tone
Model:           Opus 4.8 (default · 1.0×)
Estimated cost:  ≈ 100–250 credits · ≈ $1–2.50
Attachments:     None
Time saved:      ≈ 5–10 min
Estimated value: ≈ €6–12 (at €75/hr)
Verdict:         Marginal — a per-seat tool can do this free

Run it leaner:
• Draft it for free in M365 Copilot in Outlook (no metered credits)
• Or switch to Sonnet 4.6 (~0.6×) — this is a routine draft
```

**Why:** A single-output, low-reasoning task. Cowork would work, but a per-seat
tool does the same job with **no metered credits**.

**Suggested Copilot prompt:** *"In Outlook, click Copilot → Draft with Copilot.
Paste the paragraph and ask: 'Rewrite this in a professional, friendly tone for a
customer reply.'"*

---

## Example 2 — A weekly manager-ready deck → proceed in Cowork

**Task:** "Pull highlights from my email, calendar and the team channel for the
last week and build a manager-ready highlights deck for my 1:1."

**Pre-check:**

```
Cowork task pre-check
MEDIUM

Task:            Weekly highlights deck from email + calendar + channel
Model:           Opus 4.8 (default · 1.0×)
Estimated cost:  ≈ 300–700 credits · ≈ $3–7
Attachments:     None
Time saved:      ≈ 108 min (Analysis + Document + Meeting + Communication)
Estimated value: ≈ €135 (at €75/hr)
Verdict:         Strongly positive — proceed

Run it leaner:
• Run the web/source-gathering and deck build on Sonnet 4.6 (~0.6×),
  reserve heavier reasoning for the synthesis — could cut cost to roughly half
```

**Why:** Multi-source, multi-step, single polished deliverable that would take
well over an hour by hand. The time-value clearly dwarfs the credit cost — a good
Cowork job.

**Suggested Cowork prompt:** *"Gather last week's highlights from my email,
calendar and the team channel. Group them into Wins / In progress / Risks /
Asks, then build a clean 5-slide deck for my manager 1:1. Keep it to one idea per
slide."*

---

## Example 3 — A very large task → simplify before running

**Task:** "Analyze every company in the S&P 500 — for each one produce a chat
summary, a 2-page Word cover sheet, and a 5-tab financials workbook (income
statement, balance sheet, cash flow, key ratios, valuation), with peer
comparisons."

**Pre-check:**

```
Cowork task pre-check
HEAVY

Task:            500-company analysis × (summary + Word doc + 5-tab workbook)
Model:           Opus 4.8 (default · 1.0×)
Estimated cost:  ≈ very high — far above a single Heavy band, run hundreds of times
Attachments:     None
Time saved:      large, but spread across an enormous run
Verdict:         Proceed with caution — simplify or split first
```

**Why:** This is hundreds of Heavy tasks stacked into one prompt. The estimate
balloons and the run becomes hard to predict or steer.

**Recommendation — simplify or split:**

- **Narrow the scope:** start with **one** company (or a 5–10 company shortlist)
  end to end, confirm the output is right, then scale.
- **Split the deliverables:** run the summaries first, then the cover sheets, then
  the workbooks — each as its own task so you can check quality and cost between
  stages.
- **Right-size the model:** do the data-gathering and document/spreadsheet build
  on Sonnet 4.6, and reserve heavier reasoning only for the financial synthesis.

**Suggested Cowork prompt (scoped):** *"Do a full analysis for **one** company,
[TICKER]: a short chat summary, a 2-page Word cover sheet, and a 5-tab financials
workbook (income statement, balance sheet, cash flow, key ratios, valuation with
peer comparison). I'll review it before we scale to more companies."*

---

> Every figure above is a directional estimate. The real cost depends on what
> actually runs and is shown by `/cost` and the Cost Management dashboard after
> the task.
