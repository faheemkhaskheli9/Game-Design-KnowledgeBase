# Instructions for AI agents (Claude Code, Codex, Cursor, Copilot, ...)

This repo is a reference knowledge base on game design and gameplay: what
makes games fun, core loops, difficulty and flow, player motivation,
mechanics and balance, progression and rewards, economies, game feel,
onboarding, level design, narrative, retention, playtesting and prototyping.

## Consulting it

1. Read `INDEX.md` (one section per category). Match your task against the
   **Tags** and **Use when** columns. `llms.txt` is a shorter one-line-per-topic
   list; `glossary.md` maps terms to the topic that explains each.
2. For "my game is boring / too hard / players quit / what should I add" start
   at `scenarios/scenario-chooser.md`, which maps symptoms to topics. To review
   a design or feature, use `scenarios/design-review-checklist.md`.
3. Read the **full** matched file(s), not just the index row. Follow `[[links]]`
   in the `## Related` section when they apply.
4. Adapt the guidance to the game's genre, audience and platform; principles
   from one genre do not transfer blindly (a roguelike wants run variance a
   competitive shooter must avoid).
5. Mention which file(s) informed your work.

Quick search without reading the index: `grep -ril "<keyword>" --include=*.md .`

## Which knowledge base answers what

| Question | Go to |
|---|---|
| Fun, loops, balance, progression, rewards, game feel, onboarding, levels, narrative, playtesting | this base |
| Server architecture, netcode infra, databases, APIs, scaling | `E:\Projects\Software-Engineering-KnowledgeBase` |
| AI models for NPCs, procedural content with LLMs, ML | `E:\Projects\AI Knowledge Base` |

## Adding or editing a topic

1. Copy `_template.md` into the right category folder. One topic per file,
   kebab-case filename.
2. Fill in every section. Prefer worked examples from real games; code (Python)
   only where math helps (curves, drop tables, balance).
3. Cite sources (books, GDC talks, papers, designer articles). Set
   `last_verified` to today. Do not invent statistics; leave them out instead.
4. Link a new topic from at least one existing topic's `## Related` and, if it
   answers a symptom, from `scenarios/scenario-chooser.md`.
5. Run `python build_index.py` (stdlib only) and commit `INDEX.md`/`llms.txt`.
   It fails on invalid frontmatter (`category` must match the folder, `status`
   one of draft/stable/needs-review, `last_verified` YYYY-MM-DD, non-empty
   `sources`/`use_cases`), missing or thin template sections, and broken
   `[[links]]` or relative Markdown links; it warns on orphans and on topics
   not re-verified within 365 days.
6. New terms go in `glossary.md` as `- **Term** - definition. [[topic]]`.
7. LF line endings, UTF-8.
