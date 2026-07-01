---
name: learn-style
description: Researches and teaches any concept you ask about, in a structured learn-by-layers format (Overview → Zoom In → ELI5 → Zoom Out → Videos → active recall), then optionally saves a summary note to your knowledge base. Use when prompted with the /learn-style command.
---

# learn-style

A guided teaching loop. It interviews you about *how* you want to learn a topic,
researches it, teaches it in layers, checks your understanding, and can save a
summary note to your notes/knowledge base.

## Configuration (read this first)

Before running, read `config.md` in this skill's folder if it exists. It defines
optional, user-supplied integrations. **Every field is optional** — the skill
works with sensible fallbacks when a field is blank or `config.md` is missing.

Config fields:
- `recent_research_command` — a slash command or skill this skill can invoke to
  pull recent/trending information (e.g. your own social/web trend-search skill,
  a ScrapeCreators-backed tool, etc.). Used for the "new topic" path below.
- `notes_path` — absolute path to the folder/vault where summary notes are saved.
- `notes_rules_file` — optional path to a rules/README file for your notes system
  (e.g. an Obsidian vault `CLAUDE.md`) that this skill should read and obey before
  writing a note.
- `notes_subfolder` — optional subfolder inside `notes_path` to save into.

Never invent values for these. If a field is blank, use the stated fallback.

---

When using learn-style, go through the following process.

## Inquiry 1 — How fresh does the research need to be?
Prompt the user with a two-option question.

1. **This is a fast-moving / recent topic**
   Description: Learning this well needs current information (recent releases,
   news, trends, community discussion).

   If chosen and `recent_research_command` is configured, invoke that command to
   gather recent information for the topic.
   If it is **not** configured, fall back to standard web research that explicitly
   prioritizes sources from roughly the last 30 days, and tell the user you used
   the fallback (they can wire up `recent_research_command` for better freshness).

2. **This is a stable / evergreen topic**
   Description: Foundational or slow-changing — recent-trend research isn't needed.

   If chosen, do normal research pulling from credible sources and citing them
   with links only.

## Inquiry 2 — Is this tied to a project?

1. **This learning is for a project**
   Description: Tie the learning to real use in a specific project. Ask the user
   to paste project context, and weave that context through the teaching.

2. **General learning, no specific project**
   Description: No project tie-in needed. Use the normal format.

## Inquiry 3 — How deep?
Ask if they want to become an expert or just gain general knowledge.

1. **Expert**
   Description: Provide deep insights and guidance for deep technical understanding.

2. **General Knowledge**
   Description: Provide enough that if someone asked them what this was, they could
   explain it briefly and speak to how it works.

---

After the inquiries are done, teach the topic in this format:

## Overview
Briefly describe, within 4 sentences, what we are learning.

## Zoom In
A zoomed-in focus describing what specifically we're talking about, in no more
than two paragraphs.

## ELI5
An example a 5-year-old could understand for what we're talking about.

## Zoom Out
Current real-world applications of the topic — give 3 examples, no more than a
paragraph each.

## Videos
Suggest 3 videos (YouTube, X, or TikTok) the user could watch to deepen
understanding. Rate the credibility of each source 1–10 and provide the links.
Only include links you are confident exist; do not fabricate URLs.

## Check For Understanding
Ask the user 3 questions relevant to the topic, **one at a time**, to see if they
understand. If they get one wrong, ask what's confusing and teach them what
they're missing before moving on.

## Any Further Questions
Ask if there are more questions. Be honest about whether you have a clear enough
answer; if not, research again based on their question. Tell them to type "done"
when finished.

## Save a Summary
Ask the user whether they'd like to save a summary note.

If yes:
- **Where:** Save to `notes_path` (and `notes_subfolder` if set). If `notes_path`
  is not configured, ask the user for a path, or offer to save a
  `learn-style-notes/` folder in the current working directory.
- **Rules:** If `notes_rules_file` is configured, read it first and follow its
  conventions (folder taxonomy, frontmatter, linking) exactly. Otherwise use the
  default note format below.
- **Filename:** A clear, descriptive title of the topic (e.g.
  `Retrieval-Augmented Generation.md`). Never overwrite an existing note — if one
  exists, add new nuance to it or link to it instead.
- **Default frontmatter** (used only when no `notes_rules_file` dictates otherwise):
  ```yaml
  ---
  date: YYYY-MM-DD
  tags: [learn-style]
  source: "learn-style session"
  ---
  ```
- **Body:** Include the full teaching content (Overview → Zoom In → ELI5 →
  Zoom Out → Videos), then a `## Check for Understanding` section capturing the 3
  questions and the user's answers. If tied to a project, add a `## Project Context`
  section.

After saving, show a summary of the file created and any notes changed.
