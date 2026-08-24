# Convention: ClaudeOS ↔ Notion

The operative rules for using Notion alongside ClaudeOS. Delete this file
(and the Notion section in root `CLAUDE.md`) if you're not using Notion.

---

## The split

**Notion is the inbox. ClaudeOS is the library.**

Notion is optimized for *writing* — fast capture, mobile, daily churn,
operational tracking. ClaudeOS is optimized for *reading* — curated,
versioned, loaded into context. Connect Notion via MCP and read it live;
don't keep synced copies.

Knowledge moves **one direction only**: Notion → ClaudeOS, via a deliberate
promotion step. No two-way sync, ever. ClaudeOS does not write to Notion
unless you explicitly ask it to.

## Routing

Two questions, in order:

1. **Will this need to be true in six months?** Yes → ClaudeOS. No → Notion.
2. **Does Claude need this to reason well about the work?** Yes → ClaudeOS.

Both no → it stays in Notion, and that is a complete answer. Not everything
deserves promotion.

Where something legitimately exists in both:
**ClaudeOS holds the conclusion. Notion holds the material.**

| Artifact | Canonical | Notion's role |
|---|---|---|
| Architecture, ADRs | ClaudeOS | Pointer page + decision-log row linking to the ADR |
| Positioning, business model | ClaudeOS | Working drafts until promoted |
| Roadmap | ClaudeOS (stated direction) | Working board |
| Competitive analysis | ClaudeOS (synthesis) | Running tracker, raw intel |
| Meeting notes | Notion (raw) | ClaudeOS gets only the extracted decision |
| Tasks, journal, ideas, ops | Notion | — |

**Never duplicate ClaudeOS architecture or positioning docs into Notion.** The
moment the same fact exists in both, they diverge and neither is trustworthy.

## Conflict protocol

When ClaudeOS and Notion disagree:

1. **Never silently pick a winner.** Surface both.
2. **Cite timestamps** — `git log`/file mtime for ClaudeOS, page last-edited for Notion.
3. **Default prior:** ClaudeOS is more current for durable facts; Notion may
   predate the last promotion pass. State that assumption explicitly.
4. **Ask, then fix the loser** — correct ClaudeOS, or flag the Notion page as
   superseded with a pointer to the canonical file.

Template:

> "ClaudeOS says X (`path`, last changed 2026-06-27). Notion says Y
> ([page], last edited 2025-11-02). ClaudeOS looks newer — confirm X and I'll
> mark the Notion page superseded?"

## Notion structure rules

- Every company and product page uses the same numbered pillar pattern:
  `00 · Hub`, `01…06`, `99 · Archive` — mirroring ClaudeOS numbering makes the
  two systems navigable the same way.
- Top-level Notion items: keep it small (≤ 6-8). New ventures nest, never sit
  at top level.
- Archive, don't delete. Prefix `[ARCHIVED YYYY-MM]`.
- Title Case, no trailing punctuation. Date-prefix anything time-bound.
- Databases for anything with a status or a date; pages for anything read
  start to finish.

## Promotion workflow

Capture in Notion (no routing decisions at capture time) → weekly triage →
promote what's durable:

- decision → `<scope>/decisions/ADR-XXXX-title.md`
- research → `<scope>/research/YYYY-MM-DD-topic.md`
- meeting outcome → `<scope>/meetings/YYYY-MM-DD-topic.md`
- reusable method → `05-Evergreen/Skills|Prompts/`
- founder-level standing decision → `06-Memory/decisions-global.md`

Then `git commit`, and leave a pointer in the Notion page
(`→ promoted to ClaudeOS: <path>`) so it never gets promoted twice.

## Optional: a mobile mirror

If you use Claude on mobile without filesystem/GitHub access, one pattern is
to maintain a single generated Notion page (e.g. "ClaudeOS Context") that
mirrors your `06-Memory/` files and root `CLAUDE.md`, so Claude on mobile has
*something* to read. If you do this:

- It's the **only** permitted duplication of ClaudeOS content into Notion.
- One-directional: ClaudeOS → Notion. Never edit the Notion page directly —
  edit the source `.md` files and regenerate.
- On conflict, ClaudeOS wins — the mirror may be stale.
- Track which files should trigger a regeneration prompt in
  `06-Memory/notion-map.md` (see that file for the pattern).

This is optional — plenty of setups skip it entirely and just accept that
mobile sessions are Notion-only or ClaudeOS-only, not both.

## Search before answering "I don't know"

**Standing rule worth adopting:** for any factual question about you, your
company, or your work, search before concluding the answer doesn't exist.
Order: any mobile mirror → Notion workspace → ClaudeOS repo (desktop only).
If it really isn't there, say where you looked. This one rule prevents a lot
of "I don't have that on file" answers when the data was one MCP call away.

## Sensitive content — read this before connecting Notion

Notion workspaces often hold things that should never be read into a chat
session or copied into a git repo: credentials, API keys, legal/financial
identifiers, anything a plaintext database property might be hiding. Before
connecting Notion via MCP:

- Identify any pages/databases that store secrets in plaintext and explicitly
  tell Claude (in this file, or in `CLAUDE.md`) not to read, quote, or copy
  their contents.
- Never let a promotion step copy raw Notion content into a public or
  shared ClaudeOS repo without a human review pass.
