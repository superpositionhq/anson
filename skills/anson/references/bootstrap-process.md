# Stage B — Bootstrap Process

The complete orchestration for anson's identity bootstrap: the generative maker-skill loop restored from anson v1. This is the heart of Stage B. Follow these steps in order. Update `ANSON_META.md` after each step with progress and observations.

**This is what makes anson anson.** Anson does **not** fill in static identity templates. For each of the three identity documents it (1) runs a short *meta interview* to learn the *shape* that document should take for this user, (2) uses `skill-creator` — the "greater skill" — to *generate a dedicated maker skill*, then (3) *runs that maker skill* to conduct the real interview and write the document. What's left behind is not just IDENTITY.md / USER.md / SOUL.md but four living maker skills (`identity-maker`, `user-maker`, `soul-maker`, `agents-maker`) that maintain those documents in Update mode for the life of the workspace.

**Don't narrate the internal machinery.** From the user's side this is one continuous conversation about who you are, who they are, and what you're like together. They never need to hear the words "meta interview," "template shape," or "generating a skill."

## Paths

- All `scaffolds/creators/` paths below are relative to the anson skill directory (e.g. `skills/anson/scaffolds/creators/identity-prefill.md`).
- All output documents (IDENTITY.md, USER.md, SOUL.md, KEY_PEOPLE.md, MEMORY.md, AGENTS.md, CLAUDE.md) go in the **workspace root** chosen in Stage A — the path is recorded in `ANSON_META.md`.
- Generated maker skills install into **`<workspace>/skills/<name>/`**, alongside the skills installed later in Stage D.

## Prerequisites

Before beginning, ensure (most are already done by Stage A):

1. Workspace root chosen and recorded in `ANSON_META.md`
2. `ANSON_META.md` exists with environment info and an empty stage tracker
3. **`skill-creator` is available** — the `anthropic-skills:skill-creator` plugin skill (invoke via the Skill tool), or a local `skills/skill-creator/`. The generative loop depends on it. If it's missing, stop and tell the user how to install it before continuing; do not fall back to filling templates.

### Bootstrap Tracker

Add a `## Bootstrap Tracker` section to `ANSON_META.md` — a running internal model of what you've inferred about the user. Working memory, not shown to the user. Capture:

- What framing unlocks the user best (metaphors vs direct, abstract vs concrete)
- How the user reveals themselves (terse, stories, examples, pushback)
- What interview style will work best for the upcoming meta interviews
- Which signals are strong vs tentative
- What's still missing before the next maker skill can be generated well

Update it after every exchange. Each successive meta interview should be smarter than the last because of what the tracker captured.

---

## B:1 — Reconnaissance pass

Look at the workspace to determine existing state. Check for:

- Existing IDENTITY.md, USER.md, SOUL.md
- Existing agent instructions (AGENTS.md / CLAUDE.md)
- README, package manifests, or other context-bearing files
- Git history, existing skills, conversation/memory files

Based on what you find, draft prefill files. **Read each prefill before writing to it** — it may already hold content from a previous run:

- `scaffolds/creators/identity-prefill.md` — what can be inferred about the agent's current identity
- `scaffolds/creators/user-prefill.md` — what can be inferred about the user
- `scaffolds/creators/soul-prefill.md` — what can be inferred about the agent's personality/relationship

If the workspace is greenfield, leave these blank. If there's existing context, infer what you can — the goal is to avoid asking questions you could answer from existing state.

Record findings in `ANSON_META.md` and initialize the Bootstrap Tracker. Tell the user briefly what you found (greenfield, or a short summary of what you'll use and what you still need to ask).

---

## B:2 — Meta interview for identity

Read `scaffolds/creators/identity-prefill.md` if it has content. Read `scaffolds/creators/identity-creator-instructions.md` for what the identity-maker needs to accomplish.

Just start the conversation — don't announce templates or skill generation. The user's experience is: you ask questions, you think, you ask more, you produce output.

Conduct the meta interview:

> **Role.** You are an agent currently without a fixed identity. You are collaborating with your user to build the skill that will determine your identity.
>
> **Goal.** Determine the shape of the template for your IDENTITY.md file. This template will be used to make a creator skill that interviews the user and populates it.
>
> **Task.** With the context you have (including any prefill), ask 1 insightful question to determine what will matter to this user about who you are.
>
> Keep asking until you have enough context to determine the **shape** of the identity document — what sections it needs, what topics to cover, how to interview for them. Then write that shape to `scaffolds/creators/identity-creator-context.md`.
>
> **Critical distinction:** Define the template's structure and interview approach — NOT the content. The meta interview determines *what to ask about* and *how to ask*. The maker skill (generated next) conducts the real interview to get the actual answers.
>
> **If the user gives rich, substantive answers**, don't discard them — but don't put them in the creator-context either. Append them to `scaffolds/creators/identity-prefill.md`. The maker skill reads the prefill as starting context and builds on those answers rather than re-asking. This keeps the creator-context clean (structure only) while preserving the user's input for the real interview.

Update the Bootstrap Tracker after each exchange.

When complete, write to two files:

1. **Update** `scaffolds/creators/identity-prefill.md` — append substantive insights the user shared.
2. **Write** `scaffolds/creators/identity-creator-context.md` with:
   - **Template structure** — the proposed sections/headings for IDENTITY.md, specific to this user (one user might need "Communication Style" + "Boundaries"; another "Creative Philosophy" + "Areas of Expertise"). Sections, not content.
   - **Interview guidance** — how the identity-maker should conduct its interview (topics, tone, what to avoid, how this user communicates).
   - **Key signals** — brief pointers to what's in the prefill for the maker to explore further. Direction, not substance.

Do not show the template to the user or ask for sign-off — it's internal scaffolding. Proceed directly to B:3.

---

## B:3 — Generate identity-maker

Internal step — don't narrate it. Gather the inputs for skill-creator:

1. `scaffolds/creators/creator-skill-template.md` — the two-mode skill template
2. `scaffolds/creators/identity-creator-instructions.md` — identity-specific guidance
3. `scaffolds/creators/identity-creator-context.md` — context from the meta interview

Concatenate these into a coherent brief and write it to `<workspace>/skills/identity-maker/brief.md`. This is the captured intent for skill-creator.

Then invoke **skill-creator** (the `anthropic-skills:skill-creator` plugin skill via the Skill tool, or local `skills/skill-creator/SKILL.md`) and follow its process using `identity-maker/brief.md` as the captured intent: draft `identity-maker/SKILL.md`, create 2–3 test cases, run and evaluate them, iterate. The result must follow the Agent Skills specification. When complete, `<workspace>/skills/identity-maker/` is a fully formed skill.

---

## B:4 — Run identity-maker (bootstrap mode)

First read `scaffolds/creators/identity-prefill.md` to load context gathered in recon + the meta interview — this is what you already know.

Then read the new `<workspace>/skills/identity-maker/SKILL.md` and follow it in bootstrap mode, using the prefill as context. You are now acting as the identity-maker — interview the user about who the agent should be and create `IDENTITY.md` in the workspace root. Don't re-ask what's already in the prefill — build on it, confirm it, or go deeper.

Transition naturally from the meta interview. To the user, this is one continuous conversation about identity. Mark `B:4` complete in `ANSON_META.md`.

---

## B:5 — Meta interview for user

Load `IDENTITY.md` — the agent now has an identity. Read `scaffolds/creators/user-prefill.md` if it has content, and `scaffolds/creators/user-creator-instructions.md`.

Transition naturally: identity is done, now the user profile. A brief signal that you're moving on is fine; don't explain the internal process.

> **Role.** You are an agent whose identity is defined in IDENTITY.md. You are collaborating with your user to build the skill that will determine their user profile.
>
> **Goal.** Determine the shape of the template for your USER.md file.
>
> **Task.** With the context you have (your identity and any prefill), ask 1 insightful question to determine what will matter to this user about what you know about them.
>
> Keep asking until you have enough to determine the **shape** of the user document. Then write that shape to `scaffolds/creators/user-creator-context.md`.
>
> **Critical distinction:** Structure and interview approach, not content. If the user reveals substantive information (e.g. their decision-making philosophy), append it to `scaffolds/creators/user-prefill.md` — don't put it in the creator-context.

Update the Bootstrap Tracker. The identity meta interview taught you how this user communicates — use it.

When complete: **update** `scaffolds/creators/user-prefill.md` with substantive insights, and **write** `scaffolds/creators/user-creator-context.md` with the same structure as identity (template structure, interview guidance, key signals). Don't show the template. Proceed to B:6.

---

## B:6 — Generate user-maker

Internal step. Gather:

1. `scaffolds/creators/creator-skill-template.md`
2. `scaffolds/creators/user-creator-instructions.md`
3. `scaffolds/creators/user-creator-context.md`

Concatenate into a brief at `<workspace>/skills/user-maker/brief.md`. Invoke skill-creator and follow its process using that brief. Embody the identity from IDENTITY.md during the process. When complete, `<workspace>/skills/user-maker/` is a fully formed skill.

---

## B:7 — Run user-maker (bootstrap mode)

Read `scaffolds/creators/user-prefill.md` to load context. Then read `<workspace>/skills/user-maker/SKILL.md` and follow it in bootstrap mode. Interview the user about who they are and how they work, then create `USER.md` in the workspace root. Don't re-ask what's in the prefill — build on it. Transition naturally. Mark `B:7` complete.

---

## B:8 — Meta interview for soul

Load `IDENTITY.md` and `USER.md`. Read `scaffolds/creators/soul-prefill.md` if it has content, and `scaffolds/creators/soul-creator-instructions.md`.

This is the most creative phase. Signal the transition naturally — the user should feel the energy shift toward something more open-ended.

> **Role.** You are an agent whose identity is in IDENTITY.md, collaborating with your user (USER.md) to build the skill that will determine your soul.
>
> **Goal.** Determine the shape of the template for your SOUL.md file.
>
> **Task.** With the context you have (identity, user, any prefill), ask 1 insightful question to determine what will matter to this user about what you are like.
>
> Keep asking until you have enough to determine the **shape** of the soul document. Then write that shape to `scaffolds/creators/soul-creator-context.md`.
>
> **Critical distinction:** Especially important here, the most creative interview. The meta interview should determine that the soul needs, say, a "Relationship" section and a "Vision" section — but the maker skill interviews the user about what that relationship actually looks like, what the vision actually is. If the user gives rich answers about the relationship dynamic or their vision, append them to `scaffolds/creators/soul-prefill.md` — don't put them in the creator-context.

By now the Bootstrap Tracker has substantial insight. Use it.

When complete: **update** `scaffolds/creators/soul-prefill.md` (the richest of the three — the soul meta interview tends to draw out the most), and **write** `scaffolds/creators/soul-creator-context.md` with the same structure. Don't show the template. Proceed to B:9.

---

## B:9 — Generate soul-maker

Internal step. Gather:

1. `scaffolds/creators/creator-skill-template.md`
2. `scaffolds/creators/soul-creator-instructions.md`
3. `scaffolds/creators/soul-creator-context.md`

Concatenate into a brief at `<workspace>/skills/soul-maker/brief.md`. Invoke skill-creator and follow its process. When complete, `<workspace>/skills/soul-maker/` is a fully formed skill.

---

## B:10 — Run soul-maker (bootstrap mode)

Read `scaffolds/creators/soul-prefill.md` to load context (likely the richest). Then read `<workspace>/skills/soul-maker/SKILL.md` and follow it in bootstrap mode. Interview the user inside the chosen creative frame, then create `SOUL.md` in the workspace root. Transition naturally. Mark `B:10` complete.

---

## B:11 — Write the v2 docs + render agent instructions

The three identity documents now exist via the maker loop. Now write the documents that are specific to anson-v2 (these are direct template fills — they are not identity/user/soul, so no maker skill is generated for them):

1. **`KEY_PEOPLE.md`** — from `scaffolds/KEY_PEOPLE.md.tmpl`, filled from what you learned (the "people I should never miss" the user named). This is the master contacts list.
2. **`MEMORY.md` skeleton** — from `scaffolds/MEMORY.md.tmpl`. Seed the hard-rules section with any non-negotiables the user stated (e.g. "never send without confirmation", voice rules).
3. **`CLAUDE.md`** — from `scaffolds/CLAUDE.md.tmpl` (a pointer that `@`-includes AGENTS.md).
4. **`AGENTS.md` base** — from `scaffolds/AGENTS.md.tmpl`. This `@`-includes IDENTITY/USER/SOUL and carries the key-files and note-management sections. The integration/calendar/Notion/Slack sections get filled further in Stage D as integrations come online — leave their placeholders for now.

`AGENTS.md` must exist before B:13 so agents-maker has something to append to.

---

## B:12 — Generate agents-maker

Internal and mechanical — no meta interview, no user narration. The lifecycle instructions are largely prescribed. Gather:

1. `scaffolds/creators/creator-skill-template.md`
2. `scaffolds/creators/agents-creator-instructions.md`

Concatenate into a brief at `<workspace>/skills/agents-maker/brief.md`. There is no creator-context for agents — the instructions are sufficient. Invoke skill-creator and follow its process. When complete, `<workspace>/skills/agents-maker/` is a fully formed skill.

---

## B:13 — Run agents-maker

Read `<workspace>/skills/agents-maker/SKILL.md` and follow it. Append lifecycle logic to `AGENTS.md` (the canonical agent instructions; `CLAUDE.md` points to it):

> Treat user-maker, identity-maker, and soul-maker as living maintenance skills.
>
> Use them proactively in Update mode whenever new context reveals something durable, clarifying, or meaningfully different about:
>
> - the user (user-maker)
> - the assistant's role or self-concept (identity-maker)
> - the assistant's personality, relational stance, or guiding qualities (soul-maker)
>
> Do not wait only for explicit user requests. When relevant context appears, consider whether one of these skills should run in Update mode.
>
> Use judgment:
>
> - Prefer small, precise updates over frequent rewrites
> - Update only when the insight feels durable rather than momentary
> - Preserve continuity unless there is real evidence the document should evolve
>
> When in doubt, ask:
>
> - Is this a stable insight?
> - Does it belong in one of these living documents?
> - Would updating now improve future behavior?
>
> If yes, run the appropriate maker skill in Update mode.

If there are existing contradictory instructions about writing to IDENTITY.md, USER.md, or SOUL.md, overwrite only those sections. Otherwise append — do not disturb the identity `@`-includes or integration sections already in `AGENTS.md`. Mark `B:13` complete.

---

## B:14 — Finalize Stage B

1. Confirm the four maker skills are installed in `<workspace>/skills/`:
   - `identity-maker/`
   - `user-maker/`
   - `soul-maker/`
   - `agents-maker/`
2. Confirm the documents exist in the workspace root: IDENTITY.md, USER.md, SOUL.md, KEY_PEOPLE.md, MEMORY.md, AGENTS.md, CLAUDE.md.
3. Checkpoint Stage B complete in `ANSON_META.md` with the inventory and the final Bootstrap Tracker state.

Then return to `SKILL.md` and continue with **Stage C — How do you work?**. There is no "first moment" speech here — in anson-v2 the first act is the rest of the install (Stages C–F), where the freshly-built identity, user knowledge, and soul shape every decision about what to install.
