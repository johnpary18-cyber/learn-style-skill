# learn-style configuration (example)

Copy this file to `config.md` in the same folder and fill in the values you want.
Every field is optional — leave a field blank to use the skill's fallback behavior.
`config.md` is git-ignored so your personal paths and setup never get committed.

```yaml
# A slash command / skill this skill can invoke to gather recent, trending, or
# real-time information (used for the "recent topic" path). This is where you plug
# in your OWN research tool — e.g. a skill backed by the ScrapeCreators API, a
# social-trends search, a web-search skill, etc. Leave blank to fall back to
# standard web research that favors sources from the last ~30 days.
recent_research_command: ""      # e.g. "/last30days" or "/my-trend-search"

# Absolute path to the folder or note vault where summary notes are saved.
# Leave blank to be asked at save time (or to save into ./learn-style-notes/).
notes_path: ""                   # e.g. "/Users/you/Documents/My Vault"

# Optional: a rules/README file for your notes system that the skill should read
# and obey before writing a note (folder taxonomy, frontmatter standard, linking
# conventions). Great for Obsidian vaults with a CLAUDE.md. Leave blank to use
# the skill's default note format.
notes_rules_file: ""             # e.g. "/Users/you/Documents/My Vault/CLAUDE.md"

# Optional: a subfolder inside notes_path to save into (e.g. "Reference Notes").
notes_subfolder: ""
```
