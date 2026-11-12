# xav-skills

**Universal Skill Discovery & Orchestration**

`xav-skills` is a coordinator skill for AI coding agents and other assistants that support skills. It discovers the skills available to the current agent, evaluates them against the user's intent, reads the selected skills' instructions, and coordinates all skills that materially help complete the task.

## What it does

- Discovers skills exposed by the current agent.
- Considers the full accessible skill catalogue, not just one category.
- Selects one or multiple relevant skills automatically.
- Reads selected skill instructions before applying them.
- Resolves prerequisites, overlap, and conflicts.
- Coordinates sequential or safe parallel work.
- Reassesses when the task changes.
- Verifies results and reports limitations honestly.

It does **not** blindly run every installed skill. It considers every accessible skill and uses the complete relevant set while excluding irrelevant skills.

## Files

```text
xav-skills/
├── SKILL.md
└── README.md
```

## Installation

Install the `xav-skills` directory in a skill location recognized by your AI agent. Skill locations and discovery rules differ between products and may change over time; follow the current official documentation for the agent you use.

For dependable automatic invocation, also add a short instruction to the agent's always-on user or project instructions:

> At the beginning of every substantive task, invoke and follow the `xav-skills` skill. It must inspect all skill sources exposed to this agent, consider every available skill, read the instructions of all selected relevant skills, and coordinate their use. Do not wait for the user to name a skill. Be transparent about inaccessible skill sources and never claim a skill was used unless it was actually read and applied.

If the agent supports native automatic skill matching, make sure `xav-skills` is discoverable through that mechanism as well.

## Important compatibility note

A portable `SKILL.md` does not, by itself, force every AI agent to execute it on every prompt. Automatic invocation depends on each agent's own skill discovery and instruction mechanisms. Some agents expose only a subset of installed skills, require explicit invocation, or use different directory conventions.

Use the appropriate bootstrap/instruction file for each agent. Do not assume that `AGENTS.md`, `CLAUDE.md`, or another platform's convention is universally recognized.

## Design principle

**Discover everything accessible. Consider every discovered skill. Select the complete relevant set. Read before use. Orchestrate safely. Verify honestly.**
