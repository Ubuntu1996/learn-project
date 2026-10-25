# Learn a Project

An agent skill that helps software engineers understand unfamiliar repositories
through evidence-based walkthroughs of their purpose, alternatives, usage,
architecture, execution paths, and design trade-offs.

Instead of summarizing every file, it builds a mental model around one real
workflow and connects explanations to inspected code. No pre-existing knowledge
graph is required.

## Installation

Use a coding agent that supports `SKILL.md`-based skills and can access the project
you want to study. Install through your host's supported skill/plugin installer.

For hosts supported by the [skills CLI](https://github.com/vercel-labs/skills),
run the following with Node.js and npm available. Replace `AGENT_ID` with your
host's identifier from the [supported agents list](https://github.com/vercel-labs/skills/blob/main/docs/agents.md):

```text
npx --yes skills add Ubuntu1996/learn-project --skill learn-project --agent AGENT_ID --global --yes
```

Refresh skill discovery or restart your agent session if the host requires it.

### Diagram prerequisite

The skill requires [diagram-design](https://github.com/cathrynlavery/diagram-design).
At the start of a walkthrough, it checks for an existing installation and reuses
it without updating or overwriting it. If missing, it installs the complete skill
through the active host's supported installer, at user scope and outside the
project under study, subject to host approvals and filesystem permissions.

If installation or loading is blocked, the agent reports the blocker and
continues with prose and tables rather than substituting another renderer.

## Usage

Ask your agent to learn a local repository or an accessible GitHub project:

```text
Help me learn the project at D:\src\InterestingProject.
Explain https://github.com/owner/project. Focus on its plugin architecture.
Walk me through D:\src\InterestingProject. I know TypeScript and want to contribute.
```

For hosts that support `/skill:` invocation:

```text
/skill:learn-project "D:\src\InterestingProject"
/skill:learn-project https://github.com/owner/project
/skill:learn-project "D:\src\InterestingProject" Full walkthrough; goal: contribute.
```

You can specify your background, focus, language preference, or time budget.
For a large monorepo, the agent gives a whole-project orientation and selects a
relevant package or workflow for a deeper look.

## Learning flow

| Stage | Topics |
| --- | --- |
| 1-3: Orientation | Purpose, evidence-backed comparisons with alternatives, and a realistic usage example. |
| 4-6: Implementation | Runtime architecture, a selective code map, and an execution trace of that same example. |
| 7-9: Design and practice | Abstractions and invariants, build/run/test instructions, a reading order, and a small change plan. |
| 10: Optional understanding check | Five interactive questions, asked one at a time, or feedback on your own explanation. |

By default, the first response covers stages 1-3. Say `continue` to move through
4-6, then 7-9, or jump directly to a topic. Request a **full walkthrough** to cover
1-9 without intermediate approval gates; the understanding check remains optional.

Important claims are tied to repository-relative paths and symbols, with line
references when available. The agent distinguishes documented behavior, inspected
implementation, and inference, and makes access limitations or unknowns explicit.

## Diagrams and saved progress

When a visual improves understanding, the skill creates a focused architecture,
sequence, data-flow, or other appropriate diagram using `diagram-design`.
The default is its shipped **default light / Minimal light** style, delivered as
static, self-contained HTML with inline SVG. PNG and standalone SVG exports are
produced only when requested.

Diagrams go to an established output location or, for a local project, to
`docs\learning\diagrams\` beneath the permitted task directory. Workspace and
worktree rules take precedence. The agent returns the artifact path, source
references, and meaningful simplifications, and reports blocked validation checks.

The skill does not automatically remember previous sessions. Ask to **save
progress** for a learning note containing the revision, scope, findings, code
references, diagram links, and next action. On resume, the agent checks that note
against relevant source changes.

## Safety boundaries

- The project under study stays read-only by default, apart from permitted
  learning artifacts. Source edits and exercises are plans, not automatic changes.
- Project dependency installation and execution of builds, tests, examples,
  setup scripts, or application code require separate authorization.
- Installing the prerequisite skill is separate from installing project dependencies.
- Repository instructions, filesystem restrictions, and worktree requirements
  remain in effect. Commits, pushes, and pull requests require an explicit request.
- Private source and diagrams are not uploaded to external services. Unrun commands
  are not presented as verified results.

## Skill definition

[`SKILL.md`](SKILL.md) contains the full workflow, evidence rules, diagram policy,
and completion criteria. This repository contains skill instructions, not a
standalone application.
