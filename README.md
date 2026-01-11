# Cursor Planning with Files

> **Manus-style file-based planning for Cursor IDE & Agent**

A Cursor rules adaptation of [planning-with-files](https://github.com/OthmanAdi/planning-with-files) — the workflow pattern behind Manus AI's $2B acquisition.

[![Version](https://img.shields.io/badge/version-1.1.0-blue.svg)](#changelog)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Cursor Rules](https://img.shields.io/badge/Cursor-Rules-purple)](https://docs.cursor.com/context/rules-for-ai)

## What is This?

This project brings the **"planning with files"** methodology to Cursor IDE and Cursor Agent. Instead of relying on volatile context, you use persistent markdown files as your AI's "working memory on disk."

### Works With All Cursor Modes

| Mode | Supported |
|------|-----------|
| **Cursor Chat** (Cmd+L) | ✅ |
| **Cursor Agent** (agentic mode) | ✅ |
| **Inline Edit** (Cmd+K) | ✅ |
| **Composer** | ✅ |

**Cursor Agent benefits the most** from this pattern — it makes many autonomous tool calls and is prone to goal drift without persistent planning.

### The Core Principle

```
Context Window = RAM (volatile, limited)
Filesystem = Disk (persistent, unlimited)

→ Anything important gets written to disk.
```

## Quick Install

```bash
# Clone this repo
git clone https://github.com/grantchen08/cursor-planning-with-files.git

# Copy rules to your project
cp -r cursor-planning-with-files/.cursor YOUR_PROJECT/
```

Or manually copy `.cursor/rules/planning-with-files.mdc` to your project.

## The 3-File Pattern

For complex tasks, create these files in your project root:

| File | Purpose | When to Update |
|------|---------|----------------|
| `task_plan.md` | Phases, progress, decisions, errors | After each phase |
| `findings.md` | Research, discoveries, requirements | After ANY discovery |
| `progress.md` | Session log, test results | Throughout session |

Templates are provided in the `templates/` directory.

## Key Rules

1. **Create Plan First** — Never start complex tasks without `task_plan.md`
2. **The 2-Action Rule** — After every 2 view/search operations, save findings to files
3. **Read Before Decide** — Re-read the plan before major decisions
4. **Log ALL Errors** — Every error goes in the plan file with attempt number
5. **Never Repeat Failures** — Track attempts, mutate approach

## Cursor vs Claude Code

| Feature | Claude Code | Cursor |
|---------|-------------|--------|
| Core 3-file pattern | ✅ | ✅ |
| Templates | ✅ | ✅ |
| Planning rules | ✅ | ✅ |
| SessionStart hook | ✅ | ❌ |
| PreToolUse hook | ✅ | ❌ |
| PostToolUse hook | ✅ | ❌ |
| Stop hook | ✅ | ❌ |

Since Cursor doesn't support hooks, the workflow is **manual** — you may need to remind the AI to create/update planning files, or it will proactively suggest it based on the rules.

## Usage

Once the rules are installed, for complex tasks:

1. Ask the AI to "create planning files" or "use the planning pattern"
2. The AI will create `task_plan.md`, `findings.md`, and `progress.md`
3. Periodically ask to "re-read the plan" to keep goals in focus
4. After phases complete, ask to "update the task plan"

Or the AI may proactively suggest using the pattern when it detects a multi-step task.

## File Structure

```
cursor-planning-with-files/
├── .cursor/
│   └── rules/
│       └── planning-with-files.mdc   # The Cursor rules file
├── templates/
│   ├── task_plan.md                  # Phase tracking template
│   ├── findings.md                   # Research storage template
│   └── progress.md                   # Session logging template
├── LICENSE
└── README.md
```

## Credits

This project is a Cursor adaptation of [planning-with-files](https://github.com/OthmanAdi/planning-with-files) by [Ahmad Adi](https://github.com/OthmanAdi).

The methodology is based on [Context Engineering for AI Agents](https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus) from Manus AI.

## Changelog

### v1.1.0 (2026-01-11)

- **Added:** Self-Evolution section for upstreaming improvements back to this repo
  - Guidelines on when to upstream (new anti-patterns, better heuristics, missing guidance)
  - What makes a good upstream candidate vs. project-specific customization
  - Step-by-step instructions for forking, committing, and creating PRs
  - Upstream checklist to ensure quality contributions

### v1.0.0 (Initial Release)

- Core 3-file pattern (`task_plan.md`, `findings.md`, `progress.md`)
- Critical rules (Create Plan First, 2-Action Rule, Read Before Decide, etc.)
- 3-Strike Error Protocol
- Read vs Write Decision Matrix
- 5-Question Reboot Test
- Anti-patterns guide
- Task Plan Template

## Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

See the **Self-Evolution** section in the [rules file](.cursor/rules/planning-with-files.mdc) for guidelines on what makes a good contribution.

## License

MIT License — see [LICENSE](LICENSE) for details.
