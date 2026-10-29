# Make Pre-cost yours — upgrade ideas

> **Pre-cost is not an official Microsoft skill.** It is a community example
> built to show what anyone can do with Cowork skills. Use it as-is, as
> inspiration, or as the starting point for your own skill. Change the
> questions, the numbers and the routes to fit how *your* business works.

Pre-cost answers one generic question: *"Is this task worth running in Cowork,
and how do I run it with fewer credits?"* Your organization probably has a more
specific one: *"Is this process worth automating?"*, *"Does this pay back for my
team?"*, *"Which of our own agents should handle this?"* The ideas below show how
to get there.

---

## Step 0 — Get it into your Cowork first

1. Download `precost-skill-v3.zip` from this repository.
2. In Cowork, open **Customize → Skills → Add → Upload skill** and select the
   `.zip`. (Or open a new Cowork chat, attach the `.zip` and ask: *"Install this
   as my skill named precost."*)
3. Test it: write any task and add `/precost` at the end.
4. Now improve it in plain language — open a Cowork chat and say, for example:
   *"Edit my precost skill: before estimating, ask me which business process
   this task belongs to."* Cowork edits the skill files for you.
5. Prefer GitHub? Fork this repo, edit the files under `skill/`, zip the folder
   and upload it again.

Tip: keep the description (frontmatter) under ~800 characters. Cowork ignores
skills whose description is longer than 1,024 characters.

---

## Idea 1 — Process-discovery questions (for automations)

Today Pre-cost asks at most 3 questions (outcome, scope, frequency). If your
users mainly want to **automate a recurring process**, ask about the process
instead, so the estimate and the route fit reality.

Add to `SKILL.md` → Step 2:

```markdown
If the task is a recurring process, ask (max 4, skip what the prompt answers):
- Trigger: on a schedule, on an incoming email/Teams message, or on demand?
- Volume: how many runs or items per week?
- Systems: only Microsoft 365, or also CRM / ERP / ticketing (which plugin)?
- Human checkpoints: does anyone need to approve before something is sent?
Then show cost per run and per month, and flag any step that needs a plugin
or an approval.
```

Why it matters: a task that runs every weekday costs ~22× a one-off. A tight
trigger ("only emails from customers with 'invoice' in the subject") can cut
that a lot.

---

## Idea 2 — ROI questions that can change the verdict

Pre-cost v3 often recommends the Microsoft 365 Copilot route because it uses no
Cowork credits. But **no credits ≠ cheapest overall**: that route usually
means more of the user's own time (hand-offs between Researcher, Word,
PowerPoint, Outlook). For some customers, Cowork pays for itself.

Add to `SKILL.md` → Step 2 (or a new Step 4b):

```markdown
Ask (max 3):
- How long does this take you today, by hand or with M365 Copilot? (minutes)
- Who does it (role) and how often?
- What happens if it is late or wrong? (low / medium / high impact)
Then compare: (minutes saved by Cowork vs. the M365 Copilot route) × hourly
rate × runs per month, against the Cowork credits for the same runs. If the
time value is clearly higher, switch the verdict to "Cowork pays back" and say why.
```

Worked example (numbers from the v3 tables, €75/h default rate):

| | M365 Copilot route | Cowork (lean) |
|---|---|---|
| Weekly customer-account review (brief + deck + email) | Researcher → Word agent → PowerPoint agent → Outlook: ≈ 35 min of the user's time | ≈ 5 min to review the result |
| Credits per run | 0 Cowork credits | ≈ 180–420 credits (≈ $1.80–4.20) |
| Per month (4 runs) | 0 credits, but ≈ 2 h more of the user's time | ≈ 720–1,680 credits (≈ $7.20–16.80) |
| Time value of the difference | — | 30 min × 4 runs ≈ **€150 / month** |

→ For this team, Cowork is the better investment, even though it is metered.
Add the business impact (late reports, missed follow-ups) and the case gets
stronger.

---

## Idea 3 — Your own numbers

Edit `pricing-reference.md` §0:
- **Hourly rate by role** (e.g. analyst €55, manager €95, sales €80) instead of one blended €75.
- **Your real monthly credit limit** (users can see theirs with `/cost`).
- **Your currency** for value.
- **Approved models** only — remove models your tenant does not offer.

## Idea 4 — Route to *your* agents and plugins

Add rows to `value-and-routing.md` §3 and recipes to §4 for the agents your
organization already has: a Copilot Studio HR agent, a Dynamics 365 Sales
plugin, a ServiceNow or Jira connector, an internal knowledge agent. Pre-cost
will then send users to the cheapest *approved* tool for the job.

## Idea 5 — Budget guardrails

```markdown
If the upper estimate is above 1,000 credits (or 50% of the monthly limit),
show a ⚠️ banner, propose the lean plan first and ask the user to confirm the
budget before proceeding.
```

## Idea 6 — Learn from real usage

After the task, ask the user to type `/cost` (free) and log *estimate vs.
actual* in an Excel table or SharePoint list. After 20–30 runs, adjust the
bands and the model tiers in `pricing-reference.md` to your real data.

## Idea 7 — Department presets

Create variants such as `precost-sales`, `precost-finance` or `precost-hr`
with typical tasks, sources and routes for each team, so the questions and the
examples feel familiar.

## Idea 8 — Language and tone

Translate the card text and questions (e.g. Spanish, French, German) and adapt
the tone to your culture. Keep the disclaimer.

## Idea 9 — Share the result

Let the skill post the card to a Teams channel ("cost of the week") or add it
to a project page, so teams learn which tasks are worth Cowork.

## Idea 10 — Sustainability reporting

Count how many tasks users moved to the lean option or to Microsoft 365
Copilot, and the credits avoided. Present it as *compute avoided* — do not
invent CO₂ figures.

---

## Ground rules when you adapt it

- Keep it **clearly labelled as unofficial** if you share it.
- Keep **the check itself cheap**: no web searches, mail or file reads during
  the estimate. Every extra question or lookup adds credits. In our test the
  full check (card included) used **56 credits ≈ $0.56**; `/precost lite`
  (text only, no card) should cost less.
- Use **ranges, not exact prices**, and link to the official sources.
- Never put confidential data, internal prices or private screenshots in a
  public repository.
