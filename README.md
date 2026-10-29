# Conversation Design Playbook

An agent-era playbook for teams building LLM-powered shopping or advice assistants: chatbots and agents that help someone choose a product, get advice, or complete a task through conversation.

## What this is

Most conversation-design advice was written for an older generation of chatbots: hand-scripted dialog trees, slot-filling intake forms, strict intent classifiers. Large language models changed the job. You no longer write the exact words an assistant says — you design the conditions it operates under: what it's grounded on, what it's allowed to do, how it asks and recommends, how it fails, and how you keep testing it. That's the agent era, and most of the available writing on conversation design hasn't caught up.

This playbook collects what's genuinely still true from the older craft, what's new and specific to LLM agents, and where the two give opposite advice. It's organized in three layers:

- **`principles/`** — one file per topic (question design, recommendation design, failure recovery, trust, testing, agent boundaries, and more). Each principle is tagged by era — whether it's a timeless piece of craft, something that only makes sense now that the assistant is a language model, or something from the old slot-filling world that doesn't transfer and should be dropped. Each one also carries the reasoning behind it, not just the rule, plus the exceptions and inversions that make it usable in practice instead of a slogan.
- **`skills/`** — eight runnable playbooks for Claude Code (or any agentic coding assistant) that turn the principles into a repeatable process: scoping an agent's remit, designing a conversation flow, grounding it on a knowledge base, writing its failure and escalation behavior, setting its trust and disclosure policy, building its eval suite, critiquing a prototype, and running the improvement loop once it's live.
- **`SOURCES.md`** — every public talk that fed into this, with a link and a short note on what it contributed, organized by theme.

## How it was made

This was synthesized from public conversation-design talks and public guidance from major AI labs on building reliable agents — not from any single vendor's proprietary framework. Every principle is era-tagged (does this apply to the old intent-based chatbot world, the new LLM-agent world, or both), and every non-obvious claim traces back to a real talk, listed in `SOURCES.md`. Nothing here reproduces a talk's content wholesale; it's a synthesis, in our own words, credited to its sources.

Where the source material leaned on examples from a specific company or industry, this playbook generalizes them — the principles apply to any team building a conversational shopping or advice assistant, not to one vertical.

## How to use it with Claude Code

Each file in `skills/` is a standard Claude Code skill: drop the `skills/` directory into a project's `.claude/skills/` folder (or point Claude Code at this repo) and the skills become invocable by name — e.g. "use conversation-architect to design the return flow" or "run eval-designer against this feature." They're meant to be used together and in sequence: scope the agent first, design the conversation inside that scope, ground it on real content, write its failure behavior and trust policy, build the eval suite, critique the result, then run the live improvement loop. Each skill's "when to use / when not to use" section tells you which sibling skill owns the adjacent work.

You don't need Claude Code to get value from this — the `principles/` files stand alone as a reference for any team's conversation design, review, or eval work.

## License

MIT. See `LICENSE`.
