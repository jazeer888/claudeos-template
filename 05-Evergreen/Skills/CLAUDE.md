# Skills — Index & Registry

Reusable Claude Skills, organized by domain. One entry per skill with a
one-line description and trigger condition. Use this file to find the right
skill when starting a thread, and keep it updated when you add/download new
skills.

## Skills Index

- example-skill/ — replace this with your own skills as you build them

## How to add a new skill

**When you build a new skill:**
1. Use the `skill-creator` tool, or build manually in `<skill-name>/SKILL.md`
2. Add one line here: `- <skill-name>/ — <one-line description>`
3. Commit to git: `git add . && git commit -m "Add <skill-name> skill"`

**When you download a skill:**
1. Extract the `.skill` zip: `unzip <skill-name>.skill`
2. Move to this folder: `mv <skill-name> 05-Evergreen/Skills/`
3. Add one line here with source: `- <skill-name>/ — <description> (downloaded from [source], v1.0)`
4. Commit to git

## Example edits

**Adding a new skill you built:**
```markdown
# Before
- example-skill/ — replace this with your own skills as you build them

# After
- example-skill/ — replace this with your own skills as you build them
- terraform-azure/ — Terraform + Azure patterns, best practices, cost optimization
```

## Notes

- Keep the list alphabetical or grouped by domain for readability
- If a skill becomes obsolete, move it to `99-Archive/Skills/` instead of deleting
- Link to source for downloaded skills (marketplace, GitHub, etc.)
- Update this file **before** committing the skill itself
