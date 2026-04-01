# Anson

A bootstrap-orchestrator skill for making a personal AI assistant richer, more personal, and more self-aware.

## The problem

Bootstrapping a personal AI assistant is a paradox. How do you get a rich identity before the agent has a soul? How can it ask meaningful questions about who you are before it has a real personality? The agent needs to know you to ask good questions, but it needs to ask good questions to know you.

Most setups punt on this. OpenClaw's `BOOTSTRAP.md` is thin — a few prompts, and then it's up to you to proactively define `IDENTITY.md`, `USER.md`, and `SOUL.md`. The result is usually sparse documents that don't capture what actually matters.

## What Anson does

Anson is a wizard that resolves the bootstrap paradox through progressive interviews. It:

1. **Scans your workspace** for existing context — if you've been working with your agent already, Anson won't re-ask what it can infer
2. **Conducts meta interviews** — short conversations to figure out what the right questions are for *you specifically*, before asking them
3. **Generates bespoke maker skills** — `identity-maker`, `user-maker`, `soul-maker` — tailored to your answers, not generic templates
4. **Runs those skills** to create rich, personalized `IDENTITY.md`, `USER.md`, and `SOUL.md`
5. **Installs lifecycle rules** so the documents stay alive — the maker skills run proactively in update mode as the agent learns more over time

The result: an agent that knows who it is, knows who you are, and has a defined relationship with you — maintained by permanent infrastructure, not a one-shot script.

## Agent-agnostic

Anson has defaults for OpenClaw but works in any environment where an agent has a writable workspace. Claude Code, or any repo where you're running an AI assistant — it detects the environment and adapts.

## Why "Anson"

Named after Anson MacDonald — the pen name Robert A. Heinlein used to publish *By His Bootstraps* (1941), the novella that defined the bootstrap paradox in fiction. A character caught in a causal loop with no external origin, becoming the person who set the whole thing in motion. Felt right.

## Usage

Install the skill into your project's `skills/` directory and invoke it. Anson will guide you through the rest.

## License

MIT
