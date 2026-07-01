# learn-style

A Claude Code / Agent Skill that teaches you any concept the way you learn best.

It interviews you about how fresh, how applied, and how deep you want to go — then
researches the topic and teaches it in layers:

**Overview → Zoom In → ELI5 → Zoom Out → Videos → active-recall check → optional saved note**

It finishes with a "Check for Understanding" quiz (one question at a time, with
targeted re-teaching when you miss one) and can save a clean summary note to your
own notes system.

## Install

Copy the skill folder into your agent's skills directory. For Claude Code:

```
~/.claude/skills/learn-style/
├── SKILL.md
├── config.example.md
└── README.md
```

Then restart your session so the skill is registered. Invoke it with `/learn-style`.

> Skill folders are discovered by the presence of `SKILL.md`. The folder name and
> the `name:` field in `SKILL.md` should match (`learn-style`).

## Configure (optional)

Everything works out of the box with sensible fallbacks. To make it yours, copy
`config.example.md` to `config.md` and fill in any of these:

| Field | What it does | Fallback if blank |
|---|---|---|
| `recent_research_command` | A command/skill to pull recent/trending info for fast-moving topics. **Plug in your own** — e.g. a ScrapeCreators-backed trend search or any web-search skill. | Standard web research prioritizing the last ~30 days |
| `notes_path` | Where summary notes are saved | Asks you, or saves to `./learn-style-notes/` |
| `notes_rules_file` | A rules/README the skill reads before writing a note (e.g. an Obsidian vault `CLAUDE.md`) | Uses a simple default note format |
| `notes_subfolder` | Subfolder inside `notes_path` | Saves at the vault root |

### Bring your own recent-research tool

The "recent topic" path is designed to be pluggable. Point `recent_research_command`
at any skill/command you already have that returns fresh information — social scraping
(ScrapeCreators, etc.), a web-search skill, or your own custom research routine. This
repo intentionally ships **no** API keys and **no** bundled research provider.

### Bring your own notes system

Set `notes_path` to your Obsidian vault (or any folder). If your vault has a rules
file describing its structure and frontmatter, point `notes_rules_file` at it and the
skill will follow those conventions when it writes the summary.

## Privacy

- `config.md` is git-ignored — your paths and tool names stay local.
- The skill ships no secrets. Keep any API keys in your own tool's config/`.env`,
  never in this repo.

## License

MIT
