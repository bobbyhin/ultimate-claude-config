# Ultimate Claude Config

A comprehensive configuration framework for Claude Code that transforms Claude into a powerful project execution engine for solo developers.

## What's Included

| Component | Count | Description |
|-----------|-------|-------------|
| Agents | 14 | Specialized AI agents for different tasks |
| Commands | 22 | Executable workflow commands |
| Skills | 18 | Reusable knowledge modules |
| Rules | 9 | Behavioral guidelines |

## Installation

```bash
# Clone the repo
git clone https://github.com/affaan-m/everything-claude-code.git

# Copy agents to your Claude config
cp everything-claude-code/agents/*.md ~/.claude/agents/

# Copy rules
cp everything-claude-code/rules/*.md ~/.claude/rules/

# Copy commands
cp everything-claude-code/commands/*.md ~/.claude/commands/

# Copy skills
cp -r everything-claude-code/skills/* ~/.claude/skills/

# Copy settings (enables Context7 MCP for up-to-date docs)
cp everything-claude-code/settings.json ~/.claude/settings.json
```

> **Note:** `settings.json` configures [Context7 MCP](https://github.com/upstash/context7) which gives Claude access to up-to-date library documentation. Requires `npx` (Node.js).

---

# Workflows

## Workflow 1: Plan & Build a Feature

Plan a new feature and implement it with tests.

```
┌──────────────────────────────────────────────────────────────────┐
│  STEP 1: Plan the Feature                                        │
│  Command: /plan                                                  │
│                                                                  │
│  What happens:                                                   │
│  - Describe what you want to build                               │
│  - Claude creates a structured plan                              │
│  - Identifies tasks, dependencies, risks                         │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 2: Write Tests First                                       │
│  Command: /tdd                                                   │
│                                                                  │
│  What happens:                                                   │
│  - Writes tests before implementation (RED)                      │
│  - Defines expected behavior                                     │
│  - Tests should fail initially                                   │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 3: Implement                                               │
│  (Claude writes the code)                                        │
│                                                                  │
│  What happens:                                                   │
│  - Implements minimal code to pass tests (GREEN)                 │
│  - Follows coding standards from rules/                          │
│  - Uses patterns from skills/                                    │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 4: Verify Everything                                       │
│  Command: /verify                                                │
│                                                                  │
│  What happens:                                                   │
│  - Runs build, lint, and tests                                   │
│  - Confirms everything passes                                    │
│  - Reports any issues                                            │
└──────────────────────────────────────────────────────────────────┘
```

---

## Workflow 2: Explore & Document Codebase

Understand and document an existing codebase.

```
┌──────────────────────────────────────────────────────────────────┐
│  STEP 1: Map the Codebase                                        │
│  Command: /update-codemaps                                       │
│                                                                  │
│  What happens:                                                   │
│  - Scans all source files                                        │
│  - Generates architecture documentation                          │
│  - Creates codemaps for backend, frontend, data                  │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 2: Update Documentation                                    │
│  Command: /update-docs                                           │
│                                                                  │
│  What happens:                                                   │
│  - Syncs docs with source code                                   │
│  - Detects stale documentation                                   │
│  - Generates updated API docs                                    │
└──────────────────────────────────────────────────────────────────┘
```

---

## Workflow 3: Code Review & Quality

Ensure code quality before committing.

```
┌──────────────────────────────────────────────────────────────────┐
│  STEP 1: Review Code                                             │
│  Command: /code-review                                           │
│                                                                  │
│  What happens:                                                   │
│  - Analyzes code for issues                                      │
│  - Checks patterns, security, performance                        │
│  - Provides actionable feedback                                  │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 2: Fix Issues                                              │
│  (Address review feedback)                                       │
│                                                                  │
│  What happens:                                                   │
│  - Apply suggested changes                                       │
│  - Refactor if needed                                            │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 3: Check Test Coverage                                     │
│  Command: /test-coverage                                         │
│                                                                  │
│  What happens:                                                   │
│  - Analyzes current coverage                                     │
│  - Identifies untested code                                      │
│  - Target: 80%+ coverage                                         │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 4: Run E2E Tests                                           │
│  Command: /e2e                                                   │
│                                                                  │
│  What happens:                                                   │
│  - Runs end-to-end tests                                         │
│  - Validates full user flows                                     │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
                         ✅ Ready to commit
```

---

## Workflow 4: Refactoring

Clean up and remove dead code safely.

```
┌──────────────────────────────────────────────────────────────────┐
│  STEP 1: Analyze Dead Code                                       │
│  Command: /refactor-clean                                        │
│                                                                  │
│  What happens:                                                   │
│  - Runs analysis tools (knip, depcheck, ts-prune)                │
│  - Generates report in .reports/dead-code-analysis.md            │
│  - Categorizes: SAFE / CAUTION / DANGER                          │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 2: Remove Dead Code                                        │
│  (Claude applies safe deletions)                                 │
│                                                                  │
│  What happens:                                                   │
│  - Deletes unused exports, files, dependencies                   │
│  - Runs tests before and after each deletion                     │
│  - Rolls back if tests fail                                      │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 3: Verify No Regressions                                   │
│  Command: /verify                                                │
│                                                                  │
│  What happens:                                                   │
│  - Runs full test suite                                          │
│  - Confirms nothing broke                                        │
└──────────────────────────────────────────────────────────────────┘
```

---

## Workflow 5: Build Error Resolution

Fix build failures quickly.

```
┌──────────────────────────────────────────────────────────────────┐
│  STEP 1: Diagnose Build Error                                    │
│  Command: /build-fix                                             │
│                                                                  │
│  What happens:                                                   │
│  - Analyzes build output                                         │
│  - Identifies root cause                                         │
│  - Proposes fixes                                                │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 2: Apply Fixes                                             │
│  (Claude implements fixes)                                       │
│                                                                  │
│  What happens:                                                   │
│  - Fixes type errors                                             │
│  - Resolves missing dependencies                                 │
│  - Corrects syntax issues                                        │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 3: Verify Build                                            │
│  (Claude runs build again)                                       │
│                                                                  │
│  What happens:                                                   │
│  - Confirms build passes                                         │
│  - Checks for new errors                                         │
└──────────────────────────────────────────────────────────────────┘
```

---

## Workflow 6: Test-Driven Development

Build features with tests first.

```
┌──────────────────────────────────────────────────────────────────┐
│  STEP 1: Write Failing Tests (RED)                               │
│  Command: /tdd                                                   │
│                                                                  │
│  What happens:                                                   │
│  - Define expected behavior in tests                             │
│  - Run tests - they should FAIL                                  │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 2: Write Minimal Implementation (GREEN)                    │
│  (Claude writes just enough code)                                │
│                                                                  │
│  What happens:                                                   │
│  - Implements minimum to pass tests                              │
│  - Run tests - they should PASS                                  │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 3: Clean Up (IMPROVE)                                      │
│  Command: /refactor-clean                                        │
│                                                                  │
│  What happens:                                                   │
│  - Clean up implementation                                       │
│  - Improve naming, structure                                     │
│  - Tests still pass                                              │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 4: Check Coverage                                          │
│  Command: /test-coverage                                         │
│                                                                  │
│  What happens:                                                   │
│  - Verifies 80%+ coverage                                        │
│  - Identifies gaps                                               │
└──────────────────────────────────────────────────────────────────┘
```

---

## Workflow 7: Save Progress & Learn

Capture knowledge from your work session.

```
┌──────────────────────────────────────────────────────────────────┐
│  STEP 1: Save Checkpoint                                         │
│  Command: /checkpoint                                            │
│                                                                  │
│  What happens:                                                   │
│  - Saves current project state                                   │
│  - Records what was accomplished                                 │
│  - Creates restore point                                         │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 2: Extract Learnings                                       │
│  Command: /learn                                                 │
│                                                                  │
│  What happens:                                                   │
│  - Extracts reusable patterns from session                       │
│  - Updates instinct files                                        │
│  - Improves future performance                                   │
└──────────────────────────────────────────────────────────────────┘
```

---

# Quick Reference

## Most Used Commands

| When you want to... | Use this command |
|---------------------|------------------|
| Plan a feature | `/plan` |
| Write tests first | `/tdd` |
| Review code | `/code-review` |
| Fix build errors | `/build-fix` |
| Run full verification | `/verify` |
| Check test coverage | `/test-coverage` |
| Run E2E tests | `/e2e` |
| Clean up code | `/refactor-clean` |
| Map the codebase | `/update-codemaps` |
| Fix Python errors | `/py-fix` |
| Review Python code | `/py-review` |
| Python TDD | `/py-test` |
| Fix Go build errors | `/go-build` |
| Review Go code | `/go-review` |
| Go TDD | `/go-test` |

## Decision Tree

```
What do you need to do?
│
├─► Build a new feature
│   └─► /plan → /tdd → implement → /verify
│
├─► Understand existing code
│   └─► /update-codemaps → /update-docs
│
├─► Review code quality
│   └─► /code-review → /test-coverage → /e2e
│
├─► Build is broken
│   └─► /build-fix
│
├─► Clean up code
│   └─► /refactor-clean → /verify
│
├─► Save progress
│   └─► /checkpoint → /learn
│
├─► Python-specific work
│   └─► /py-fix, /py-review, /py-test
│
└─► Go-specific work
    └─► /go-build, /go-review, /go-test
```

---

# Component Reference

## All Commands (22)

| Command | Description |
|---------|-------------|
| `/build-fix` | Fix TypeScript/JavaScript build errors |
| `/checkpoint` | Save and verify project checkpoints |
| `/code-review` | Comprehensive code review |
| `/e2e` | Run end-to-end tests |
| `/eval` | Eval-driven development workflow |
| `/go-build` | Fix Go build errors |
| `/go-review` | Go-specific code review |
| `/go-test` | Go TDD workflow |
| `/learn` | Extract reusable patterns from session |
| `/orchestrate` | Multi-agent workflow orchestration |
| `/plan` | Quick feature planning |
| `/py-fix` | Fix Python ruff/pyright/runtime errors |
| `/py-review` | Python/FastAPI code review |
| `/py-test` | Python TDD with pytest |
| `/refactor-clean` | Remove dead code safely with analysis tools |
| `/setup-pm` | Setup package manager |
| `/skill-create` | Create skills from git history |
| `/tdd` | Test-driven development |
| `/test-coverage` | Analyze test coverage |
| `/update-codemaps` | Update codebase documentation |
| `/update-docs` | Sync documentation from source |
| `/verify` | Automated build/lint/test verification |

## All Agents (14)

| Agent | Description |
|-------|-------------|
| `architect` | System design, scalability, and technical decisions |
| `build-error-resolver` | Fix build/TypeScript errors with minimal diffs |
| `code-reviewer` | Code quality, security, and maintainability review |
| `database-reviewer` | PostgreSQL query optimization and schema design |
| `doc-updater` | Documentation and codemap generation |
| `e2e-runner` | End-to-end testing with browser automation |
| `go-build-resolver` | Go build and compilation error resolution |
| `go-reviewer` | Idiomatic Go review, concurrency, and error handling |
| `planner` | Complex feature and refactoring planning |
| `py-error-resolver` | Fix Python ruff/pyright/runtime errors with minimal changes |
| `py-reviewer` | Python/FastAPI code review for patterns and security |
| `refactor-cleaner` | Dead code cleanup and consolidation |
| `security-reviewer` | OWASP Top 10 vulnerability detection |
| `tdd-guide` | Test-driven development with 80%+ coverage |

## All Skills (18)

| Skill | Description |
|-------|-------------|
| `backend-patterns` | Node.js/Express/Next.js API design and optimization |
| `clickhouse-io` | ClickHouse analytics and data engineering patterns |
| `coding-standards` | TypeScript/JavaScript/React coding best practices |
| `continuous-learning-v2` | Instinct-based learning with confidence scoring |
| `eval-harness` | Eval-driven development (EDD) framework |
| `frontend-patterns` | React/Next.js UI and state management patterns |
| `golang-patterns` | Idiomatic Go patterns and conventions |
| `golang-testing` | Go table-driven tests, benchmarks, and fuzzing |
| `iterative-retrieval` | Progressive context retrieval for subagents |
| `postgres-patterns` | PostgreSQL optimization based on Supabase practices |
| `project-guidelines-example` | Template for project-specific skill creation |
| `python-patterns` | FastAPI, Pydantic v2, async, uv, ruff, pyright patterns |
| `python-testing` | pytest fixtures, parametrize, async testing, coverage |
| `security-review` | Authentication, input handling, and secrets checklist |
| `session-start-hook` | Startup hooks for Claude Code web sessions |
| `strategic-compact` | Manual context compaction at logical intervals |
| `tdd-workflow` | TDD methodology with 80%+ coverage target |
| `verification-loop` | Comprehensive verification system for sessions |

## All Rules (9)

| Rule | Description |
|------|-------------|
| `agents` | Agent orchestration and management guidelines |
| `coding-style` | Immutability-first coding style |
| `git-workflow` | Commit message format and version control standards |
| `hooks` | Hook types and PreToolUse validation |
| `patterns` | API response format and implementation patterns |
| `performance` | Model selection strategy for cost efficiency |
| `project-detection` | Auto-detect project type and select correct toolchain |
| `security` | Mandatory security checks before commits |
| `testing` | Minimum 80% coverage with required test types |

---

## File Structure

```
.claude/
├── agents/                # 14 AI agent definitions
├── commands/              # 22 CLI commands
├── skills/                # 18 reusable knowledge modules
├── rules/                 # 9 behavioral guidelines
├── settings.json          # MCP server config (Context7)
├── CLAUDE-TEMPLATE.md     # Project README template
└── README.md              # This documentation
```

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
