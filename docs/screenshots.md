# Screenshots

Where to put images and how to reference them in the README.

## Where they live

All images go in the [`../screenshots/`](../screenshots/) folder at the repo root.
Reference them from the README with **relative paths** so they render correctly on
GitHub:

```markdown
![Built-in cost skill example](screenshots/cost-skill-example.png)

![Pre-cost skill example](screenshots/precost-skill-example.png)

![Decision flow](screenshots/decision-flow.png)
```

## Expected files

| File | What it should show | Status |
|---|---|---|
| `screenshots/cost-skill-example.png` | The built-in `/cost` command output — the "receipt" after a task | Placeholder — add your own |
| `screenshots/precost-skill-example.png` | A Pre-cost pre-check card with the "how to run" options | ✅ Included |
| `screenshots/decision-flow.png` | A simple Cowork-vs-lighter-tool decision diagram | Placeholder — add your own |
| `screenshots/precost-marginal-example.png` | A *Marginal* verdict on a simple email task | ✅ Included |
| `screenshots/how-to-run.png` | Adding `/precost` to a task to trigger the skill | ✅ Included |

The placeholders are referenced in the README already — once you drop the real
PNGs in with those exact names, the images appear automatically. No README edits
needed.

## Tips for good screenshots

- **Crop tight** to the relevant card or message.
- **Redact anything private** — names, email addresses, internal links, customer
  data. Blur or box it out before committing.
- Prefer **PNG** for crisp UI text.
- Keep file sizes reasonable (a few hundred KB is plenty for a UI capture).
- Use light mode for consistency, or note the theme in the caption.

## Safety reminder

Do **not** commit screenshots containing confidential information, internal-only
content, private customer data, or anything that implies this is an official
Microsoft feature. When in doubt, redact or leave it out.
