# Guest Post Outreach — a Claude Skill

A Claude skill that runs honest, low-volume guest-post outreach for **one** target page, every day, without ever sending an email or posting anything on your behalf.

Each run it:

1. Finds new, **free**, in-niche "write for us" sites (no paid / sponsored / link-farm sites)
2. Checks each site's **Semrush Authority Score** and skips weak ones
3. Writes a short, personal pitch and saves it as a **Gmail draft** — you review and hit Send
4. Writes helpful **Quora / Reddit** answers for you to paste yourself (no links on Reddit, disclosed links on Quora)
5. Logs everything to a **tracker** so no site is ever pitched twice
6. Gives you a clean **daily report** (any language — English, Hinglish, Urdu, …)

Works for any niche and any site — you just add your own page link.

## Why it's safe to automate

| Guardrail | How |
|---|---|
| No spam | Drafts only, human sends |
| No fake community posts | Answers are text only, human posts |
| No paid links | Sites with fees / "sponsored" are skipped |
| No low-quality sites | Authority Score floor (default 15) |
| No duplicates | Tracker is checked before every pitch |
| No hard sell | 90–150 word pitches, no link in the email |

## Requirements

- Claude with skills enabled (claude.ai, Claude Code, or the API)
- **Gmail** connector (for drafts)
- **Semrush** connector (optional — Authority Score is left blank without it)
- Web search / fetch
- A tracker: a claude.ai artifact with a database, or a local `tracker.json`

## Install

**claude.ai:** download `guest-post-outreach.zip` from Releases (or zip the `guest-post-outreach/` folder) → Settings → Capabilities → Skills → Upload.

**Claude Code:**

```bash
git clone https://github.com/heyitsTalha/guest-post-outreach-skill.git
cp -r guest-post-outreach-skill/guest-post-outreach ~/.claude/skills/
```

## Configure

**Easiest:** just run the skill. On the first run Claude asks for:

1. Your page link (the one URL to promote)
2. Brand name + what the page offers
3. Your niche
4. Your name and role (for signing pitches)
5. Gmail account for drafts
6. Report language

It saves your answers as `config.md`, so every later run (including scheduled ones) uses your site automatically.

**Manual:** copy [`references/config-template.md`](guest-post-outreach/references/config-template.md), set `target_url` to your page, fill the rest, and paste it into your project instructions or save it as `config.md` next to the skill.

## Run

```
Run guest post outreach for today.
```

Or schedule it daily (e.g. a Claude scheduled task at 11:57 AM) with the prompt:

```
Use the guest-post-outreach skill with the config in this project. Work unattended and produce today's report.
```

## Structure

```
guest-post-outreach/
├── SKILL.md                      # the workflow + hard rules
├── config.md                     # created on first run with YOUR site (git-ignored)
├── references/
│   ├── config-template.md
│   ├── tracker-schema.md
│   ├── pitch-guidelines.md
│   └── report-format.md
```

## Contributing

Issues and PRs welcome — new niche examples, better search footprints, other trackers (Google Sheets, Airtable, Notion).

## License

MIT — see [LICENSE](LICENSE).
