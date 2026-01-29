# Ultimate Claude Config

A comprehensive configuration framework for Claude Code that transforms Claude into a powerful project execution engine for solo developers.

## What's Included

| Component | Count | Description |
|-----------|-------|-------------|
| Agents | 12 | Specialized AI agents for different tasks |
| Commands | 21 | Executable workflow commands |
| Skills | 16 | Reusable knowledge modules |
| Rules | 8 | Behavioral guidelines |

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
```

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

## Workflow 3: Debug & Fix

Find and fix bugs systematically.

```
┌──────────────────────────────────────────────────────────────────┐
│  STEP 1: Analyze Issue                                           │
│  Command: /debug                                                 │
│                                                                  │
│  What happens:                                                   │
│  - Describe the bug/error                                        │
│  - Claude analyzes root cause                                    │
│  - Identifies affected code                                      │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 2: Apply Fix                                               │
│  (Claude implements the fix)                                     │
│                                                                  │
│  What happens:                                                   │
│  - Makes targeted code changes                                   │
│  - Preserves existing functionality                              │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 3: Add Tests                                               │
│  Command: /tdd                                                   │
│                                                                  │
│  What happens:                                                   │
│  - Writes tests covering the bug                                 │
│  - Ensures regression prevention                                 │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 4: Verify                                                  │
│  Command: /verify                                                │
│                                                                  │
│  What happens:                                                   │
│  - Runs all tests                                                │
│  - Confirms fix works                                            │
└──────────────────────────────────────────────────────────────────┘
```

---

## Workflow 4: Code Review & Quality

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

## Workflow 5: Refactoring

Clean up and improve existing code.

```
┌──────────────────────────────────────────────────────────────────┐
│  STEP 1: Analyze Code                                            │
│  Command: /refactor                                              │
│                                                                  │
│  What happens:                                                   │
│  - Identifies improvement opportunities                          │
│  - Suggests refactoring strategies                               │
│  - Preserves behavior                                            │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 2: Clean Dead Code (Optional)                              │
│  Command: /refactor-clean                                        │
│                                                                  │
│  What happens:                                                   │
│  - Finds unused code                                             │
│  - Removes dead imports                                          │
│  - Cleans up leftovers                                           │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 3: Verify No Regressions                                   │
│  Command: /tdd                                                   │
│                                                                  │
│  What happens:                                                   │
│  - Runs existing tests                                           │
│  - Ensures nothing broke                                         │
└──────────────────────────────────────────────────────────────────┘
```

---

## Workflow 6: Build Error Resolution

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

## Workflow 7: Test-Driven Development

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
│  STEP 3: Refactor (IMPROVE)                                      │
│  Command: /refactor                                              │
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

## Workflow 8: Save Progress & Learn

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
| Fix a bug | `/debug` |
| Review code | `/code-review` |
| Fix build errors | `/build-fix` |
| Run full verification | `/verify` |
| Check test coverage | `/test-coverage` |
| Run E2E tests | `/e2e` |
| Refactor code | `/refactor` |
| Map the codebase | `/update-codemaps` |

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
├─► Fix a bug
│   └─► /debug → fix → /tdd → /verify
│
├─► Review code quality
│   └─► /code-review → /test-coverage → /e2e
│
├─► Build is broken
│   └─► /build-fix
│
├─► Clean up code
│   └─► /refactor → /refactor-clean → /tdd
│
├─► Save progress
│   └─► /checkpoint → /learn
│
└─► Go-specific work
    └─► /go-build, /go-review, /go-test
```

---

## All Commands (21)

| Command | Description |
|---------|-------------|
| `/build-fix` | Fix TypeScript/JavaScript build errors |
| `/checkpoint` | Save and verify project checkpoints |
| `/code-review` | Comprehensive code review |
| `/debug` | Quick debugging checklist |
| `/e2e` | Run end-to-end tests |
| `/eval` | Eval-driven development workflow |
| `/go-build` | Fix Go build errors |
| `/go-review` | Go-specific code review |
| `/go-test` | Go TDD workflow |
| `/learn` | Extract reusable patterns from session |
| `/orchestrate` | Multi-agent workflow orchestration |
| `/plan` | Quick feature planning |
| `/refactor` | General code refactoring |
| `/refactor-clean` | Remove dead code |
| `/setup-pm` | Setup package manager |
| `/skill-create` | Create skills from git history |
| `/tdd` | Test-driven development |
| `/test-coverage` | Analyze test coverage |
| `/update-codemaps` | Update codebase documentation |
| `/update-docs` | Sync documentation from source |
| `/verify` | Automated build/lint/test verification |

---

## File Structure

```
.claude/
├── agents/                # 12 AI agent definitions
├── commands/              # 21 CLI commands
├── skills/                # 16 reusable knowledge modules
└── rules/                 # 8 behavioral guidelines
```

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
