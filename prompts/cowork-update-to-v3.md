# Prompt for Copilot Cowork — install or update Pre-cost to v3

> [!IMPORTANT]
> Pre-cost is not an official Microsoft skill or feature. It is a community
> example — use it as inspiration and adapt it to your own business needs.

Use this prompt to **update** an existing `precost` skill (v1 or v2) to v3, or to
install v3 for the first time.

## Before you start

1. Download [`precost-skill-v3.zip`](../precost-skill-v3.zip?raw=1) from this repository.
2. Open a **new chat** in Copilot Cowork.
3. Attach `precost-skill-v3.zip` to the message.
4. Paste everything inside the box below and send it.

> Prefer the UI? Go to **Customize → Skills**, remove your old `precost` skill,
> then **Add → Upload skill** and select `precost-skill-v3.zip`.

## Prompt (copy everything inside the box)

```text
I've attached precost-skill-v3.zip. Please install it as my "precost" skill,
replacing any older version I already have.

1. Unzip the attachment. It contains one folder, precost/, with exactly four
   files: SKILL.md, pricing-reference.md, value-and-routing.md and
   card-template.md.
2. If I already have a skill named "precost" (v1 or v2), replace its contents
   completely with these four files. Remove leftover files from the old
   version (for example precost.md), so the skill has a single SKILL.md.
3. If I don't have it yet, create a new skill named "precost" from the folder.
4. Do not edit, shorten, translate or merge the files. Keep the SKILL.md
   frontmatter exactly as it is (its description is under 1,024 characters;
   Cowork ignores skills above that).
5. Keep the skill name "precost" so it triggers with /precost.
6. Do not run any other task, search, or open any other files.

When you're done, reply in 4 lines or fewer:
- skill name and version (v3),
- the files installed,
- whether an older version was replaced,
- "Open a new chat, write a task and add /precost to test it."
```

## Optional — make it yours in the same step

If you want to change the defaults while installing, add this paragraph to the
end of the prompt above. Only the settings table in `pricing-reference.md` §0
should change.

```text
After installing, edit only the "Your settings" table (§0) in
pricing-reference.md:
- HOURLY_RATE: <e.g. €90 / hour (= €1.50 / minute)>
- CURRENCY: <e.g. €>
- MONTHLY_LIMIT: <e.g. 3,000 credits / user / month>
Leave every other line in every file unchanged.
```

> [!NOTE]
> If you change `HOURLY_RATE` or `MONTHLY_LIMIT`, the worked examples elsewhere
> in the files (such as "€75/h" and "% of 2,000") still use the defaults.
> The skill reads §0 for your values, but check the first few cards.

## Test it

1. Open a **new chat** (skills load when a chat starts).
2. Send a task followed by `/precost`, for example:

   ```text
   Research my business idea for a bike-sharing service in Madrid on the web
   and build a polished 10–12 slide pitch deck with speaker notes. /precost
   ```

3. You should see the v3 card: a verdict, a class badge, credits / ≈ USD /
   time-saved tiles, a comparison chart and a "How do you want to run this?"
   question. Nothing runs until you choose.
4. For a text-only result that uses fewer credits, try `/precost lite`.
5. After any task, type `/cost` (free) to see what it actually used.

## Troubleshooting

| Problem | Fix |
|---|---|
| `precost` isn't in the `/` list | Open a new chat or reopen Cowork. |
| The old v2 card still appears | An old copy is still installed. Remove every `precost` skill in **Customize → Skills** and upload the zip again. |
| Cowork says the skill is invalid | Make sure `SKILL.md` is unchanged. If you edited the description, keep it under 1,024 characters. |
| Two `precost` skills appear | Delete the older one so `/precost` always uses v3. |
