# cloudsec-ares-ai-tools

Shared Codex parent-agent workflow and custom subagents for the Ares team.

## Contents

- `AGENTS.md` defines the parent workflow and delegation rules.
- `.codex/agents/` contains one TOML file per custom subagent.

### Subagents

| Subagent | Role |
| --- | --- |
| [ares_jira_specialist](.codex/agents/ares_jira_specialist.toml) | Jira search and context; specific updates when requested. |
| [ares_code_explorer](.codex/agents/ares_code_explorer.toml) | Read-only code and documentation research. |
| [ares_debugger](.codex/agents/ares_debugger.toml) | Read-only runtime and failure investigation. |
| [ares_developer](.codex/agents/ares_developer.toml) | Scoped code, configuration, and infrastructure changes. |
| [ares_pr_reviewer](.codex/agents/ares_pr_reviewer.toml) | Read-only PR and branch diff review. |
| [ares_github_pr_coordinator](.codex/agents/ares_github_pr_coordinator.toml) | PR metadata and requested creation or updates. |
| [ares_jenkins_specialist](.codex/agents/ares_jenkins_specialist.toml) | Placeholder; not ready for Jenkins work. |

The linked TOMLs contain the complete role definitions.

These files apply to this repository when Codex works here. To use them in another project or across projects, install them in one of the locations below. Merge `AGENTS.md` with existing instructions instead of overwriting repository-specific guidance.

## Personal configuration

For a workflow that applies across local projects, place the files under your Codex home directory:

```text
~/.codex/
├── AGENTS.md
└── agents/
    └── ares_*.toml
```

Copy this repository's `AGENTS.md` to `~/.codex/AGENTS.md` and its agent TOMLs to `~/.codex/agents/`. If you already have personal instructions, merge the workflow into them.

## Project configuration

To share the workflow through a project repository, use:

```text
project-root/
├── AGENTS.md
└── .codex/
    └── agents/
        └── ares_*.toml
```

Copy this repository's `AGENTS.md` to the project root and the agent TOMLs to `.codex/agents/`. If the project already has an `AGENTS.md`, merge the workflow with its existing instructions. Keep repository-specific practices in the project's instructions.

A project `AGENTS.md` belongs at the repository root, not under `.codex/`.

## Instruction order

Codex reads global instructions first, then project instructions from the repository root toward the current directory. Instructions in a closer directory take precedence when they conflict. In each directory, `AGENTS.override.md` replaces `AGENTS.md` if both exist.

If `~/.codex/AGENTS.override.md` exists, Codex reads it instead of `~/.codex/AGENTS.md` when a new session starts. Project instructions still load. An override with only extra rules hides the parent workflow stored in the personal `AGENTS.md`; include any rules you still need, or edit `AGENTS.md` for a permanent change. Remove the override to restore the personal file.

The TOMLs define agent roles; they do not install external services or grant access to Jira, GitHub, or Jenkins. Those integrations must be available in the Codex session for an agent to use them.

## Example prompt

> use MARS-XXXX as context. Add the Ares subagent TOMLs and `AGENTS.md`, update the README, and open a PR when ready.

The parent agent delegates work when a specialist or parallel investigation helps.
To request delegation explicitly, add `use subagents` to your prompt; you do not need to name them.
