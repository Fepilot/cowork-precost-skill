# Usage

How to use **Pre-cost** step by step.

## 1. Install the skill

1. Open [`../skill/precost.md`](../skill/precost.md) and copy its contents. If your
   Cowork environment supports multi-file skills, also copy the companion files in
   the same folder:
   - [`../skill/pricing-reference.md`](../skill/pricing-reference.md)
   - [`../skill/value-and-routing.md`](../skill/value-and-routing.md)
   - [`../skill/card-template.md`](../skill/card-template.md)
2. In Cowork, create a **new custom skill**.
3. Paste in the instructions.
4. Name it **`Pre-cost`**.
5. (Optional) Assign it the command **`/precost`**.

> Prefer a single self-contained prompt instead? Use
> [`../prompts/precost-system-prompt.md`](../prompts/precost-system-prompt.md).

## 2. Run a pre-check

Before (or at the start of) a task, type **`/precost`** — or just include it with
your request:

```
Build me a weekly highlights deck for my 1:1 with my manager, pulling from my
email, calendar and the team channel. /precost
```

Pre-cost runs **once**, at the start of the task. It does **not** re-run on
follow-up messages like "make the title bigger" or "add a slide".

## 3. Read the card

You'll get a compact card with:

| Field | What it tells you |
|---|---|
| **Class badge** | Light / Medium / Heavy |
| **Model** | The active model and its credit multiplier |
| **Estimated cost** | A credit band and a rough dollar band |
| **Attachments** | What you attached and how much weight it adds |
| **Estimated time saved** | Roughly how long the same work would take by hand |
| **Estimated value** | Time saved × your hourly rate (default €75/hr) |
| **Verdict** | *Strongly positive — proceed* or *Marginal — a per-seat tool can do this free* |
| **Run it leaner** | Optional, only when a cheaper path genuinely exists |

A short disclaimer always appears: this is an **estimate**, not the metered bill.

## 4. Choose how to proceed

After the card, Pre-cost asks one question. Typical options:

- **Proceed in Cowork** — run the task as written. Best for Medium/Heavy,
  multi-deliverable work.
- **Use Cowork — sustainably** — same outcome, fewer credits (e.g. a lighter
  model, a converted attachment, tighter scope). Offered when a lever applies.
- **Use Copilot Chat / M365 Copilot instead** — for small tasks a per-seat tool
  does with no metered credits. Pre-cost gives you the concrete steps and a
  suggested prompt for that tool.

## 5. (Optional) Adjust the assumptions

- **Hourly rate.** The default value rate is **€75/hr**. Tell Pre-cost your own
  rate (e.g. "use €120/hr") and the value estimate updates.
- **Model.** Mention the model you'll use, or let Pre-cost detect it. If it can't
  tell, it assumes the Cowork default (Opus 4.8, 1.0×) and says so.
- **Attachments.** Heavy formats (PDFs, slides, images) drive cost up. Converting
  to `.md` first is the single biggest sustainability lever.

## Tips

- Use it on tasks you're **unsure** about — not every trivial message.
- Treat the verdict as a **second opinion**, not a hard rule.
- For the **real** cost after a task, use the built-in **`/cost`** command and the
  **Cost Management dashboard**.
