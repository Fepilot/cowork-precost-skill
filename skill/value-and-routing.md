# Value Bands & Tool Routing (with step-by-step alternatives)

> Companion reference for the **precost** skill. Loaded on demand by `SKILL.md`
> for: (a) the **time-saved / value** estimate, (b) the **which-Copilot-to-use**
> routing, and (c) the **step-by-step instructions** to hand the user when they
> choose a lighter tool instead of Cowork. Reading this file is a **cheap local
> Read** — compatible with the skill's "fast, local-only" rule.

**Sourcing & safety note.** The routing guidance reflects Microsoft's public
"what to use and when" positioning for Copilot Chat, Microsoft 365 Copilot, and
Cowork (see **Sources**). The time-savings bands are **directional planning
estimates** from the Cowork ROI methodology — not a guarantee. No internal or
confidential data is included.

---

## 1. Time saved per run — PLANNING ESTIMATE

Map the task to the categories it actually touches and **sum the Typical minutes
saved**. A multi-part task touches several (e.g. meeting prep = Analysis +
Document + Meeting).

| ROI category | Typical min saved / run |
|--------------|-------------------------|
| Analysis & Research | 60 |
| Document & content creation | 24 |
| Email workflows | 5 |
| Meeting workflows | 24 |
| Communication workflows | 4 |
| Specialized workflows (cross-system) | 25 |
| Write or debug code | 56 |
| General assistance / Other | 5 |

### Value formula

```
time_saved_hours = total_minutes_saved / 60
value           = time_saved_hours × HOURLY_RATE
```

- **`HOURLY_RATE` default = €75/hour** — a blended knowledge-worker assumption.
  State it on the card so it's transparent; the user can change it.
- **Cost is in USD** (credits are USD-denominated); **value is in the user's
  currency**. Do **not** invent an FX rate — present cost and value side by side
  and give the verdict qualitatively.

---

## 2. Verdict logic

- **Strongly positive — proceed.** Time-value clearly dwarfs credit cost. Typical
  for **Medium/Heavy multi-deliverable** tasks (several artifacts, cross-system
  work). Recommend staying in Cowork.
- **Marginal — offer a lighter tool.** A **Light** task whose single output a
  per-seat tool (Copilot Chat / M365 Copilot) produces at **no metered credit
  cost**. Surface the alternative but let the user choose.
- **Heavy / broad — consider splitting.** A single request that spans many
  sources or deliverables and lands at the top of the **Heavy** band. Still worth
  running in Cowork, but suggest **splitting it into scoped sub-tasks** (or
  narrowing the scope) so each run is cheaper, easier to review, and less likely
  to burn credits on a wrong turn.

---

## 3. Which Copilot to use when — OFFICIAL positioning

Cowork credits are only worth spending when the task needs **agentic,
multi-step, multi-artifact, cross-system** execution. For everything lighter, a
per-seat tool does the job with **no metered Cowork credits**.

| If the task is… | Best tool | Metered Cowork credits? |
|-----------------|-----------|--------------------------|
| Brainstorm, find info, quick Q&A | **Copilot Chat** | No |
| Catch up on emails or meetings | **M365 Copilot** | No |
| Create / edit a **single** artifact (one doc, one email, one summary) | **M365 Copilot** | No |
| Single-output deep research | **M365 Copilot** | No |
| **Multi-artifact creation in one task** | **Cowork** (stay) | Yes |
| **Multi-step process across systems** | **Cowork** (stay) | Yes |
| **Long-running autonomous job** (compare thousands of files, batch jobs) | **Cowork** (stay) | Yes |

---

## 4. Step-by-step: do it in M365 Copilot / Copilot Chat instead

Use these when the user picks **"Use Copilot Chat / M365 Copilot instead."** Pick
the recipe that matches the task, name the tool, and give the user the concrete
steps. Keep it to the few steps that apply — don't pad.

### A. Quick question / brainstorm / find info → **Copilot Chat**
1. Open **Copilot Chat** (the chat icon in Teams, Outlook, or
   **microsoft365.com/chat**; or the toggle in the Microsoft 365 app — switch from
   the agentic/Cowork view back to **Chat**).
2. Type the question in natural language. Add **"use the web"** if it needs
   current public info.
3. Refine by replying in the same thread. **No Cowork credits are metered.**

### B. Summarize / catch up on email → **M365 Copilot in Outlook**
1. Open **Outlook**.
2. For one thread: open it and choose **Summary** at the top of the message.
3. For a sweep: open **Copilot Chat** in Outlook and ask, e.g. *"Summarize unread
   mail from the last 2 days and list what needs a reply."*

### C. Recap a meeting → **M365 Copilot in Teams**
1. Open the meeting in **Teams** (it must have a recording/transcript).
2. Open the **Recap** tab, or ask Copilot *"Summarize this meeting and list action
   items and decisions."*

### D. Create or edit **one** document → **M365 Copilot in the app**
1. Open **Word / Excel / PowerPoint**.
2. Use the **Copilot** button: *"Draft a one-page proposal about X"* (Word),
   *"Summarize and chart this table"* (Excel), *"Create a 5-slide deck from this
   doc"* (PowerPoint).
3. Iterate inline with follow-up prompts. **No Cowork credits are metered.**

### E. Draft / reply to **one** email → **M365 Copilot in Outlook**
1. In **Outlook**, start a new message or open the one to reply to.
2. Click **Copilot → Draft with Copilot**, describe the message, generate, edit,
   send.

### F. Single-output deep research → **M365 Copilot (Researcher agent)**
1. Open **Copilot Chat** / the **Researcher** agent in the Microsoft 365 app.
2. Ask the research question in one prompt; it returns a single grounded answer
   with sources — **no metered Cowork credits**.

> If the task actually needs **several** of the above chained together (e.g.
> *read mail + recap a meeting + build a doc + a deck, in one go*), that is a
> genuine **Cowork** job — staying in Cowork is the right call.

---

## Sources (public, customer-facing)

- **Microsoft 365 Copilot plans & pricing** (Chat included; Cowork metered) —
  https://www.microsoft.com/en-us/microsoft-365-copilot/pricing
- **What's the difference between Microsoft Copilot (free) and Copilot in
  Microsoft 365** —
  https://support.microsoft.com/en-us/Microsoft-365-Copilot/what-s-the-difference-between-microsoft-copilot-free-and-copilot-in-microsoft-365
- **Microsoft 365 Copilot (FastTrack) — usage scenarios** —
  https://learn.microsoft.com/en-us/microsoft-365/fasttrack/microsoft-365-copilot
- **Copilot Cowork GA — scenarios & model choice** —
  https://www.heise.de/en/news/From-Chat-to-Agent-Copilot-Cowork-for-Microsoft-365-is-here-11335714.html

*Last refreshed from sources: 2026-06-30.*
