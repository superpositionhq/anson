# Agents Maker — Creator Instructions

These instructions guide the skill-creator in building the agents-maker skill.

## Purpose

The agents-maker creates or updates the agent instructions file with lifecycle logic that tells the agent when and how to use the maker skills in update mode.

In anson-v2 the canonical agent instructions file is **`AGENTS.md`** at the workspace root (`CLAUDE.md` is a thin pointer that `@`-includes it). The agents-maker writes the lifecycle block into `AGENTS.md`. The exact path comes from `ANSON_META.md`.

## What makes a good agents-maker

Unlike the other maker skills, agents-maker is more mechanical than conversational. No user interview is needed. Its job is to:

- Read the existing agent instructions file (if any)
- Add lifecycle instructions for the maker skills without disrupting existing content
- Define when each maker skill should run in update mode
- Be precise about trigger conditions and judgment criteria

## Key instructions to add

The agents-maker must ensure the agent instructions file contains:

1. That identity-maker, user-maker, and soul-maker are living maintenance skills
2. That they should be used proactively in Update mode when durable insights emerge
3. Judgment criteria: prefer small updates, only when durable, preserve continuity
4. The three-question test: Is this stable? Does it belong? Would updating improve future behavior?

## Key considerations for the skill-creator

When building this skill:

- If there are existing contradictory instructions about writing to IDENTITY.md, USER.md, or SOUL.md, overwrite those sections only
- Do not otherwise overwrite existing agent instructions — only append. In anson-v2, `AGENTS.md` already carries identity `@`-includes and integration/credential sections by the time agents-maker runs; preserve all of it
- Handle the case where no agent instructions file exists yet (create from scratch)
- The skill should be idempotent — running it twice should not duplicate instructions
- In update mode, the agents-maker should be able to add new lifecycle rules or refine existing ones
- The agent instructions file path comes from ANSON_META.md
