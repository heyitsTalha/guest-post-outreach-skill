# Tracker schema

The tracker is the shared memory between daily runs. Read it first, write to it last.

## Collection `sites`

One record per domain. `id` = domain with dots replaced by `-` (e.g. `example-blog-com`).

| Field | Type | Notes |
|---|---|---|
| domain | string | root domain |
| url | string | write-for-us / guidelines page |
| niche | string | short label |
| authority | number or "" | Semrush Authority Score |
| method | "email" \| "form" \| "direct" | how to pitch |
| contact | string | email address or form URL |
| subject | string | email subject, or "" |
| pitchTopic | string | one line |
| draftLink | string | Gmail draft link, or "" |
| status | "drafted" \| "skip" \| "sent" \| "accepted" \| "published" \| "rejected" | agent only writes drafted / skip |
| foundOn | YYYY-MM-DD | |
| notes | string | link policy, word count, skip reason, form pitch text |

## Collection `community`

`id` = platform + short slug (e.g. `quora-best-crm-small-business`).

| Field | Type | Notes |
|---|---|---|
| platform | "Quora" \| "Reddit" | |
| question | string | |
| url | string | |
| answer | string | plain text, ready to paste |
| status | "to-post" \| "posted" | agent only writes to-post |
| foundOn | YYYY-MM-DD | |
| notes | string | e.g. "check subreddit rules before posting" |

## Local file format (`tracker.json`)

```json
{
  "sites": [ { "id": "example-com", "domain": "example.com", "status": "drafted" } ],
  "community": []
}
```
