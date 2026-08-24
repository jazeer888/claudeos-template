# Playbook: Research → Capture Workflow

How to actually work with ClaudeOS day to day, using a worked example:
researching a competitor for "YourProduct." This is the pattern to reuse for
any research/analysis task across any company or product — swap in your own
scope name.

---

## The general pattern (4 steps)

**1. Orient** — tell Claude the scope, don't make it guess. Name the
product/company so it reads the right `CLAUDE.md` and existing files before
starting, instead of researching cold or duplicating work that already exists.

**2. Work** — Claude does the research/analysis in the session (web search,
file reads, whatever the task needs).

**3. Capture** — decide *where the output lives* using the filing rule below.
Most findings are a file, not a memory edit.

**4. Commit** — git commit at the end of the session. This is the actual
"save to long-term memory" step — everything else is just a file on disk
until it's committed.

You almost never need to manually "open a folder" first. With the repo
connected (Cowork folder, or `cd` + `claude` in Claude Code), Claude can
navigate to the right place itself — your job is to say enough for it to
scope correctly.

---

## Worked example: researching a new competitor for YourProduct

**You type, in chat:**

> "New competitor for YourProduct — [CompetitorName], here's their
> GitHub/site: [link]. Do a competitive analysis and tell me how they compare
> on [the dimension that actually matters for your positioning]."

**What should happen, and why:**

| Step | What Claude does | Why |
|---|---|---|
| Orient | Reads `01-Companies/YourCompany/products/YourProduct/CLAUDE.md`, then the existing files in `research/` | Won't re-derive your positioning from scratch, won't contradict existing conclusions, can slot the new competitor into the existing comparison format |
| Work | Web search, repo/site metrics, whatever the analysis needs — same rigor as prior entries | Keeps every competitor entry in the knowledge base comparable, not a one-off format |
| Capture | See filing rule below | Determines whether this is a new file or an edit to an existing one |
| Commit | `git commit` at end of session | Locks it into versioned history |

**If you don't name the product**, Claude has to infer scope from context or
ask — for a one-line request like the example above, naming it costs you
three words and saves a clarifying question.

---

## Filing rule: where does the output actually go?

This is the part people get wrong — not every finding is worth a `CLAUDE.md`
edit, and not every finding needs a new file.

**Does it change how you'd explain YourProduct's competitive position to
someone in one sentence?**

- **No, it's incremental** (a new competitor that doesn't change the threat
  ranking) → new dated file in `research/`, using
  `05-Evergreen/Templates/template-research-note.md`. Example:
  `research/2026-08-15-competitor-agentkey.md`. The master doc and
  `CLAUDE.md` stay untouched.
- **Yes, it changes the picture** (new competitor jumps to "High" threat, or
  invalidates a claim in the existing analysis) → update the master doc's
  executive summary and comparison table directly, *and* update the
  one-line competitive summary in `products/YourProduct/CLAUDE.md` so anyone
  opening that file gets the current picture without reading every research
  file.

**Never** put raw research findings directly into `CLAUDE.md` — it's a
navigation/summary layer, not a notebook. `CLAUDE.md` gets a sentence; the
research folder gets the depth.

**Never** create a research file with an ambiguous name like `notes.md` or
`competitor-research.md` when one already exists — that's how you end up with
three overlapping competitive-analysis files a year from now. Check
`research/` first, extend what's there.

---

## What "saving to memory" actually means here

There is no separate "memory" step for routine work. Three tiers, in order of
how often you'll actually use them:

1. **The research file itself** — this *is* the memory for this finding.
   It's what Claude reads next time this comes up. This is where ~95% of
   research ends up.
2. **`products/YourProduct/CLAUDE.md`** — only touched if the finding changes
   the one-sentence summary of where the product stands. Most individual
   findings don't warrant this.
3. **`06-Memory/decisions-global.md`** — only for a standing decision at the
   founder/individual level (e.g., "deprioritizing segment X because of
   competitor Y"), not a research finding. Touch this rarely — if you're
   editing it weekly, something's mis-scoped.

If you're unsure which tier, default to tier 1. It's easy to promote a
finding to tier 2 later; it's costly to have bloated `CLAUDE.md` files you
have to prune.

---

## Best practices

Name the product or company at the start of a task, every time — "for
YourProduct," "for the day job," "personal" — even when it feels obvious.
This is the single highest-leverage habit for keeping ClaudeOS usable: it's
what lets Claude load the right 200 lines of context instead of the wrong
ones or none at all.

Point Claude at the existing file when one plausibly exists, rather than
letting it decide fresh — "check `research/` first" costs nothing and
prevents duplicate/competing files.

Do a real git commit at the end of every working session, not just when you
remember. A commit message that names what changed ("add AgentKey competitor
analysis") is what makes `git log` a usable second timeline of decisions
later — treat it the same way you'd treat writing a commit message for code.

Batch related findings into one commit. If you research three competitors in
one sitting, that's one commit with three files, not three commits — easier
to review a year from now.

Reread each product's `CLAUDE.md` yourself once a month. If it doesn't match
what you'd actually say about its status right now, that's the signal to
update it — not a fixed schedule.

## Common mistakes to avoid

Dumping a long research answer into chat and never saving it — if it's worth
asking, it's worth a file; ask Claude to save it before you close the session.

Creating a new file when an existing one already covers the topic — check
`research/` (or whichever folder) before generating output, not after.

Editing `CLAUDE.md` for every finding — this is the fastest way to blow past
the 150–200 line budget and have Claude start skimming it.

Skipping the git commit — an uncommitted file is one accidental overwrite
away from being gone, and you lose the dated history that makes "why did we
conclude X" answerable later.

## Applying this pattern elsewhere

Same 4 steps for any task type — only the filing rule changes:

- **Meeting notes** → always a new dated file in `<scope>/meetings/`, never
  an edit to an existing one (meetings are point-in-time by nature). Use
  `05-Evergreen/Templates/template-meeting-note.md`.
- **Architecture decisions** → new `ADR-000X-title.md` in `<scope>/decisions/`,
  numbered sequentially. Use `05-Evergreen/Templates/template-adr.md`. Update
  `CLAUDE.md`'s architecture summary only if the decision changes the current
  design, same rule as above.
- **Product requirements** → edit the existing PRD in `<product>/product/` in
  place (PRDs are living documents, not point-in-time like meetings) — use
  git history for the "what changed" trail instead of dated file forks.
- **GTM/positioning work** → same as research: incremental update goes into
  the existing `gtm/positioning.md` in place if it's a refinement, or a new
  dated file if it's a distinct campaign/analysis that shouldn't overwrite the
  standing positioning doc.
