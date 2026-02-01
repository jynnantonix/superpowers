# Superpowers Skills System

A portable collection of skills, commands, and hooks for Claude Code that guide structured development workflows including brainstorming, planning, test-driven development, and systematic debugging.

## Installation

### Fresh Install

If you don't have a `.claude/` directory yet:

```bash
# From your project root
cp -r path/to/portable/commands .claude/commands
cp -r path/to/portable/hooks .claude/hooks
cp -r path/to/portable/skills .claude/skills
cp -r path/to/portable/agents .claude/agents
```

Then create `.claude/settings.json`:

```json
{
  "hooks": {
    "SessionStart": [
      {
        "matcher": "startup|resume|clear|compact",
        "hooks": [
          {
            "type": "command",
            "command": "${CLAUDE_PROJECT_DIR}/.claude/hooks/session-start.sh"
          }
        ]
      }
    ]
  }
}
```

### Merge Into Existing Configuration

If you already have a `.claude/` directory with content:

1. Copy the folders (merge if they exist):
```bash
cp -rn path/to/portable/commands/* .claude/commands/
cp -rn path/to/portable/hooks/* .claude/hooks/
cp -rn path/to/portable/skills/* .claude/skills/
cp -rn path/to/portable/agents/* .claude/agents/
```

2. Add the hook configuration to your existing `.claude/settings.json`:

```json
{
  "hooks": {
    "SessionStart": [
      {
        "matcher": "startup|resume|clear|compact",
        "hooks": [
          {
            "type": "command",
            "command": "${CLAUDE_PROJECT_DIR}/.claude/hooks/session-start.sh"
          }
        ]
      }
    ]
  }
}
```

If you already have a `SessionStart` hook, merge the matcher and hooks into your existing configuration.

## Usage

### Slash Commands

- **`/brainstorm`** - Start a collaborative brainstorming session to explore ideas and create designs before implementation
- **`/write-plan`** - Create a detailed implementation plan from a spec or requirements
- **`/execute-plan`** - Execute an existing implementation plan with batch checkpoints

### Typical Workflow

1. **`/brainstorm`** - Explore the idea, clarify requirements, produce a design spec
2. **`/write-plan`** - Turn the spec into a detailed implementation plan
3. **`/execute-plan`** - Execute the plan in batches with review checkpoints

## Available Skills

| Skill | Description |
|-------|-------------|
| **brainstorming** | Use before any creative work - creating features, building components, adding functionality, or modifying behavior. Explores user intent, requirements and design before implementation. |
| **dispatching-parallel-agents** | Use when facing 2+ independent tasks that can be worked on without shared state or sequential dependencies. |
| **executing-plans** | Use when you have a written implementation plan to execute in a separate session with review checkpoints. |
| **finishing-a-development-branch** | Use when implementation is complete, all tests pass, and you need to decide how to integrate the work. |
| **receiving-code-review** | Use when receiving code review feedback, before implementing suggestions, especially if feedback seems unclear or technically questionable. |
| **requesting-code-review** | Use when completing tasks, implementing major features, or before merging to verify work meets requirements. |
| **subagent-driven-development** | Use when executing implementation plans with independent tasks in the current session. |
| **systematic-debugging** | Use when encountering any bug, test failure, or unexpected behavior, before proposing fixes. |
| **test-driven-development** | Use when implementing any feature or bugfix, before writing implementation code. |
| **using-git-worktrees** | Use when starting feature work that needs isolation from current workspace or before executing implementation plans. |
| **using-superpowers** | Use when starting any conversation - establishes how to find and use skills. |
| **verification-before-completion** | Use when about to claim work is complete, fixed, or passing, before committing or creating PRs. |
| **writing-plans** | Use when you have a spec or requirements for a multi-step task, before touching code. |
| **writing-skills** | Use when creating new skills, editing existing skills, or verifying skills work before deployment. |

## Customization

These skills are designed to be customized for your project:

- **Modify skills** - Edit any skill in `.claude/skills/` to match your team's practices
- **Add project-specific skills** - Create new skill directories following the same structure
- **Adjust hooks** - Modify `session-start.sh` to load different skills at startup
- **Create new commands** - Add `.md` files to `.claude/commands/` for custom slash commands

Each skill follows a consistent structure with frontmatter (name, description) and detailed guidance. Review the existing skills for examples of the format.
