# precost — Value, verdict & lighter routes

> Companion to `SKILL.md`. Read §1–§3 at Step 4 and §4–§5 only when the user
> picks "Use M365 Copilot instead". Cheap local Read. Time-saved figures are
> directional planning estimates (community methodology), not a guarantee.
> Last verified: **2026-10-29**.

---

## 1. Time saved per run — PLANNING

Sum the typical minutes of every category the task touches (meeting prep =
Analysis + Document + Meeting).

| Category | Typical minutes saved |
|---|---|
| Analysis & research | 60 |
| Document & content creation | 24 |
| Meeting workflows | 24 |
| Specialized cross-system workflow | 25 |
| Write or debug code / build an app | 56 |
| Email workflows | 5 |
| Communication (Teams posts, updates) | 4 |
| General assistance / other | 5 |

**Value ≈ minutes × €1.25** (at the §0 default of €75/h): 30 min ≈ €38 ·
60 ≈ €75 · 90 ≈ €113 · 108 ≈ €135 · 120 ≈ €150 · 180 ≈ €225. For recurring
tasks, value scales with runs just like cost. Cost is USD, value is the user's
currency — show them side by side, never convert.

---

## 1b. Your time on each route — PLANNING

"No Cowork credits" still costs the user's time: prompting, waiting, moving
output between apps, fixing format. Planning minutes of hands-on time:

| M365 Copilot step (recipe in §4) | Hands-on minutes |
|---|---|
| Researcher report (A) | ≈ 10 |
| Analyst / Excel analysis (B, E) | ≈ 10 |
| Word document (C) | ≈ 10 |
| PowerPoint deck (D) — add ≈ 10 more if it must be brand-polished | ≈ 10–15 |
| Outlook / Teams step (F, G) | ≈ 5 |
| Each hand-off between apps (copy, attach, re-prompt) | + 5 |

Cowork route: ≈ 5–10 min to write the prompt and review the result
(+ 5 per deliverable that needs a careful check).

Example — research + polished 10–12 slide deck: M365 route = Researcher 10 +
hand-off 5 + PowerPoint 15 (+ 10 brand polish) ≈ 30–40 min · Cowork ≈ 10 min.

---

## 2. Verdict rules (check in this order — first match wins)

0. **⛔ Not enough credits** — caution 🔴, only possible when the balance is
   known (`pricing-reference.md` §11).
   Offer lean only if its upper end ≤ 60% of what's left; otherwise the M365
   Copilot route, split the task, wait for the reset, or request credits.
1. **Cowork-only work** → ✅ or 🌱 below. Cowork is the right route when the
   task needs: multi-step work chained across apps, several deliverables with
   one consistent design, actions (send, schedule, post, update records),
   partner plugins/connectors, browser tasks, app building, long-running or
   event-driven automation.
2. **M365 Copilot can do it** (a §3 route gives the same outcome, no item from
   rule 1) → decide on *total* cost, not credits alone:
   - Time difference = M365 hands-on minutes − Cowork review minutes (§1b).
   - Value of that time = difference × per-minute rate (§1).
   - **🌱 "Cowork pays back"** when value ≥ 3× the lean Cowork upper cost in
     USD (caution 🟢) or ≥ 5× (🟡 / 🟠) — the margin absorbs the currency difference, so no
     exchange rate is needed — OR a quality need applies (brand template,
     exec-ready polish, generated visuals, several matching artifacts) and the
     caution level is 🟢. Say which reason won.
   - Otherwise **💡 Use M365 Copilot instead** — state the trade-off ("≈ N min
     more of your time, 0 Cowork credits").
3. **⚠️ Rescope first** — the outcome is still vague after Step 2, a Heavy
   task is set to a Premium model without a clear need, or caution is 🟠 Big
   spend (show it as "⚠️ Big spend — run lean or split").
4. Among Cowork verdicts: **🌱 run it lean** when a lean lever cuts the upper
   end by ≥ 30% (Baseline → Efficient = −40%) or caution is 🟡; else
   **✅ Cowork as written**.

Worked example (research + polished deck, Medium, balance unknown → spend size
Medium → 🟢): lean Cowork ≈ 180–420 credits (≈ $1.80–4.20). M365 route ≈ 30–40
min vs Cowork ≈ 10 → 20–30 min ≈ €25–38 ≥ 3 × $4.20 → 🌱 Cowork pays back.
If a `/cost` result in the chat shows only ~500 credits left: as written 700 =
140% (🔴) and lean 420 = 84% (> 60%) → ⛔ → 💡 M365 Copilot route.

---

## 3. Routing table — which tool, which meter

| If the task is… | Lighter route (M365 Copilot) | Cowork credits? |
|---|---|---|
| Quick question, brainstorm, find info | Copilot Chat (Auto) | No |
| Deep research with citations (work + web), one report | **Researcher** | No* |
| Analyze a spreadsheet/CSV, trends, charts, forecasts | **Analyst** or Copilot in Excel | No* |
| One document from a brief or sources | **Word agent** (in Copilot Chat) or Copilot in Word | No* |
| One deck (from a brief or a Word file) | **PowerPoint agent** or Copilot in PowerPoint | No* |
| One workbook/model | **Excel agent** or Copilot in Excel | No* |
| Catch up / triage / draft one email | Copilot in Outlook | No* |
| Recap or run a meeting | Teams Recap · Facilitator | No* |
| Ongoing project context from many files | Copilot Notebooks | No* |
| Recurring digest of mail/calendar/Teams | Scheduled prompts in Copilot Chat | No* |
| Meeting prep pack (brief + deck) | Researcher → Word agent → PowerPoint agent | No* |
| Data report with narrative | Analyst → Word agent → Outlook draft | No* |
| Chained actions, many artifacts, plugins, browser, apps, event triggers | — stay in **Cowork** | Yes |

\* Included in the Microsoft 365 Copilot license within fair use. Choosing a
frontier model (e.g. Astra, Fable) or exceeding a model's limit can switch to
credits — see §5.

---

## 4. Step-by-step recipes (adapt the prompts to the user's task)

Entry point for all: the **Microsoft 365 Copilot app** (Copilot in Teams,
Outlook, microsoft365.com or m365.cloud.microsoft). Agents such as Researcher
and Analyst are pinned there or can be called with **@Researcher** /
**@Analyst** in Copilot Chat. Menu names can differ by version/tenant.

**A. Research report → Researcher**
1. Open Researcher. 2. Paste: *"Research <topic> using my emails, meetings and
files from <period> plus reliable web sources. Output: a 1-page brief with
key facts, risks, open questions and citations."* 3. Answer its clarifying
questions; let it run. 4. Export/open the result in Word or a Page to share.

**B. Data analysis → Analyst (or Copilot in Excel)**
1. Open Analyst and attach the `.xlsx`/`.csv` (or open the file in Excel →
Copilot). 2. *"Clean this data, show the top 5 trends for <metric> by
<dimension>, chart them, and flag anomalies with a one-line explanation."*
3. Ask follow-ups; download the output file.

**C. One document → Word agent / Copilot in Word**
1. In Copilot Chat ask the Word agent (or open Word → Copilot): *"Create a
<type> for <audience> from <source files / the Researcher output>. Sections:
<…>. Length: <…>. Tone: <…>."* 2. Iterate inline; it saves to OneDrive.

**D. One deck → PowerPoint agent / Copilot in PowerPoint**
1. *"Create a <N>-slide deck for <audience> from <Word file / brief>, using our
brand template, one key message per slide, speaker notes included."*
2. Refine slide by slide.

**E. One workbook → Excel agent / Copilot in Excel**
1. *"Build a workbook that <goal> with inputs, formulas, a summary sheet and a
chart."* 2. Check formulas before sharing.

**F. Email → Copilot in Outlook**
Thread: open it → **Summary**. Sweep: Copilot in Outlook → *"Summarize my
unread mail from the last 2 days and list what needs a reply."* Reply: **Draft
with Copilot** → review → send.

**G. Meetings → Teams**
Before: Copilot Chat → *"Prep me for <meeting> on <date>: attendees, recent
threads, open actions."* During: add **Facilitator** for live notes and
agenda. After: **Recap** tab → *"Decisions, owners and next steps."*

**H. Multi-file project context → Copilot Notebooks**
Create a notebook, add the files/pages/links, then ask grounded questions or
*"Draft a status summary from these references."*

**I. Recurring digest → scheduled prompt**
1. Run the prompt once in Copilot Chat (Work IQ), e.g. *"Every Monday 8:00:
summarize last week's emails and Teams threads about <project>; list decisions,
risks and my open actions."* 2. Hover your message → clock icon **Schedule
this prompt** → set recurrence. Scope is mainly mail, calendar and Teams — for
files use a Notebook.

**Combos** (chain the outputs; open each next step with the previous file):
- **Meeting prep pack:** A (brief) → C (briefing doc) → D (client deck).
- **Monthly data report:** B (analysis + charts) → C (narrative) → F (email
  draft to stakeholders).
- **Customer/market scan:** A (research) → D (5-slide readout).

When the chain needs more than ~4 hand-offs, actions in several apps, or the
same thing every week with files, say so: Cowork (lean) is likely the better
trade-off.

---

## 5. Stay inside your license (no surprise credits)

- Leave Copilot Chat / Researcher on **Auto** or an included model; frontier
  models (e.g. Astra, Fable) are usage-based even outside Cowork.
- Some models are included **with limits** (e.g. Opus). When you near a limit
  you'll be notified and can switch back to Auto at no extra cost.
- Agents your organization builds that read SharePoint or connector data may be
  metered for unlicensed users — licensed users are generally covered.

---

## Sources (public)

- Copilot plans & pricing — https://www.microsoft.com/en-us/microsoft-365-copilot/pricing
- USL vs. usage-based billing — https://learn.microsoft.com/en-us/microsoft-365/copilot/user-subscription-license-usage-based-billing
- Scheduled prompts — https://learn.microsoft.com/en-us/microsoft-365/copilot/scheduled-prompts
- Copilot extensibility cost considerations (agents) — https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/cost-considerations
- Microsoft 365 Copilot release notes — https://learn.microsoft.com/en-us/microsoft-365/copilot/release-notes
