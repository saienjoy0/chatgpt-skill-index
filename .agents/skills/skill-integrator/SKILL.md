---
name: skill-integrator
description: Use when adopting, combining, forking, or folding one or more existing agent skills, SKILL.md files, GitHub repositories, or documented agent workflows into a user's own existing skill without blindly concatenating them.
---

# Skill Integrator

## Overview

Turn useful third-party skills into improvements to the user's own skill. Extract behavior, preserve the target skill's identity, resolve conflicts explicitly, and keep provenance so the result can evolve safely.

**Core principle:** integrate capabilities, not files.

A successful fold-in should make the target skill better at its job without turning it into a dump of copied instructions.

## When to Use

Use this skill when the user says things like:
- "このSkillを自分のSkillに入れて"
- "これをベースに改造したい"
- "この2つのSkillを統合して"
- "このGitHub repoの良い部分を取り込みたい"
- "fork/cloneして自分用にしたい"
- "既存Skillを育てたい"

Do not use merely to summarize a repository or compare two skills without modifying/creating a target skill.

## Inputs

Identify:
1. **TARGET** — the user's existing skill directory/repository, or the new skill to create.
2. **SOURCES** — one or more SKILL.md files, skill directories, repositories, docs, or URLs.
3. **USER INTENT** — what capability the user wants to gain.
4. **HOST** — ChatGPT/Codex, Claude Code, Copilot CLI, Amp, or another agent runtime if relevant.

If TARGET is not explicitly named but there is one obvious active skill/project, use it. Do not ask a question that can be resolved by inspecting the repository.

## Fold-in Workflow

### 1. Inspect the target first

Read the target skill before reading sources deeply.

Capture:
- mission
- trigger/description
- current workflow
- tools/integrations
- state/memory model
- invariants and safety/privacy rules
- existing references/scripts/tests

The target is the product. Sources are ingredients.

### 2. Inspect source provenance and license

For every source, record:
- repository / URL
- exact path to the skill or relevant files
- commit/ref when available
- license
- files actually used

If redistribution/modification rights are unclear, do not vendor substantial copied text. Extract ideas and keep a link/provenance note instead.

### 3. Extract capabilities, not summaries

For each source identify only reusable behavior:

| Category | Extract |
|---|---|
| Trigger | When should this behavior activate? |
| Decision rules | How does it choose what to do? |
| Workflow | What ordered actions matter? |
| State | What must persist between runs? |
| Tools | Which integrations/actions are required? |
| Failure handling | What happens when data is missing/stale/conflicting? |
| Proactivity | What should happen before the user asks? |
| Tests | What scenario proves the behavior works? |

Ignore branding, redundant prose, source-specific assumptions, and features unrelated to USER INTENT.

### 4. Build a capability matrix

Compare TARGET vs SOURCES.

Classify each candidate capability as:
- **KEEP** — target already handles it well.
- **ADD** — missing and useful.
- **UPGRADE** — source has a stronger version of existing behavior.
- **ADAPT** — useful but must change for the user's environment.
- **REJECT** — irrelevant, conflicting, unsafe, overly broad, or too costly.

Do not merge duplicate instructions just because they are phrased differently.

### 5. Resolve conflicts using this precedence

Highest priority first:
1. Explicit current user requirements.
2. Target skill's core mission and user-specific rules.
3. Current real integrations/capabilities of the host environment.
4. Proven useful behavior from source skills.
5. Source defaults and stylistic preferences.

Never let a newly imported source silently weaken privacy, safety, confirmation rules, or a user-specific invariant.

### 6. Design the patch before writing

A fold-in should normally modify the smallest useful surface:
- `SKILL.md` for core behavior and triggers.
- `references/` for detailed procedures or source-derived knowledge.
- `scripts/` for deterministic/repeated logic.
- `tests/` or scenario files for behavioral checks.
- `SOURCES.md` for provenance.

Avoid giant SKILL.md files. Keep frequently needed decision rules in the main skill; move long reference material out.

### 7. Apply the fold-in

When editing an existing skill:
- preserve its name unless renaming is necessary;
- preserve unrelated working behavior;
- add only capabilities justified by USER INTENT;
- update the `description` only when trigger coverage truly changes;
- remove obsolete/conflicting instructions rather than leaving both versions;
- record the source and date in `references/SOURCES.md`.

When creating a new skill from several sources, define one coherent mission first, then integrate capabilities under that mission.

### 8. Validate behavior with scenarios

Before declaring success, test at least these classes:

**Positive trigger:** a request that should invoke the new capability.

**Negative trigger:** a superficially similar request that should not invoke it.

**Conflict case:** imported behavior conflicts with an existing user-specific rule.

**Missing-data case:** required external state is unavailable or stale.

**Update case:** a later source is folded into the already-modified target.

For manager/planner skills also test:
- a deadline hidden inside a casual message;
- a hard calendar conflict;
- an overdue item;
- a deadline with a practical start date earlier than the official due date;
- a new message that invalidates an old plan.

### 9. Report the delta

After integration, state concisely:
- what was added/upgraded;
- what was deliberately not imported;
- which source(s) informed the change;
- where the target skill now lives;
- any remaining integration that requires external credentials or runtime setup.

## Special Mode: Life Manager Fold-in

When TARGET is a personal/executive/life-manager skill, prioritize imported capabilities in this order:

1. Deadline / application / submission / renewal detection.
2. Practical latest-start-date calculation, not just official due dates.
3. Current-time-aware next-action selection.
4. Calendar conflicts and available work windows.
5. Commitments, waiting-for, follow-ups, and unresolved loops.
6. Persistent memory of durable facts and decisions.
7. Replanning when new messages change state.
8. Proactive surfacing of risk/opportunity only when actionable.

Every incoming real-life message should be evaluated for:
- actionable item?
- official deadline?
- practical start deadline?
- consequence of missing it?
- required prerequisites?
- should it become a task/event/reminder/memory/watch item?
- does it change what the user should do now?

## Source-Inspired Pattern: Update / Fold-in

This skill adopts the useful idea of an explicit **Update / Fold-in** mode from `corpus-to-skill`: new source material can update an existing skill rather than always generating a new one. The implementation here is specialized for merging agent skills and repositories into a user-owned target skill.

## Common Mistakes

**Blind concatenation** — creates contradictory instructions and bloated context. Extract capabilities and rewrite coherently.

**Source becomes the boss** — third-party defaults override the user's established rules. Apply the precedence order.

**No provenance** — six weeks later nobody knows why a rule exists. Keep SOURCES.md.

**Copying without license review** — inspect license before vendoring substantial source text.

**Treating deadlines as dates only** — a 9/30 deadline may require documents by 9/20. Track official due date and practical start date separately.

**Planning once per day** — life-manager targets must re-evaluate after meaningful new information, not only during a morning plan.
