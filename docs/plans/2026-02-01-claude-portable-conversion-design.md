# Convert Superpowers Plugin to Portable .claude Directory

**Date:** 2026-02-01
**Status:** Design Complete

## Overview

Convert the superpowers plugin into a self-contained package that users can copy directly into their project's `.claude/` directory, without requiring plugin installation.

## Goals

- Self-contained with skills, commands, and hooks
- Working `/brainstorm`, `/write-plan`, `/execute-plan` commands
- Session bootstrap behavior preserved via hooks
- No build step required - just copy and configure

## Directory Structure

Users receive a folder with this structure to copy into `.claude/`:

```
.claude/
├── commands/
│   ├── brainstorm.md
│   ├── write-plan.md
│   └── execute-plan.md
├── hooks/
│   └── session-start.sh
├── skills/
│   ├── brainstorming/SKILL.md
│   ├── writing-plans/SKILL.md
│   ├── executing-plans/SKILL.md
│   ├── test-driven-development/
│   │   ├── SKILL.md
│   │   └── testing-anti-patterns.md
│   ├── using-git-worktrees/SKILL.md
│   ├── subagent-driven-development/SKILL.md
│   ├── dispatching-parallel-agents/SKILL.md
│   ├── requesting-code-review/SKILL.md
│   ├── receiving-code-review/SKILL.md
│   ├── finishing-a-development-branch/SKILL.md
│   ├── systematic-debugging/SKILL.md
│   ├── verification-before-completion/SKILL.md
│   ├── writing-skills/
│   │   ├── SKILL.md
│   │   ├── anthropic-best-practices.md
│   │   ├── testing-skills-with-subagents.md
│   │   ├── persuasion-principles.md
│   │   ├── graphviz-conventions.dot
│   │   └── examples/
│   └── using-superpowers/SKILL.md
└── agents/
    └── code-reviewer.md
```

## Changes Required

### 1. Prefix Removal

Remove all `superpowers:` prefixes from skill references.

**Commands:**
```markdown
# Before
Invoke the superpowers:brainstorming skill and follow it exactly

# After
Invoke the brainstorming skill and follow it exactly
```

**Skills:**
- Grep all SKILL.md files for `superpowers:` references
- Update to use unprefixed skill names

### 2. Hook Script Updates

**session-start.sh changes:**

```bash
# Before
PLUGIN_ROOT="$(cd "${SCRIPT_DIR}/.." && pwd)"
using_superpowers_content=$(cat "${PLUGIN_ROOT}/skills/using-superpowers/SKILL.md" ...)

# After
SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
CLAUDE_DIR="$(cd "${SCRIPT_DIR}/.." && pwd)"
using_superpowers_content=$(cat "${CLAUDE_DIR}/skills/using-superpowers/SKILL.md" ...)
```

**Also remove:**
- Legacy warning about `~/.config/superpowers/skills`
- References to `${CLAUDE_PLUGIN_ROOT}`

### 3. Hook Configuration

Users must add to `.claude/settings.json`:

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

### 4. README.md

Create installation instructions covering:

1. **What this is** - Brief description of superpowers skills system
2. **Installation steps:**
   - Copy `commands/`, `hooks/`, `skills/`, `agents/` folders into `.claude/`
   - Add hook configuration to `.claude/settings.json`
   - Include both fresh install and merge examples
3. **Usage** - How to use `/brainstorm`, `/write-plan`, `/execute-plan`
4. **Available skills** - List of all 14 skills with descriptions
5. **Customization** - Note that users can modify skills

## Files Included

| Category | Files |
|----------|-------|
| Commands | brainstorm.md, write-plan.md, execute-plan.md |
| Hooks | session-start.sh |
| Skills | 14 skill directories with SKILL.md and supporting files |
| Agents | code-reviewer.md |

## Files Excluded

- `.claude-plugin/`, `.codex/`, `.opencode/` - platform-specific plugin files
- `lib/` - plugin infrastructure code
- `tests/` - development tests
- `docs/` - repository documentation
- `hooks/hooks.json` - plugin-specific hook format (replaced by settings.json config)

## Output

Create converted files in a distribution directory (e.g., `dist/` or `portable/`) ready for users to copy.

## Implementation Steps

1. Create output directory structure
2. Copy and modify commands (remove prefixes)
3. Copy and modify session-start.sh (fix paths, remove legacy code)
4. Copy all skills, updating any cross-references
5. Copy agents directory
6. Create README.md with installation instructions
7. Test by copying to a fresh project's `.claude/` directory
