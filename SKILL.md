---
name: superpowers
description: Bootstrap for the full superpowers skill library — TDD, systematic debugging, brainstorming, code review, plan writing, branch finishing, parallel agents, git worktrees, and more. Use at the start of every task, before clarifying questions, before planning, before coding. If any skill might apply, invoke this first. Never skip it because a task seems simple.
---

<SUBAGENT-STOP>
If you were dispatched as a subagent to execute a specific task, skip this skill.
</SUBAGENT-STOP>

<EXTREMELY-IMPORTANT>
If you think there is even a 1% chance a skill might apply to what you are doing, you ABSOLUTELY MUST invoke the skill.

IF A SKILL APPLIES TO YOUR TASK, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.

This is not negotiable. This is not optional. You cannot rationalize your way out of this.
</EXTREMELY-IMPORTANT>

## Instruction Priority

Superpowers skills override default system prompt behavior, but **user instructions always take precedence**:

1. **User's explicit instructions** (CLAUDE.md, AGENTS.md, direct requests) — highest priority
2. **Superpowers skills** — override default system behavior where they conflict
3. **Default system prompt** — lowest priority

If CLAUDE.md or AGENTS.md says "don't use TDD" and a skill says "always use TDD," follow the user's instructions. The user is in control.

## How to Access Skills

**With the full superpowers plugin installed** (`IvDev19/superpowers-IvDev19`): Use the `Skill` tool. When you invoke a skill, its content is loaded and presented to you — follow it directly. Never use the Read tool on skill files.

**Standalone (this skill only):** Fetch skill content on demand via WebFetch. See `references/skill-library.md` for the full URL index of all 14 skills.

**In Copilot CLI:** Use the `skill` tool. Skills are auto-discovered from installed plugins. See `references/copilot-tools.md` for tool equivalents.

**In other environments:** Check your platform's documentation for how skills are loaded.

## Platform Adaptation

Skills use Claude Code tool names. Non-CC platforms: see `references/copilot-tools.md` for tool equivalents.

# Using Skills

## The Rule

**Invoke relevant or requested skills BEFORE any response or action.** Even a 1% chance a skill might apply means that you should invoke the skill to check. If an invoked skill turns out to be wrong for the situation, you don't need to use it.

```dot
digraph skill_flow {
    "User message received" [shape=doublecircle];
    "About to EnterPlanMode?" [shape=doublecircle];
    "Already brainstormed?" [shape=diamond];
    "Invoke brainstorming skill" [shape=box];
    "Might any skill apply?" [shape=diamond];
    "Invoke Skill tool" [shape=box];
    "Announce: 'Using [skill] to [purpose]'" [shape=box];
    "Has checklist?" [shape=diamond];
    "Create TodoWrite todo per item" [shape=box];
    "Follow skill exactly" [shape=box];
    "Respond (including clarifications)" [shape=doublecircle];

    "About to EnterPlanMode?" -> "Already brainstormed?";
    "Already brainstormed?" -> "Invoke brainstorming skill" [label="no"];
    "Already brainstormed?" -> "Might any skill apply?" [label="yes"];
    "Invoke brainstorming skill" -> "Might any skill apply?";

    "User message received" -> "Might any skill apply?";
    "Might any skill apply?" -> "Invoke Skill tool" [label="yes, even 1%"];
    "Might any skill apply?" -> "Respond (including clarifications)" [label="definitely not"];
    "Invoke Skill tool" -> "Announce: 'Using [skill] to [purpose]'";
    "Announce: 'Using [skill] to [purpose]'" -> "Has checklist?";
    "Has checklist?" -> "Create TodoWrite todo per item" [label="yes"];
    "Has checklist?" -> "Follow skill exactly" [label="no"];
    "Create TodoWrite todo per item" -> "Follow skill exactly";
}
```

## Red Flags

These thoughts mean STOP—you're rationalizing:

| Thought | Reality |
|---------|---------|
| "This is just a simple question" | Questions are tasks. Check for skills. |
| "I need more context first" | Skill check comes BEFORE clarifying questions. |
| "Let me explore the codebase first" | Skills tell you HOW to explore. Check first. |
| "I can check git/files quickly" | Files lack conversation context. Check for skills. |
| "Let me gather information first" | Skills tell you HOW to gather information. |
| "This doesn't need a formal skill" | If a skill exists, use it. |
| "I remember this skill" | Skills evolve. Read current version. |
| "This doesn't count as a task" | Action = task. Check for skills. |
| "The skill is overkill" | Simple things become complex. Use it. |
| "I'll just do this one thing first" | Check BEFORE doing anything. |
| "This feels productive" | Undisciplined action wastes time. Skills prevent this. |
| "I know what that means" | Knowing the concept ≠ using the skill. Invoke it. |

## Skill Priority

When multiple skills could apply, use this order:

1. **Process skills first** (brainstorming, debugging) — these determine HOW to approach the task
2. **Implementation skills second** — these guide execution

"Let's build X" → brainstorming first, then implementation skills.
"Fix this bug" → debugging first, then domain-specific skills.

## Skill Types

**Rigid** (TDD, debugging): Follow exactly. Don't adapt away discipline.

**Flexible** (patterns): Adapt principles to context.

The skill itself tells you which.

## User Instructions

Instructions say WHAT, not HOW. "Add X" or "Fix Y" doesn't mean skip workflows.

# Skill Library

Full library source: `https://github.com/IvDev19/superpowers-IvDev19` — 14 skills, load on demand only.

For standalone fetch URLs, load `references/skill-library.md`.

| Skill | Purpose | Load when |
|-------|---------|-----------|
| brainstorming | Visual/interactive brainstorming (WS server) | User needs visual/interactive brainstorming |
| dispatching-parallel-agents | Run multiple subagents in parallel | Parallelizing independent tasks |
| executing-plans | Execute a structured plan step by step | Implementing an approved plan |
| finishing-a-development-branch | Merge/PR/cleanup after dev work | A development cycle completes |
| receiving-code-review | Process and respond to review feedback | Review comments arrive |
| requesting-code-review | Request and structure a code review | Before merging a non-trivial change |
| subagent-driven-development | Autonomous multi-task dev via subagents | Large feature implementation |
| systematic-debugging | Structured debugging methodology | Debugging a non-obvious bug |
| test-driven-development | TDD red-green-refactor workflow | Writing new features test-first |
| using-git-worktrees | Isolated worktree per feature | Required before subagent-driven-development |
| using-superpowers | Plugin bootstrap and skill index | Loaded at session start always |
| verification-before-completion | Pre-completion checklist | Before marking any task done |
| writing-plans | Write structured implementation plans | Before executing a non-trivial feature |
| writing-skills | Author new skills for this plugin | Creating a new skill |
