# Pre-check Adaptive Card template

> Companion for the **precost** skill, used at **Step 7** only. Read this when you
> render the card. Fill in the values from Steps 1–6; keep colours subtle and
> on-brand. **Drop the "Run it leaner" Recommendations block when Step 5 found no
> levers.** Render it inline via the `render-ui` skill — never write it to a file.
> Keep the disclaimer wording exactly as below.
>
> **Badge and cost must agree.** The Estimated cost band is the §6 band for the
> effective class (the badge). A heavy input (`.pptx`, scanned PDF, images) or an
> expensive tool bumps the class up one level in Step 3 before you read the band
> — so e.g. a Medium task with a `.pptx` shows **HEAVY · ≈ 700–1400 credits ·
> ≈ $7–14**, not a Medium band multiplied by a weight. The example below is a
> plain Medium task (text PDF, no bump).

```json
{
  "type": "AdaptiveCard",
  "version": "1.6",
  "body": [
    { "type": "TextBlock", "text": "Cowork task pre-check", "weight": "Bolder", "size": "Medium" },
    { "type": "Badge", "text": "MEDIUM", "style": "Accent" },
    { "type": "FactSet", "facts": [
      { "title": "Model", "value": "Opus 4.8 (default · 1.0×)" },
      { "title": "Estimated cost", "value": "≈ 300–700 credits · ≈ $3–7" },
      { "title": "Attachments", "value": "1 PDF (text — no class bump)" },
      { "title": "Estimated time saved", "value": "≈ 90 min" },
      { "title": "Estimated value", "value": "≈ €110 (at €75/hr)" },
      { "title": "Verdict", "value": "Strongly positive — proceed" }
    ]},
    { "type": "TextBlock", "wrap": true, "size": "Small", "weight": "Bolder", "text": "Run it leaner" },
    { "type": "TextBlock", "wrap": true, "size": "Small", "text": "• Switch to Sonnet 4.6 (~0.6×)  • Convert the PDF to .md  • Narrow to last 30 days" },
    { "type": "TextBlock", "isSubtle": true, "wrap": true, "size": "Small",
      "text": "Estimate only — not the metered bill. It factors the model, context, runtime, tools and attachments, but the real cost depends on what actually runs and is shown by /cost and the Cost Management dashboard after the task. This pre-check is advisory, not a spending limit, and uses research-based pricing and time-savings bands (directional, not a guarantee). Running this check itself uses a small amount of credits." }
  ]
}
```
