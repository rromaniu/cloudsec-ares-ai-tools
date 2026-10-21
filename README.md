# cloudsec-ares-ai-tools

Shared Codex parent-agent workflow and custom subagents for the Ares team.

## Contents

- `AGENTS.md` defines the parent workflow and delegation rules.
- `.codex/agents/` contains one TOML file per custom subagent.
- `ares_jenkins_specialist` is a placeholder; it is not ready for Jenkins work.

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

Codex reads global instructions first, then project instructions from the repository root toward the current directory. Instructions in a closer directory take precedence when they conflict. In each directory, `AGENTS.override.md` takes precedence over `AGENTS.md`.

The TOMLs define agent roles; they do not install external services or grant access to Jira, GitHub, or Jenkins. Those integrations must be available in the Codex session for an agent to use them.
