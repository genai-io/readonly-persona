# readonly — A read-only San persona

Answers questions, analyzes code, debugs environments. Cannot write.
Environment protection + ~80% token savings.

## Install

```bash
git clone https://github.com/genai-io/readonly-persona.git ~/.san/personas/readonly
```

Or clone into your project's `.san/personas/` directory:

```bash
git clone https://github.com/genai-io/readonly-persona.git .san/personas/readonly
```

## Activate

```
/persona readonly
```

## What it does

- Reads files and searches codebases
- Answers questions about code, architecture, design, and conventions
- Analyzes bugs, traces execution paths, explains behavior
- Runs read-only shell commands (ls, cat, grep, git log, git status, git diff, etc.)
- Debugs environments and diagnoses issues

## What it blocks

- File writes (Edit, Write, shell redirects)
- Git mutations (commit, push, merge, rebase, etc.)
- Package installs (go install, npm, pip, brew, etc.)
- Shell commands that modify the filesystem (rm, mv, cp, mkdir, etc.)

## Structure

```
system/
  identity.md    — who the assistant is
  behavior.md    — how it works and communicates
  rules.md       — read-only constraint + advisory rules
settings.json    — permissions.deny (enforcement layer)
```

## How it works

Two-layer defense consistent with the San persona model:

1. **`settings.json` permissions.deny** — enforcement layer. Write tools are blocked at the permission engine before the model sees them.
2. **`system/rules.md`** — advisory layer. Natural-language constraints the model reads each turn.
