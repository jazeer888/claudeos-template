# ClaudeOS

A git-backed, Claude-native knowledge base template — the structure for a
single source of truth that centralizes your product strategy, technical
architecture, research, GTM, career context, and reusable Skills, so Claude
has real context instead of starting cold every session.

**Fork it, rename the example folders, and it's yours.**

---

## Why this exists

Most people running serious work through Claude end up with context
scattered across Notion docs, half-written wikis, Claude Projects, and Slack
threads — so every new session starts with re-explaining the same background.
ClaudeOS fixes that by keeping durable knowledge as versioned markdown in one
git repo that Claude reads directly: no re-pasting context, no drift between
sources, and a `git log` that doubles as a decision history.

**The gain, concretely:** local, git-versioned memory that Claude reads
automatically, wired up to Notion for fast capture and (optionally) Obsidian
for visual review, turns "explain my situation again" into "for X, do Y" —
for founders juggling multiple ventures or engineers running long-lived
projects, that compounding-context effect is where the 5-10x productivity
gain actually comes from, not from any single feature.

---

## Who this is for

- **Entrepreneurs / founders** — one place for company strategy, GTM, and
  investor context across every venture you're running
- **DevOps / platform engineers** — architecture decisions, runbooks, and
  infra patterns that survive past the Slack thread they were decided in
- **Developers** — a Claude Code-native project memory that isn't tied to any
  single codebase
- **Anyone else working seriously with Claude** — the pattern (structured
  markdown + `CLAUDE.md` navigation files + git) works for any domain where
  you want Claude to remember your context without you re-explaining it

---

## What's inside

```
ClaudeOS/
├── 00-System/           # Meta: conventions, index, playbooks
├── 01-Companies/        # Every company/product you own (example: YourCompany)
├── 02-Career/           # Full-time role, projects, skills inventory
├── 03-StartupIdeas/     # Pre-venture exploration
├── 04-Personal/         # Personal life, separate from work
├── 05-Evergreen/        # Reusable Skills, prompts, templates, patterns
├── 06-Memory/           # Stable identity, preferences, standing decisions
└── 99-Archive/          # Retired projects, decision history
```

**Key principle:** every company, product, and scope follows the same
internal structure:

```
<scope>/
├── CLAUDE.md            # Navigation file, quick context
├── product/             # PRDs, roadmaps, requirements
├── architecture/        # System design, ADRs, technical decisions
├── research/            # Competitive analysis, market research
├── gtm/                 # Positioning, messaging, launch strategy
├── meetings/            # Dated meeting notes
├── decisions/           # ADRs and decision logs
└── engineering/         # Infrastructure notes, runbooks (for products)
```

Same mental model everywhere — Claude learns the pattern once and applies it
to every scope you add.

---

## How it works with Claude

**You:** "For YourProduct, research a new competitor"

**Behind the scenes:**
1. Claude reads `01-Companies/YourCompany/products/YourProduct/CLAUDE.md`
2. Loads the competitive analysis from `research/`
3. Checks the positioning framework from `gtm/positioning.md`
4. Answers with real context — no copy-pasting, no re-explaining

**Filing new work follows the same pattern:** scope → type → file. A research
finding goes in `<scope>/research/YYYY-MM-DD-topic.md`; a decision becomes an
`ADR-000X-title.md`; a meeting note is always a new dated file. See
`00-System/playbooks/research-and-capture-workflow.md` for the full pattern.

---

## Getting started

1. **Use this template** (GitHub → "Use this template", or clone/fork it)
2. **Rename the examples** — `01-Companies/YourCompany` and
   `.../YourProduct` become your real company/product names; delete what you
   don't need
3. **Fill in `06-Memory/identity.md` and `preferences.md`** — this is what
   makes Claude's output feel tailored to you instead of generic
4. **Connect it to Claude:**
   - **Cowork (Claude desktop app):** use the folder picker to connect your
     ClaudeOS folder, then start a thread with "For YourProduct, [task]"
   - **Claude Code (CLI):** `cd` into any subfolder and run `claude` — it
     loads `CLAUDE.md` and nested files automatically
5. **Work, then commit:** `git add -A && git commit -m "..."` at the end of
   every session — this is the actual "save to memory" step

---

## Notion integration

ClaudeOS treats Notion as the **inbox** and the repo as the **library**:
Notion is for fast capture (mobile, daily churn, task tracking); ClaudeOS is
for durable, versioned, Claude-readable knowledge. Connect Notion via MCP and
Claude reads it live — nothing gets synced or duplicated by default.

**Setup:** add the Notion MCP connector in Claude (Settings → Connectors, or
`claude mcp add notion` in Claude Code), then fill in
`06-Memory/notion-map.md` with where things live in *your* workspace.

**The routing rule:** "Will this need to be true in six months, and does
Claude need it to reason well?" → promote it from Notion into the repo as a
dated file. Everything else stays in Notion. Full rules, conflict handling,
and the promotion workflow: `00-System/conventions/notion-integration.md`.

Not using Notion? Delete that file and the Notion section in root
`CLAUDE.md` — nothing else depends on it.

---

## Obsidian (optional)

ClaudeOS is plain markdown in plain folders, so it opens as an Obsidian vault
with zero setup — point Obsidian at the repo root and you get graph view,
backlinks, and visual browsing of the same files Claude reads. Handy for
reviewing how your companies/products/decisions connect at a glance, on top
of the git history Claude already gives you.

---

## Best practices

1. **Name your scope at the start of every thread** — "For YourProduct,"
   "For Career" — costs three words, saves Claude from guessing
2. **Keep `CLAUDE.md` files as navigation layers, not knowledge dumps** — one
   sentence per fact, link to the file for depth
3. **File research, decisions, and notes by scope and type** — not one big
   `Notes/` folder
4. **Commit after every working session** — makes `git log` a useful timeline
5. **Archive, don't delete** — dead projects have value as decision history

---

## Extending ClaudeOS

**Add a new company:**
```bash
mkdir -p 01-Companies/<NewCompany>/{company,strategy,research,meetings,decisions,products}
cp 01-Companies/YourCompany/CLAUDE.md 01-Companies/<NewCompany>/
# Edit CLAUDE.md with the new company's context
git add . && git commit -m "Add <NewCompany> to companies"
```

**Add a new product under a company:**
```bash
mkdir -p 01-Companies/<Company>/products/<NewProduct>/{product,architecture,research,gtm,meetings,decisions,engineering}
cp 01-Companies/YourCompany/products/YourProduct/CLAUDE.md 01-Companies/<Company>/products/<NewProduct>/
git add . && git commit -m "Add <NewProduct> to <Company>"
```

**Add a new Skill:**
```bash
mkdir -p 05-Evergreen/Skills/<skill-name>
# Create SKILL.md, update 05-Evergreen/Skills/CLAUDE.md registry
git add . && git commit -m "Add <skill-name> skill"
```

---

## FAQ

**Do I need to put everything in ClaudeOS?**
No. Code repos, video projects, and tools have their own homes. ClaudeOS is
knowledge and decisions — what Claude needs to reason about your work.

**Should I sync ClaudeOS with Notion?**
No — one-directional promotion, not sync. Notion for fast capture, ClaudeOS
for durability and Claude-readability. See the Notion section above.

**Can I use this without Notion or Obsidian?**
Yes, both are fully optional. The core of ClaudeOS is just structured
markdown + git + Claude reading `CLAUDE.md` files — everything else is an
add-on.

**How do I keep this private if I fork it for real use?**
Fork or clone it, then keep your working copy in a **private** repo — this
template being public doesn't mean your filled-in version has to be. That's
exactly what the original version of this repo is (private, real data);
this template is the sanitized structure only.

---

## License

MIT — see [LICENSE](LICENSE). Use it, fork it, change it, ship your own
version.

---

**Created by:** Jazeer ([@jazeer888](https://github.com/jazeer888)) — built and open-sourced from a real, in-daily-use
setup. If you improve the structure or the playbooks, PRs are welcome (see
[CONTRIBUTING.md](CONTRIBUTING.md)) — this stays a template for the *system*,
never a place for anyone's real data.
