# Config template

Copy this into your project instructions, a `config.md` next to the skill, or the scheduled-task prompt, and fill it in.

```yaml
target_url: https://your-site.com/your-page/    # <-- YOUR page: the ONLY link to promote
company: Example Ltd
offer_summary: >
  One or two factual sentences about what the page offers
  (course, product, service), price if relevant, audience.
sender_name: Your Name
sender_role: Your Role, Example Ltd
gmail_account: you@example.com                  # connected Gmail used for drafts
niche: your main niche                            # e.g. personal finance, SaaS marketing
related_niches: [related topic 1, related topic 2]
regions: [UK, US]                                # optional search angles
tracker: artifact:https://claude.ai/artifact/XXXX  # or: file:tracker.json

daily_sites: 5
min_authority: 15
max_semrush_calls: 10
community_answers: 3
report_language: English                         # e.g. English, Hinglish, Urdu, Spanish

seed_sites:                                      # optional, processed first
  - domain.com (contact@domain.com, 800+ words)
skip_sites:                                      # optional, known bad fits
  - example-paid-site.com (paid links only)
forbidden_names: []                              # names never to use in any output

pitch_ideas:                                     # optional article angles
  - An article angle that fits your page
  - Another angle
```
