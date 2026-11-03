# precost — Card template (Step 5)

> Companion to `SKILL.md`. Read only at Step 5 (skip in lite mode). Layout
> test-rendered in Cowork on 2026-10-29; links use RichTextBlock text runs
> (plain TextBlocks show markdown links as raw text). Fill the values, keep the
> structure, make ONE `render_ui` call (raw card: `type`, `version`, `body`).
> Never write the card to a file. Do not restate the card in text afterwards —
> go straight to the Step 6 question.

## Fill rules

| Slot | What to put |
|---|---|
| Subtitle | The task in ≤ 12 words: input → outputs (+ "weekly" / "on every email" for automations) |
| Badge | `LIGHT` (style `Good`) · `MEDIUM` (`Warning`) · `HEAVY` (`Attention`) — the class after the bump |
| Verdict container | style `good` for 🌱/✅/💡, `attention` for ⚠️. One line: emoji + verdict + the main reason or saving |
| KPI 1 · Credits | band as written; small green line "lean ≈ …" (omit if no lean option) |
| KPI 2 · Cost | ≈ USD (credits ÷ 100); small green "lean ≈ $…" |
| KPI 3 · Time saved | ≈ minutes; small line "≈ €value at €75/h" (rate from §0) |
| Automations | change labels to "Credits / run" and add to the subtitle "≈ X–Y / month" |
| Bar chart | upper ends: as written (`warning`), lean (`good`), M365 Copilot route at 0 (`good`, name the tool flow). Drop a bar that doesn't apply; keep ≥ 2 bars |
| Recommended | model · effort, with "(if in your picker; else Auto)" |
| Cost drivers | the 2–4 signals that set the class (sources, outputs, inputs, tools, runs) |
| Lean minimum | lower bound of the lean band (omit if no lean option) |
| Monthly limit | % of `MONTHLY_LIMIT` from §9 + "assumed limit; /cost shows yours". ProgressBar: < 25% `Good` · 25–50% `Warning` · > 50% `Attention` |
| Run it lean | ≤ 3 levers from §10, short; drop the block if none |
| Source link | always keep the Copilot Credits Guide link (the bands' source); keep the Model guide link when a model is recommended |
| Footer | keep the community note + disclaimer text verbatim |

## Template (worked example: Medium task, model unknown → Opus-class baseline)

```json
{"type":"AdaptiveCard","version":"1.6","body":[
{"columns":[{"items":[{"size":"Large","text":"💰 Cowork pre-check","type":"TextBlock","weight":"Bolder","wrap":true},{"isSubtle":true,"spacing":"None","text":"Contoso meeting prep → briefing doc + client deck + email to the team","type":"TextBlock","wrap":true}],"type":"Column","width":"stretch"},{"items":[{"size":"Large","style":"Warning","text":"MEDIUM","type":"Badge"}],"type":"Column","verticalContentAlignment":"Center","width":"auto"}],"type":"ColumnSet"},
{"items":[{"text":"🌱 Verdict: worth it in Cowork — run it lean (≈ −40% credits)","type":"TextBlock","weight":"Bolder","wrap":true}],"spacing":"Small","style":"good","type":"Container"},
{"columns":[{"items":[{"horizontalAlignment":"Center","isSubtle":true,"text":"Credits","type":"TextBlock","wrap":true},{"horizontalAlignment":"Center","size":"ExtraLarge","text":"≈ 300–700","type":"TextBlock","weight":"Bolder","wrap":true},{"color":"Good","horizontalAlignment":"Center","size":"Small","spacing":"None","text":"lean ≈ 180–420","type":"TextBlock","wrap":true}],"type":"Column","width":"stretch"},{"items":[{"horizontalAlignment":"Center","isSubtle":true,"text":"Cost","type":"TextBlock","wrap":true},{"horizontalAlignment":"Center","size":"ExtraLarge","text":"≈ $3–7","type":"TextBlock","weight":"Bolder","wrap":true},{"color":"Good","horizontalAlignment":"Center","size":"Small","spacing":"None","text":"lean ≈ $1.80–4.20","type":"TextBlock","wrap":true}],"type":"Column","width":"stretch"},{"items":[{"horizontalAlignment":"Center","isSubtle":true,"text":"Time saved","type":"TextBlock","wrap":true},{"horizontalAlignment":"Center","size":"ExtraLarge","text":"≈ 113 min","type":"TextBlock","weight":"Bolder","wrap":true},{"horizontalAlignment":"Center","isSubtle":true,"size":"Small","spacing":"None","text":"≈ €141 at €75/h","type":"TextBlock","wrap":true}],"type":"Column","width":"stretch"}],"spacing":"Medium","type":"ColumnSet"},
{"data":[{"color":"warning","x":"Cowork as written · Opus-class","y":700},{"color":"good","x":"Cowork lean · Sonnet 5","y":420},{"color":"good","x":"M365 Copilot · Researcher → Word → PowerPoint","y":0}],"showLegend":false,"showTitle":true,"title":"Estimated credits (upper end)","type":"Chart.HorizontalBar"},
{"facts":[{"title":"Recommended","value":"Sonnet 5 · effort Medium (if in your picker; else Auto)"},{"title":"Cost drivers","value":"4 sources · 2 deliverables + 1 email · 1 text PDF"},{"title":"Lean minimum","value":"≈ 180 credits"},{"title":"Monthly limit","value":"≈ 35% of 2,000 (lean ≈ 21%) — assumed limit; /cost shows yours"}],"spacing":"Medium","type":"FactSet"},
{"color":"Warning","type":"ProgressBar","value":35},
{"type":"RichTextBlock","spacing":"Medium","inlines":[{"type":"TextRun","text":"Run it lean: ","weight":"Bolder","size":"Small"},{"type":"TextRun","text":"select Sonnet 5 · Medium before launching · last 30 days only · convert the PDF to .md","size":"Small"}]},
{"type":"RichTextBlock","spacing":"Small","inlines":[{"type":"TextRun","text":"📘 How it's calculated — Copilot Credits Guide","size":"Small","color":"Accent","underline":true,"selectAction":{"type":"Action.OpenUrl","url":"https://www.microsoft.com/licensing/guidance/CopilotCreditsGuide"}},{"type":"TextRun","text":"  ·  ","size":"Small","isSubtle":true},{"type":"TextRun","text":"Model guide","size":"Small","color":"Accent","underline":true,"selectAction":{"type":"Action.OpenUrl","url":"https://learn.microsoft.com/en-us/microsoft-365/copilot/cowork/cowork-models"}}]},
{"isSubtle":true,"size":"Small","spacing":"Medium","text":"Community skill — not an official Microsoft tool; adapt it freely. Estimate only (official planning bands × directional model factors), not your bill: actual usage depends on what runs — type /cost (free) afterwards. This pre-check itself uses a small number of credits.","type":"TextBlock","wrap":true}
]}
```

## Lite mode (no card) — 7 lines of text

```
💰 Cowork pre-check — <task in ≤ 12 words>   [<CLASS>]
Verdict: <emoji + verdict>
Estimate: ≈ <band> credits (≈ $<usd>) · lean ≈ <lean band> · M365 Copilot route: no Cowork credits (<tool flow>)
Recommended: <model> · effort <level> (if in your picker; else Auto)
Time saved: ≈ <min> min (≈ €<value>) · ≈ <pct>% of an assumed 2,000-credit month
Source: Copilot Credits Guide — https://www.microsoft.com/licensing/guidance/CopilotCreditsGuide
Community skill, not official Microsoft · estimate, not your bill (/cost is free) · this check uses a few credits.
```
