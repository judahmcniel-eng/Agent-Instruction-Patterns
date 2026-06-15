# Agent Instruction Patterns

A practical toolkit for writing AI agent instructions that actually get followed.

This repo is for improving `SKILL.md` files, project instructions, system prompts, agent personas, and tool-routing rules. The main idea is simple: agents follow **concrete first actions**, **ordered decision ladders**, and **named failure modes** better than abstract principles or louder emphasis.

## Core Rule

If a rule keeps failing, do not make it louder. Assume the instruction lacks one of these:

- a concrete trigger
- a required first action
- an ordered priority ladder
- a named forbidden substitute
- a final self-check

## What This Helps With

Use these patterns when writing or fixing:

- `SKILL.md` files for repeatable workflows
- `CLAUDE.md`, `AGENTS.md`, or project instruction files
- custom system prompts
- agent personas
- tool and connector routing rules
- coding-agent instructions
- workflow checklists that agents keep ignoring

## The Main Pattern

Rewrite weak instructions into this shape:

```text
When you see X → do Y first → use this priority order → do not substitute Z → before finishing, check A/B/C.
```

Agents respond better to instructions that name the exact moment a rule activates and the exact first move to make.

## Example

Weak:

```text
Always read the repo before building.
```

Stronger:

```text
User asks for a code change → first open the actual files that implement the requested feature. File names, README summaries, and memory of the app are not enough. Do not write or patch code until you have read the relevant source file contents.
```

## Included Patterns

The `SKILL.md` covers:

1. Trigger → action instructions
2. Repetition only for true non-negotiables
3. Naming the rationalization and forbidding it
4. Ordered decision ladders
5. Self-checks before finishing
6. Rate-of-change rules for read-vs-verify decisions
7. Explicit tool priority ordering
8. Common agent failure modes
9. A reusable rewrite formula
10. Compression rules for keeping instructions sharp

## How to Use

Copy the relevant pattern from `SKILL.md` into your own project instructions, then adapt it to the actual workflow.

A good instruction should answer:

- When does this rule apply?
- What should the agent do first?
- Which source or tool wins if several seem relevant?
- What shortcut is forbidden?
- How does the agent know it complied?

## License

Use and adapt freely.