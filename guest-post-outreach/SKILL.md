---
name: guest-post-outreach
description: Daily white-hat guest-post outreach for one target page. Finds free, in-niche "write for us" sites, checks Semrush Authority Score, creates Gmail DRAFT pitches (never sends), writes helpful Quora/Reddit answers to paste manually, logs everything to a tracker, and produces a daily report. Use when the user asks to run, schedule or set up guest post / link outreach for a page.
---

# Guest Post Outreach

Run one day of honest, low-volume guest-post outreach for a single target page. The agent prepares everything; a human reviews and sends.

## Hard rules (never break these)

1. **Never send email.** Only create Gmail drafts. The human sends.
2. **Never post anywhere** (Quora, Reddit, forums, comment boxes, forms). Only produce ready-to-paste text.
3. **Free sites only.** Skip any site that charges, says "sponsored post", "paid placement", or "no free links".
4. **In-niche only.** Skip link farms, "we accept all niches" sites, and any write-for-us page that lists casino / CBD / crypto / loans.
5. **Minimum authority.** Skip sites whose Semrush Authority Score is below `min_authority` (default 15).
6. **No repeats.** Never pitch a domain or answer a question that is already in the tracker, whatever its status.
7. **Honest pitches.** 90–150 words, no hard sell, no flattery, no link in the pitch email, no fees offered.
8. **Reddit answers contain no links.** Quora answers may include the target link only when it directly answers the question, followed by a disclosure such as "(I work with <company>)".
9. Never use any name listed in `forbidden_names`.

If a tool needed for a step is missing, skip that step, continue, and say so plainly in the report. Work unattended: do not stop to ask questions.

## Setup — first run only (add your own site)

Look for a filled config in the project instructions, a `config.md` next to this skill, or the prompt. If there is none, or `target_url` is missing, and the user is present, ask for these in one message before doing anything else:

1. **Your page link** — the one URL you want guest posts to point to
2. Company / brand name and a 1–2 line description of what the page offers
3. Your niche (e.g. "personal finance", "SaaS marketing", "workplace safety")
4. Your name and role (used to sign the pitches)
5. The Gmail account to save drafts in
6. Report language (default English)

Fill `references/config-template.md` with the answers, show it to the user, and save it as `config.md` (or tell them to paste it into their project instructions) so later runs, including scheduled ones, skip this step. If the run is unattended and no config exists, stop and report that setup is needed; never guess a target page.

## Step 0 — Load config and tracker

Read the config (format in `references/config-template.md`). Required keys: `target_url`, `company`, `offer_summary`, `sender_name`, `sender_role`, `gmail_account`, `niche`, `tracker`. Optional: `daily_sites` (5), `min_authority` (15), `max_semrush_calls` (10), `community_answers` (3), `report_language` (English), `seed_sites`, `skip_sites`, `regions`, `forbidden_names`.

Get today's date in the user's timezone (`current_time` tool, else `date`).

Load the tracker (schema in `references/tracker-schema.md`):
- **Artifact database** (claude.ai): `ArtifactData` list collections `sites` and `community`, paging with the cursor.
- **Local file**: read `tracker.json` (create it with empty `sites` / `community` arrays if missing).

Build the set of domains and question URLs already seen.

## Step 1 — Find new sites

Target exactly `daily_sites` new qualifying sites (fewer only if you truly cannot find enough that pass every rule; never pad).

1. Process `seed_sites` first if not already in the tracker.
2. Then search with varied queries each day, combining the niche with footprints:
   `"write for us" <niche>`, `"guest post" <niche>`, `"submit an article" <niche>`, `"contribute" <niche> blog`, `"guest post guidelines" <niche>`, plus region angles from `regions`.
3. Fetch each candidate's guidelines page and confirm: free, in-niche, real editorial site, allows at least an author-bio link or one contextual link. Note word count, link policy and contact.
4. Skip domains in `skip_sites`.

## Step 2 — Authority check

For each kept site, get the Semrush Authority Score (Semrush MCP: `backlinks_research` → pick the overview report with authority score → `get_report_schema` → `execute_report` for the root domain). Respect `max_semrush_calls`. If Semrush has no data or errors, record authority as blank and continue. Below `min_authority` → status `skip`, note `low AS`, find a replacement.

## Step 3 — Pitch drafts

For each passing site with an email contact, create a Gmail draft (plain text, include signature) to that address. Follow `references/pitch-guidelines.md`. Record the subject and the draft link.

- Form-only site: method `form`, contact = form URL, full pitch text saved in notes.
- Direct contributor signup: method `direct`, signup URL in notes.

## Step 4 — Community answers

Find up to `community_answers` new, recent Quora or Reddit questions about the niche or offer. Write genuinely helpful answers (120–250 words, accurate, practical). Apply rule 8. Add the note "check subreddit rules before posting" to Reddit items.

## Step 5 — Save

Write all new site and community records to the tracker in one batch (`ArtifactData` batch, or rewrite `tracker.json`).

## Step 6 — Daily report

Produce the report in `report_language` using `references/report-format.md`. Include: a table of today's sites, the full email texts, the community answers, skipped sites with reasons, the tracker link, and any failures. If a `SendUserMessage` tool exists, send the report with it and also repeat it as the final response.
