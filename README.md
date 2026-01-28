# Ultimate Claude Config

A comprehensive configuration framework for Claude Code that transforms Claude into a powerful project execution engine for solo developers.

## Overview

Ultimate Claude Config provides:
- **23 Specialized Agents** - AI agents for different development tasks
- **55 Commands** - Executable commands for workflow automation
- **17 Skills** - Reusable knowledge modules
- **8 Rules** - Behavioral guidelines
- **GSD Framework** - "Get Shit Done" project lifecycle management

## Installation

Copy the entire configuration to your project's `.claude/` directory:

```bash
cp -r agents commands skills rules hooks get-shit-done settings.json /path/to/your-project/.claude/
```

## Quick Start

### Starting a New Project

```bash
# 1. Initialize project with deep context gathering
/gsd:new-project

# 2. Plan the first phase
/gsd:plan-phase 1

# 3. Execute the plan
/gsd:execute-phase

# 4. Verify the work
/gsd:verify-work
```

### Working with Existing Codebase

```bash
# 1. Map the existing codebase
/gsd:map-codebase

# 2. Initialize project
/gsd:new-project

# 3. Continue with normal workflow
```

## Use Cases

### 1. New Project Development

Full project lifecycle from idea to deployment.

```
/gsd:new-project → /gsd:plan-phase → /gsd:execute-phase → /gsd:verify-work
```

### 2. Brownfield Development (Existing Codebase)

Work with existing code while maintaining structure.

```
/gsd:map-codebase → /gsd:new-project → (normal workflow)
```

### 3. Quick Tasks

Small tasks that don't need full planning.

```
/gsd:quick
```

### 4. Debugging

Analyze and fix bugs with root cause analysis.

```
/debug
/gsd:debug
```

### 5. Build Error Resolution

Fix build failures automatically.

```
/build-fix
/go-build
```

### 6. Code Review

Get comprehensive code review feedback.

```
/code-review
/go-review
/review
```

### 7. Test-Driven Development

Write tests first, then implement.

```
/tdd
/test-coverage
/e2e
```

### 8. Refactoring

Clean up and improve code quality.

```
/refactor
/refactor-clean
```

### 9. Work Session Management

Pause and resume work with full context preservation.

```
# When stopping work
/gsd:pause-work

# When returning
/gsd:resume-work
```

### 10. Phase & Milestone Management

Manage project phases and milestones.

```
# Phases
/gsd:add-phase
/gsd:insert-phase
/gsd:remove-phase
/gsd:discuss-phase
/gsd:research-phase

# Milestones
/gsd:new-milestone
/gsd:complete-milestone
/gsd:audit-milestone
```

### 11. Documentation

Update and maintain documentation.

```
/docs
/update-docs
```

### 12. Learning System

Let Claude learn from your patterns.

```
/learn
/instinct-status
/instinct-export
/instinct-import
```

## Command Reference

### GSD Commands (Project Management)

| Command | Description |
|---------|-------------|
| `/gsd:new-project` | Initialize a new project with deep questioning |
| `/gsd:plan-phase [n]` | Create executable plan for phase n |
| `/gsd:execute-phase` | Execute the current phase plan |
| `/gsd:verify-work` | Verify completed work quality |
| `/gsd:progress` | Show project progress |
| `/gsd:quick` | Quick execution without full planning |
| `/gsd:pause-work` | Save state and pause work |
| `/gsd:resume-work` | Resume work with full context |
| `/gsd:map-codebase` | Map existing codebase structure |
| `/gsd:add-phase` | Add a new phase |
| `/gsd:insert-phase` | Insert phase at specific position |
| `/gsd:remove-phase` | Remove a phase |
| `/gsd:discuss-phase` | Discuss phase details |
| `/gsd:research-phase` | Deep research for phase |
| `/gsd:new-milestone` | Create new milestone |
| `/gsd:complete-milestone` | Mark milestone complete |
| `/gsd:audit-milestone` | Validate milestone |
| `/gsd:check-todos` | Check pending todos |
| `/gsd:add-todo` | Add a todo item |
| `/gsd:settings` | View/edit settings |
| `/gsd:help` | Get help |

### Development Commands

| Command | Description |
|---------|-------------|
| `/code-review` | Comprehensive code review |
| `/review` | Quick code review |
| `/go-review` | Go-specific code review |
| `/debug` | Debug assistance |
| `/fix` | Quick fixes |
| `/build-fix` | Fix build errors |
| `/go-build` | Build Go projects |
| `/go-test` | Test Go code |
| `/tdd` | Test-driven development |
| `/test-coverage` | Analyze test coverage |
| `/e2e` | Run E2E tests |
| `/refactor` | Refactor code |
| `/refactor-clean` | Clean dead code |
| `/docs` | Update documentation |
| `/update-docs` | Update documentation |
| `/checkpoint` | Save project checkpoint |
| `/plan` | General planning |
| `/orchestrate` | Multi-agent orchestration |

### Learning Commands

| Command | Description |
|---------|-------------|
| `/learn` | Enable learning mode |
| `/instinct-status` | View learned instincts |
| `/instinct-export` | Export instincts |
| `/instinct-import` | Import instincts |
| `/evolve` | Evolve the system |
| `/skill-create` | Create new skill |

## Agents

### GSD Agents

| Agent | Purpose |
|-------|---------|
| `gsd-planner` | Creates executable phase plans |
| `gsd-executor` | Executes planned phases |
| `gsd-verifier` | Validates work quality |
| `gsd-debugger` | Advanced debugging |
| `gsd-codebase-mapper` | Maps existing code |
| `gsd-phase-researcher` | Deep phase research |
| `gsd-project-researcher` | Project discovery |
| `gsd-plan-checker` | Validates plans |

### Development Agents

| Agent | Purpose |
|-------|---------|
| `code-reviewer` | Code review and quality |
| `go-reviewer` | Go-specific review |
| `security-reviewer` | Security analysis |
| `refactor-cleaner` | Dead code elimination |
| `build-error-resolver` | Build failure diagnosis |
| `architect` | System design |
| `tdd-guide` | TDD guidance |
| `doc-updater` | Documentation |
| `e2e-runner` | E2E test execution |
| `database-reviewer` | Database analysis |
| `planner` | Implementation planning |

## Skills

| Skill | Description |
|-------|-------------|
| `coding-standards` | Universal code quality practices |
| `tdd-workflow` | Test-driven development (80%+ coverage) |
| `verification-loop` | Quality verification patterns |
| `iterative-retrieval` | Context gathering |
| `backend-patterns` | Backend architecture |
| `frontend-patterns` | React/frontend practices |
| `golang-patterns` | Go language idioms |
| `golang-testing` | Go testing frameworks |
| `postgres-patterns` | PostgreSQL practices |
| `clickhouse-io` | ClickHouse patterns |
| `security-review` | Security analysis |
| `continuous-learning` | Session learning |
| `continuous-learning-v2` | Instinct-based learning |

## Workflows

### Standard Development Workflow

```
┌─────────────────────────────────────┐
│     1. /gsd:new-project             │  ← Gather context
└───────────────┬─────────────────────┘
                ▼
┌─────────────────────────────────────┐
│     2. /gsd:plan-phase              │  ← Break into tasks
└───────────────┬─────────────────────┘
                ▼
┌─────────────────────────────────────┐
│     3. /gsd:execute-phase           │  ← Implement
└───────────────┬─────────────────────┘
                ▼
┌─────────────────────────────────────┐
│     4. /gsd:verify-work             │  ← Quality check
└───────────────┬─────────────────────┘
                ▼
         ✅ Next phase or 🔄 Fix issues
```

### Code Quality Workflow

```
Develop → /code-review → Fix issues → /tdd → /gsd:verify-work → Commit
```

### Debugging Workflow

```
Issue → /debug → Analyze → Fix → /tdd → Verify
```

## Best Practices

1. **Always start with `/gsd:new-project`** - Ensures proper context gathering
2. **Use `/gsd:progress` frequently** - Track your progress
3. **Don't skip verification** - `/gsd:verify-work` catches bugs early
4. **Use `/gsd:quick` for small tasks** - No need for full planning
5. **Pause properly** - Use `/gsd:pause-work` to preserve context
6. **Review before committing** - Use `/code-review` or `/review`

## File Structure

```
.claude/
├── agents/                 # 23 AI agent definitions
├── commands/               # 55 CLI commands
│   └── gsd/               # GSD-specific commands
├── skills/                # 17 reusable knowledge modules
├── rules/                 # 8 behavioral guidelines
├── hooks/                 # Session lifecycle hooks
├── get-shit-done/         # GSD framework
│   ├── templates/         # Project templates
│   ├── references/        # Reference materials
│   └── workflows/         # Workflow definitions
└── settings.json          # Core configuration
```

## Key Files Generated by GSD

| File | Purpose |
|------|---------|
| `PROJECT.md` | Central project context |
| `ROADMAP.md` | Phase structure with milestones |
| `PLAN.md` | Current phase execution plan |
| `STATE.md` | Project state tracking |
| `CODEBASE.md` | Mapped codebase structure |

## Tips for Teams

1. **Share the `.claude/` folder** - Everyone uses the same config
2. **Keep `PROJECT.md` updated** - Central source of truth
3. **Use consistent commands** - Follow the same workflows
4. **Export/import instincts** - Share learned patterns

## Troubleshooting

### Lost Context?
```
/gsd:resume-work
```

### Need to see progress?
```
/gsd:progress
```

### Build failing?
```
/build-fix
```

### Need help?
```
/gsd:help
```

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
