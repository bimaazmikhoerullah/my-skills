---
name: xav-skills
description: Automatically discovers, evaluates, selects, and orchestrates all relevant skills available to the current AI agent for the user's task. Use this skill at the beginning of every substantive task, even when the user does not mention skills. It is a universal coordinator, not a replacement for the individual skills it discovers.
---

# XAV-SKILLS — Universal Skill Orchestrator

## Mission

For every substantive user task, inspect the skills that are actually available to the current agent, identify **all relevant skills**, read their instructions, and coordinate their use. Select skills by task fit and capability—not by category, popularity, or name alone.

The user should not need to name, request, or manually activate an individual skill.

This skill coordinates other skills. It does not override their instructions, grant unavailable capabilities, or claim that a skill was used unless its instructions were actually read and followed.

## Core operating rules

1. **Discover broadly.** Inspect every skill source and skill catalogue that the current platform makes available. Do not assume that one directory, one vendor, or one category contains every installed skill.
2. **Check before acting.** At the start of each substantive task, perform a fresh availability check using the platform's supported discovery mechanism. Reuse cached metadata only if the platform guarantees it is current; otherwise refresh it.
3. **Read before using.** For every candidate selected, read its complete entry-point instructions (normally `SKILL.md`) and any explicitly referenced files needed for the task. A skill's name or summary alone is not enough.
4. **Select all that materially help.** Consider every discovered skill. Select each skill that makes a meaningful contribution to the requested outcome. Do not stop after finding the first match.
5. **Avoid irrelevant loading.** Do not load or execute skills merely because they are installed. Exclude skills that do not materially help the current task.
6. **Respect platform semantics.** Use the current agent's native skill invocation, tool, or workflow. Do not pretend that reading a file is equivalent to invoking a skill if the platform requires an explicit invocation.
7. **Follow skill instructions.** Apply the selected skills' relevant workflows, constraints, tools, and output requirements, subject to higher-priority system, developer, safety, and platform instructions.
8. **Resolve dependencies.** Identify prerequisite skills and invoke/read them before dependent skills when required.
9. **Coordinate safely.** Run independent work in parallel only when the platform supports it and doing so is safe. Use sequential execution when tasks share files, state, resources, or prerequisites.
10. **Re-evaluate dynamically.** If the task changes or new requirements emerge, repeat discovery or matching as needed and add newly relevant skills.
11. **Verify.** Check the result against the user's request and the selected skills' applicable quality criteria. Run available tests or validation steps when appropriate.
12. **Be truthful.** Never claim that all skills were scanned if the platform exposed only a partial catalogue. Never claim a skill was loaded, invoked, or executed unless that actually happened.

## Workflow

### Phase 1 — Discover available skills

At the beginning of every substantive task:

1. Identify the current AI agent and its supported skill mechanism.
2. Inspect all skill registries, directories, manifests, or discovery tools exposed to the agent.
3. Include user-level, project-level, workspace-level, and platform-provided skills when they are visible and accessible.
4. Record each candidate's:
   - name and location/source;
   - description and declared capabilities;
   - entry-point instruction file;
   - prerequisites, tools, or platform requirements, if stated.
5. Deduplicate identical skills while preserving distinct versions or platform-specific variants when their behavior differs.
6. If a source cannot be inspected, note that limitation and continue with accessible sources.

Do not perform unsafe broad filesystem searches. Use documented platform discovery mechanisms and known skill locations. Do not access unrelated private files, secrets, credentials, or directories outside the task's legitimate scope.

### Phase 2 — Understand the task

Convert the user's request into a concise task model:

- desired outcome and deliverables;
- domain(s) involved;
- technologies, languages, frameworks, and platforms named or implied;
- design, quality, security, accessibility, performance, testing, or documentation needs;
- constraints, dependencies, and acceptance criteria.

Interpret intent semantically. For example, "make this website look premium and modern" may require visual design, UX, frontend implementation, responsive design, accessibility, and animation skills—not merely a skill whose name contains "website".

### Phase 3 — Match and select skills

Evaluate every discovered skill against the task model.

Select a skill when its documented capabilities or workflow materially improve a required part of the task. Consider:

- direct task relevance;
- specialist expertise;
- coverage of a required deliverable;
- dependencies on or complementarity with other skills;
- platform/tool availability;
- overlap or conflict with other candidates.

Use the smallest complete set: include every skill that materially contributes, but avoid redundant skills that add no distinct value. If two skills overlap, prefer the one with the more specific, applicable workflow; use both when they provide complementary requirements.

Do not invent a numeric score or claim an objective "best" result unless the platform or skill metadata provides a defensible scoring method.

### Phase 4 — Read and plan

For each selected skill:

1. Read its entry-point instructions in full.
2. Follow links to additional files only when needed for this task or explicitly required by the skill.
3. Identify required tools, inputs, outputs, prerequisites, and restrictions.
4. Build an execution plan that satisfies dependencies and avoids conflicting changes.
5. If instructions conflict, follow higher-priority platform and safety rules first. Among peer skills, prefer the more task-specific instruction for its own domain; reconcile compatible requirements and avoid unsafe actions.

If a required skill is unavailable, do not fabricate its instructions. Continue with available capabilities where reasonable and disclose the gap if it materially affects the result.

### Phase 5 — Execute

- Apply each selected skill's workflow to the relevant part of the task.
- Invoke skills using the current platform's supported mechanism whenever one exists.
- Keep the user's original goal as the source of truth; skills are aids, not permission to change the requested outcome.
- Share context and intermediate outputs between skills only when relevant and permitted.
- Parallelize only independent operations. Sequence operations with dependencies or shared mutable resources.
- Ask the user only when a missing decision or authorization is genuinely necessary. Do not ask the user to choose skills that the orchestrator can select itself.
- Before destructive, externally visible, costly, or security-sensitive actions, obtain the authorization required by platform policy and the user's instructions.

### Phase 6 — Reassess

During execution, check whether:

- the task scope has changed;
- a newly discovered requirement needs another skill;
- a selected skill is unavailable, incompatible, or redundant;
- a dependency or conflict has appeared.

If so, update the skill set and execution plan. Do not restart unrelated completed work.

### Phase 7 — Verify and report

Verify the deliverable against:

1. the user's explicit requirements;
2. the selected skills' applicable instructions;
3. relevant project conventions and quality standards;
4. tests, linting, builds, accessibility checks, or other validation appropriate to the task.

Fix issues when possible. Report unresolved issues honestly.

For normal user-facing responses, keep the report concise. When useful, state:
- which skill areas were actually used;
- important validation performed;
- unavailable or inaccessible skills that materially limited the work.

Do not overwhelm the user with a full inventory of irrelevant installed skills.

## Task examples

### Example A — Premium website UI

User asks: "Create a very modern, premium, responsive website with smooth interactions."

Discover and consider all available skills. A relevant set may include UI/UX design, web design, frontend implementation, responsive design, accessibility, animation, and testing. Read their instructions, coordinate design before implementation where appropriate, then verify responsive behavior and interactions. Do not load unrelated skills such as database administration unless the project requires them.

### Example B — Laravel API

User asks: "Build a secure REST API in Laravel with authentication and tests."

A relevant set may include Laravel/backend development, API design, database design, authentication/security, testing, and documentation. Resolve dependencies and coordinate them; do not automatically load unrelated design or mobile-development skills.

### Example C — Security review

User asks: "Audit this application for security issues."

Consider security auditing, relevant framework-specific security, dependency analysis, code review, and testing skills. Respect authorization and scope. Do not run intrusive tests against systems without permission.

## Platform compatibility and automatic invocation

This skill is written to be platform-neutral, but **a skill cannot guarantee that it will run on every prompt merely by being installed**.

For reliable automatic behavior:

- Install `xav-skills` in a location recognized by the target agent.
- Configure that agent's always-on project/user instructions to tell it to invoke `xav-skills` at the beginning of every substantive task.
- Where the platform supports native automatic skill matching, ensure the description is discoverable and sufficiently broad.
- Where the platform requires explicit skill invocation, use its supported instruction/configuration mechanism; do not assume another agent's convention works.
- Keep platform-specific bootstrap instructions outside this universal skill when formats differ (for example, project instruction files or agent-specific configuration).

If the platform does not expose a complete skill registry or does not support automatic invocation, explain the limitation and use the broadest supported discovery path. Never imply universal filesystem access or cross-agent control.

## Completion checklist

Before finishing a substantive task, confirm:

- [ ] Available skill sources were inspected as far as the platform permits.
- [ ] All discovered skills were considered, not just the first match.
- [ ] Every selected skill's relevant instructions were read.
- [ ] Dependencies and conflicts were considered.
- [ ] All materially relevant selected skills were applied where supported.
- [ ] Newly emerging needs triggered reassessment.
- [ ] The result was verified appropriately.
- [ ] Any discovery, access, or execution limitations were reported accurately.
