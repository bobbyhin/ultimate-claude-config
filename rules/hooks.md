# Hooks System

## Hook Types

- **PreToolUse**: Before tool execution (validation, parameter modification)
- **PostToolUse**: After tool execution (auto-format, checks)
- **Stop**: When session ends (final verification)

## Current Hooks (in ~/.claude/settings.json)

### PreToolUse
- **tmux reminder**: Suggests tmux for long-running commands (npm, pnpm, yarn, cargo, uv, go, etc.)
- **git push review**: Opens editor for review before push
- **doc blocker**: Blocks creation of unnecessary .md/.txt files

### PostToolUse
- **PR creation**: Logs PR URL and GitHub Actions status
- **Auto-format**: Formats files after edit
  - TypeScript/JavaScript: Prettier
  - Python: `ruff format`
  - Go: `gofmt`
- **Type check**: Runs type checker after editing source files
  - TypeScript: `tsc` on .ts/.tsx files
  - Python: `pyright` on .py files
  - Go: `go vet` on .go files
- **Debug statement warning**: Warns about debug statements in edited files
  - TypeScript/JavaScript: `console.log`
  - Python: `print()`, `breakpoint()`
  - Go: `fmt.Println`

### Stop
- **Debug statement audit**: Checks all modified files for debug statements before session ends

## Auto-Accept Permissions

Use with caution:
- Enable for trusted, well-defined plans
- Disable for exploratory work
- Never use dangerously-skip-permissions flag
- Configure `allowedTools` in `~/.claude.json` instead

## TodoWrite Best Practices

Use TodoWrite tool to:
- Track progress on multi-step tasks
- Verify understanding of instructions
- Enable real-time steering
- Show granular implementation steps

Todo list reveals:
- Out of order steps
- Missing items
- Extra unnecessary items
- Wrong granularity
- Misinterpreted requirements
