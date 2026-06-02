# Anson

**Opinionated coworker setup for Claude Code · Slack · Notion · Gmail · Granola.**

Bootstrap a working AI coworker end-to-end, by interview.

Anson v1 wrote your identity docs. **v2 installs the whole coworker**: identity + integrations + scheduled automations + custom workflows. You talk to it once, and at the end you have a workspace you can talk to immediately.

## What you get

- **Identity** — `IDENTITY.md`, `USER.md`, `SOUL.md` built by interview, not templates: anson runs a short meta-interview to learn the *shape* of each doc, generates a dedicated maker skill with `skill-creator`, then runs that maker to do the real interview. You're left with `AGENTS.md`, `KEY_PEOPLE.md`, `MEMORY.md` **and four living maker skills** (`identity-maker`, `user-maker`, `soul-maker`, `agents-maker`) that keep those docs current as you work
- **Integrations** — Gmail, Google Calendar, Slack, Notion, Granola (macOS), iMessage (macOS) — authenticated, verified, and wired into your agent's tool surface
- **Rhythm** — morning brief, standup notes, evening wrap-up, weekly digests — whichever you ask for, scheduled and running
- **Two-way Slack coworker (optional)** — DM the agent from your phone, get replies in thread
- **Your own workflows** — describe any automation in plain English; Anson generates a skill, dry-runs it on your real data, and installs it if you approve

Opinionated by default. Every choice reflects what's actually worked in production for the founder it was built around. You can override anything later, but anson picks first so you're not making 30 micro-decisions to get to a baseline. Strangers get the same core, customized to *their* identity and workflow.

## Install

**Via Claude Code plugin (recommended)**:

```
/plugin install superpositionhq/anson-v2
```

Then in your agent:

> Run anson

**Or clone manually as a skill**:

```bash
git clone https://github.com/superpositionhq/anson-v2 ~/.claude/skills/anson-v2
# the skill lives at skills/anson/SKILL.md inside the repo;
# the plugin layout works whether cloned as a skill or installed as a plugin.
```

Then `> Run anson`.

That's it. Anson handles the rest — step by step, one question at a time, resumable if you get interrupted.

## Requirements

- **Claude Code** (primary) — Agent SDK works with reduced features
- **Strong reasoning model** (Claude Sonnet 4.6+ / Opus)
- **`anthropic-skills:skill-creator`** plugin
- **`uv`** for the Slack bridge (optional stage)
- **macOS or Linux** — iMessage + Granola are macOS-only; everything else works on both

## What the interview covers

The flow is conversational, not a checklist — but at a high level:

| Stage | What happens | What gets written |
|---|---|---|
| **A** | Anson introduces itself, picks workspace root | `<workspace>/ANSON_META.md` |
| **B** | Who are you? Meta-interview → generate a maker skill → run it, for each of identity / user / soul (before any tools) | `IDENTITY.md`, `USER.md`, `SOUL.md`, `KEY_PEOPLE.md`, `MEMORY.md` skeleton + `identity-maker`, `user-maker`, `soul-maker`, `agents-maker` skills |
| **C** | How do you work? (open-ended workflow discovery) | workflow summary in `ANSON_META.md` |
| **D** | Anson proposes the install plan based on Stage C, then executes only what your workflow needs | `.env`, verified integrations, installed skills, scheduled tasks, optional Slack bridge |
| **E** | Any custom workflows? Describe in plain English; anson generates a skill, dry-runs it, installs it | custom skills (≤5 per session) |
| **F** | Hand-off | install inventory + next steps |

Total time: ~30–45 minutes, mostly waiting on OAuth.

Identity (Stage B) comes before integrations (Stage D) so installs are tailored to your stated voice and preferences. Integrations are consequences of Stage C — if you don't use Slack, anson never asks for a Slack token.

## Resumable

If you close the terminal mid-install, Anson picks up from the last checkpoint when you say "Run anson" again. Progress is tracked in `ANSON_META.md`.

## Adding workflows later

Re-run `anson` any time. It detects the existing install, skips everything done, and jumps you straight to Stage E so you can add more automations.

## License

MIT.

## Credits

Successor to [anson v1](https://github.com/superpositionhq/anson) by Superposition. v1's generative maker-skill loop — meta-interview, generate a maker with `skill-creator`, run it, and leave the living maker skills behind — is restored as Stage B; v2 absorbs everything around it (integrations, scheduled rhythms, Slack bridge, custom workflows).
