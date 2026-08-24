# Notion Map

Where things live in your Notion workspace — so Claude can go straight to the
right page/database instead of searching blind, and so you have one place
that documents the routing. Delete this file if you're not using Notion.

**Do not put real Notion page/database IDs, credentials, or anything
sensitive into this file if the repo is public.** For a public or shared
ClaudeOS, either keep this file local-only (add it to `.gitignore`) or keep
it to page *names*/*purposes* without IDs and rely on Notion search.

## Template

| Area | Notion location | Notes |
|---|---|---|
| Company hub | `<page name>` | e.g. top-level company workspace page |
| Tasks / to-dos | `<database name>` | operational, not promoted to ClaudeOS |
| Journal | `<database name>` | personal, daily |
| Raw meeting notes | `<database name>` | promoted decisions go to `<scope>/meetings/` |
| Research inbox | `<database name>` | promoted findings go to `<scope>/research/` |

## Sensitive pages — do not read into chat or copy to disk

List anything in your workspace that stores secrets/credentials/legal IDs in
plaintext properties, so Claude knows to skip it even if search surfaces it.

- `<page/database name>` — reason (e.g. "stores API keys in plaintext")
