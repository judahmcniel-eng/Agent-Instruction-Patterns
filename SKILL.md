# Agent Instruction Patterns

A toolkit for writing instructions that AI agents will actually follow.

The throughline: agents follow **first actions**, **ordered priorities**, and **named failure modes** more reliably than abstract principles or stern emphasis.

## First Action

When asked to improve agent instructions, do not simply make the instruction longer, louder, or more emphatic.

First identify the behavior that keeps failing. Then rewrite the instruction using this structure:

```text
trigger → first action → priority ladder → forbidden rationalization → self-check
```

If a rule keeps failing, assume the problem is not emphasis. Assume the instruction lacks a concrete trigger, a first action, or a named forbidden substitute.

---

## When to Use This Skill

Use these patterns when writing or fixing:

- a `SKILL.md` for a repeatable workflow
- a project `CLAUDE.md`, `AGENTS.md`, or persistent instruction file
- a custom system prompt
- an agent persona
- tool or connector routing rules
- coding-agent instructions
- any guideline that keeps getting ignored

If a rule keeps failing, do not make it louder. Reshape it using the right pattern.

---

## Pattern 1 — Teach With Trigger → Action, Not Description

Agents internalize “when you see X, do Y” better than “you should generally do Y.”

Every important rule should have a concrete trigger and a concrete first action.

Weak:

```text
Use flat CSS class names when building BeBuilder sections.
```

Strong:

```text
User asks for a styled BeBuilder section → write flat class names like `wagonbox-hero`. Never use scoped selector names like `.section .hero`.
```

Better structure:

```text
When [specific user request or context appears] → first [specific action]. Do not [common wrong behavior].
```

---

## Pattern 2 — Spend Repetition Only on True Non-Negotiables

Repetition signals that a rule is load-bearing. Use it sparingly.

Repeat only rules where violation would break the task, corrupt the workflow, or cause the agent to use the wrong source of truth.

Weak:

```text
Always use the right tool. It is very important to use the right tool. Never use the wrong tool.
```

Strong:

```text
For client-site facts, use the WordPress MCP before web search. Repeat check before final: Did I use the site source instead of guessing from memory?
```

Do not repeat every preference. Repetition loses force when everything is treated as critical.

---

## Pattern 3 — Name the Rationalization, Then Forbid It

Agents often invent a special case to avoid the required behavior. Name the escape hatch directly and close it.

Weak:

```text
Always read the repo before building.
```

Strong:

```text
The tree is a menu, not the meal. Reading file names is not reading files. Do not build from your recollection of the app when the real source is available — that is the lazy path.
```

Use this when an agent commonly says, implicitly or explicitly:

- “The file names were enough.”
- “I already know how this app works.”
- “The README probably tells me enough.”
- “This is a small change, so I can skip the source.”
- “The user probably meant the common version of this.”

Close the exact shortcut the agent is likely to take.

---

## Pattern 4 — Use Ordered Decision Ladders That Stop at the First Match

When routing logic branches, write it as an ordered ladder. The agent should stop at the first matching condition.

This prevents the agent from evaluating all rules simultaneously and choosing the most familiar path.

Example:

```text
Step 0 — Is the answer already in the conversation or supplied files? Use it. Stop.
Step 1 — Is a connected tool the source of truth for this category? Use it. Stop.
Step 2 — Is the fact current, unstable, or likely to drift? Verify with the source/web. Stop.
Step 3 — Otherwise answer from stable knowledge.
```

For tool rules, never use unordered bullets when priority matters.

Weak:

```text
Use GitHub for repo files. Use web for public facts. Use memory when appropriate.
```

Strong:

```text
Tool priority:
1. Current conversation/files → use first if sufficient. Stop.
2. GitHub repo source → use for repository code or project files. Stop.
3. Web/source verification → use for current, unstable, or external facts. Stop.
4. General knowledge → use only for stable concepts after the above do not apply.
```

---

## Pattern 5 — Add a Self-Check Before Finishing

A self-check fires at the moment the agent is most likely to skip a requirement.

Use three to six yes/no checks. Keep them concrete.

Example:

```text
Before publishing, confirm:
- Did I read the actual source files, not just the file tree?
- Did I use the required tool before guessing?
- Did I preserve the user’s requested format?
- Did I remove test/debug markup?
```

Avoid vague self-checks like:

```text
Make sure the answer is good.
```

Use observable checks instead.

---

## Pattern 6 — Use Rate of Change for Read-vs-Verify Rules

Tell the agent when stable knowledge is enough and when source verification is required.

Stable facts can often be answered from knowledge. Drifting facts must be read from the source.

Examples of drifting facts:

- package versions
- API signatures
- pricing
- schedules
- laws and regulations
- current page content
- live repo structure
- client-site settings
- product specs
- search rankings

Useful rule:

```text
If the fact can drift, read the source. Do not answer from memory when package versions, current content, API signatures, or client settings could have changed.
```

---

## Pattern 7 — Tool Priority With Trigger Words

When multiple tools are available, rank them explicitly and include trigger words that select each tool.

Example:

```text
Tool priority:
1. WordPress MCP — use for “our site,” “the client site,” “this page,” “BeBuilder,” “theme settings,” or current WordPress content.
2. GitHub — use for repo files, code, README, SKILL.md, branches, commits, and PRs.
3. Web search — use for external current facts, documentation, public examples, or anything likely to have changed.
4. Inline answer — use only for stable concepts or when no source/tool is needed.
```

A tool rule should answer:

- Which tool wins first?
- What words or context trigger it?
- When does the agent stop looking?
- What tool should not be substituted?

---

## Common Agent Failure Modes

Name the failure mode directly when writing corrective instructions.

### The Loud Rule Failure

The instruction repeats “always” or “must” but does not say what to do first.

Fix:

```text
Add a trigger and first action.
```

### The Vague Principle Failure

The rule describes a value but not an observable behavior.

Fix:

```text
Rewrite the value as a visible action or decision rule.
```

### The Tool Drift Failure

The agent chooses a familiar tool instead of the correct source of truth.

Fix:

```text
Use an ordered tool ladder with trigger words.
```

### The Filename Fallacy

The agent reads file names or folder structure and acts as if it has read the actual source.

Fix:

```text
Forbid treating file names, summaries, or memory as a substitute for file contents.
```

### The Special Case Escape

The agent invents an exception because the forbidden rationalization was not named.

Fix:

```text
Name the exact shortcut and say it is not allowed.
```

### The Everything-Is-Critical Failure

Too many rules are marked as non-negotiable, so none of them feel prioritized.

Fix:

```text
Repeat only the one or two rules that break the workflow if ignored.
```

### The Final-Format Drift

The agent does the work but fails the requested output shape.

Fix:

```text
Add a final self-check for format, file type, naming, and delivery requirements.
```

---

## Instruction Rewrite Formula

When rewriting an ignored rule, use this structure:

```text
1. Trigger: When the user, file, tool, or context shows X...
2. First action: Immediately do Y before anything else.
3. Priority ladder: Use A before B before C. Stop at the first match.
4. Forbidden rationalization: Do not treat Z as a substitute for Y.
5. Stop condition: After Y, stop unless...
6. Self-check: Before finishing, confirm A/B/C.
```

Do not add more words unless they change behavior.

---

## How to Fix a Failing Rule

When a rule is being ignored:

1. Name the failure: What is the agent doing wrong?
2. Find the missing trigger: What exact user request, file state, or tool result should activate the rule?
3. Define the first action: What should the agent do before reasoning further?
4. Close the escape hatch: What shortcut will the agent be tempted to treat as good enough?
5. Add a self-check: What should the agent verify before finalizing?

Do not solve ignored rules by adding more capital letters, more “musts,” or more repetition.

---

## Examples

### Example: Repo Reading

Weak:

```text
Read the repo before making changes.
```

Better:

```text
Before editing code, inspect the files related to the requested feature.
```

Best:

```text
User asks for a code change → first open the actual files that implement that feature. File names, README summaries, and memory of the app are not enough. Do not write or patch code until you have read the relevant source file contents.
```

### Example: Tool Routing

Weak:

```text
Use the right tool for the job.
```

Best:

```text
Tool priority:
1. Current conversation/files → use if they already contain the answer. Stop.
2. GitHub → use for repo code, branches, PRs, commits, README, or SKILL.md. Stop.
3. Web → use for current public facts, docs, pricing, package versions, or anything likely to drift. Stop.
4. Inline answer → use only for stable concepts.
```

### Example: BeBuilder Instruction

Weak:

```text
Use BeBuilder instead of raw HTML.
```

Best:

```text
User asks for a WordPress page or section for a BeTheme site → first create the layout using BeBuilder concepts: wraps, items, flat classes, global styles, and reusable sections. Do not jump straight to raw WordPress block editor HTML; that bypasses the intended builder workflow.
```

### Example: Current Facts

Weak:

```text
Make sure information is accurate.
```

Best:

```text
If the answer depends on a current or drifting fact — price, schedule, version, API signature, law, availability, live page content, or repo state — read the current source before answering. Do not rely on memory for facts that can change.
```

---

## Compression Rule

Do not add more words unless they change behavior.

A good instruction should answer:

- When does this apply?
- What is the first action?
- What source or tool wins first?
- What must not be substituted for that action?
- How does the agent know it is done?

Delete any sentence that only explains why the rule is important.

---

## Final Self-Check

Before finalizing an instruction set, confirm:

- Does every important rule have a trigger and first action?
- Are tool and source priorities written as an ordered ladder?
- Is the most likely rationalization explicitly forbidden?
- Are unstable or current facts routed to verification?
- Are there no vague values without observable behavior?
- Is repetition reserved only for the rules that would break the workflow?
- Does the final output format have its own check?

If the answer to any of these is no, revise the instruction before shipping it.