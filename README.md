# Ultimate Claude Config

A comprehensive configuration framework for Claude Code that transforms Claude into a powerful project execution engine for solo developers.

## What's Included

| Component | Count | Description |
|-----------|-------|-------------|
| Agents | 23 | Specialized AI agents for different tasks |
| Commands | 48 | Executable workflow commands |
| Skills | 16 | Reusable knowledge modules |
| Rules | 8 | Behavioral guidelines |

## Installation

```bash
cp -r agents commands skills rules hooks get-shit-done settings.json /path/to/your-project/.claude/
```

---

# Workflows

## Workflow 1: New Project (Greenfield)

Start a brand new project from scratch.

```
┌──────────────────────────────────────────────────────────────────┐
│  STEP 1: Initialize Project                                       │
│  Command: /gsd:new-project                                        │
│                                                                   │
│  What happens:                                                    │
│  - Claude asks deep questions about your project                  │
│  - Gathers requirements, constraints, tech stack                  │
│  - Creates PROJECT.md (context) and ROADMAP.md (phases)          │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 2: Plan First Phase                                         │
│  Command: /gsd:plan-phase 1                                       │
│                                                                   │
│  What happens:                                                    │
│  - Breaks phase into concrete tasks                               │
│  - Identifies dependencies                                        │
│  - Creates PLAN.md with executable steps                          │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 3: Execute Phase                                            │
│  Command: /gsd:execute-phase                                      │
│                                                                   │
│  What happens:                                                    │
│  - Claude works through each task in PLAN.md                      │
│  - Writes code, creates files, runs tests                         │
│  - Updates STATE.md with progress                                 │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 4: Verify Work                                              │
│  Command: /gsd:verify-work                                        │
│                                                                   │
│  What happens:                                                    │
│  - Checks all tasks completed                                     │
│  - Runs tests, validates quality                                  │
│  - Creates verification report                                    │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
                    ┌─────────┴─────────┐
                    │                   │
                    ▼                   ▼
              ✅ PASSED            ❌ FAILED
                    │                   │
                    ▼                   ▼
          /gsd:plan-phase 2      Fix issues, then
          (next phase)           /gsd:verify-work again
```

---

## Workflow 2: Existing Codebase (Brownfield)

Work with a project that already has code.

```
┌──────────────────────────────────────────────────────────────────┐
│  STEP 1: Map Existing Codebase                                    │
│  Command: /gsd:map-codebase                                       │
│                                                                   │
│  What happens:                                                    │
│  - Scans all existing code                                        │
│  - Documents architecture, patterns, conventions                  │
│  - Creates CODEBASE.md with full structure                        │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 2: Initialize Project Context                               │
│  Command: /gsd:new-project                                        │
│                                                                   │
│  What happens:                                                    │
│  - Uses CODEBASE.md as reference                                  │
│  - Asks about new features/changes needed                         │
│  - Creates PROJECT.md and ROADMAP.md                              │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
                   Continue with Steps 2-4
                   from Workflow 1
```

---

## Workflow 3: Quick Task

Small tasks that don't need full planning.

```
┌──────────────────────────────────────────────────────────────────┐
│  SINGLE STEP                                                      │
│  Command: /gsd:quick                                              │
│                                                                   │
│  What happens:                                                    │
│  - Describe what you need                                         │
│  - Claude executes immediately                                    │
│  - No planning overhead                                           │
│                                                                   │
│  Best for:                                                        │
│  - Small bug fixes                                                │
│  - Minor feature additions                                        │
│  - Quick refactors                                                │
│  - One-off tasks                                                  │
└──────────────────────────────────────────────────────────────────┘
```

---

## Workflow 4: Debug & Fix

Find and fix bugs systematically.

```
┌──────────────────────────────────────────────────────────────────┐
│  STEP 1: Analyze Issue                                            │
│  Command: /debug                                                  │
│                                                                   │
│  What happens:                                                    │
│  - Describe the bug/error                                         │
│  - Claude analyzes root cause                                     │
│  - Identifies affected code                                       │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 2: Apply Fix                                                │
│  (Claude implements the fix)                                      │
│                                                                   │
│  What happens:                                                    │
│  - Makes targeted code changes                                    │
│  - Preserves existing functionality                               │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 3: Add Tests                                                │
│  Command: /tdd                                                    │
│                                                                   │
│  What happens:                                                    │
│  - Writes tests covering the bug                                  │
│  - Ensures regression prevention                                  │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 4: Verify                                                   │
│  Command: /gsd:verify-work                                        │
│                                                                   │
│  What happens:                                                    │
│  - Runs all tests                                                 │
│  - Confirms fix works                                             │
└──────────────────────────────────────────────────────────────────┘
```

---

## Workflow 5: Code Review & Quality

Ensure code quality before committing.

```
┌──────────────────────────────────────────────────────────────────┐
│  STEP 1: Review Code                                              │
│  Command: /code-review                                            │
│                                                                   │
│  What happens:                                                    │
│  - Analyzes code for issues                                       │
│  - Checks patterns, security, performance                         │
│  - Provides actionable feedback                                   │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 2: Fix Issues                                               │
│  (Address review feedback)                                        │
│                                                                   │
│  What happens:                                                    │
│  - Apply suggested changes                                        │
│  - Refactor if needed                                             │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 3: Check Test Coverage                                      │
│  Command: /test-coverage                                          │
│                                                                   │
│  What happens:                                                    │
│  - Analyzes current coverage                                      │
│  - Identifies untested code                                       │
│  - Target: 80%+ coverage                                          │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 4: Run E2E Tests                                            │
│  Command: /e2e                                                    │
│                                                                   │
│  What happens:                                                    │
│  - Runs end-to-end tests                                          │
│  - Validates full user flows                                      │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
                         ✅ Ready to commit
```

---

## Workflow 6: Work Session Management

Pause and resume work without losing context.

```
┌──────────────────────────────────────────────────────────────────┐
│  PAUSING WORK                                                     │
│  Command: /gsd:pause-work                                         │
│                                                                   │
│  What happens:                                                    │
│  - Saves current state to STATE.md                                │
│  - Records what was in progress                                   │
│  - Notes next steps needed                                        │
│  - Creates CONTINUE-HERE.md with context                          │
└──────────────────────────────────────────────────────────────────┘

                    ... time passes ...

┌──────────────────────────────────────────────────────────────────┐
│  RESUMING WORK                                                    │
│  Command: /gsd:resume-work                                        │
│                                                                   │
│  What happens:                                                    │
│  - Loads saved state                                              │
│  - Restores full context                                          │
│  - Shows where you left off                                       │
│  - Ready to continue immediately                                  │
└──────────────────────────────────────────────────────────────────┘
```

---

## Workflow 7: Refactoring

Clean up and improve existing code.

```
┌──────────────────────────────────────────────────────────────────┐
│  STEP 1: Analyze Code                                             │
│  Command: /refactor                                               │
│                                                                   │
│  What happens:                                                    │
│  - Identifies improvement opportunities                           │
│  - Suggests refactoring strategies                                │
│  - Preserves behavior                                             │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 2: Clean Dead Code (Optional)                               │
│  Command: /refactor-clean                                         │
│                                                                   │
│  What happens:                                                    │
│  - Finds unused code                                              │
│  - Removes dead imports                                           │
│  - Cleans up leftovers                                            │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 3: Verify No Regressions                                    │
│  Command: /tdd                                                    │
│                                                                   │
│  What happens:                                                    │
│  - Runs existing tests                                            │
│  - Ensures nothing broke                                          │
└──────────────────────────────────────────────────────────────────┘
```

---

## Workflow 8: Build Error Resolution

Fix build failures quickly.

```
┌──────────────────────────────────────────────────────────────────┐
│  STEP 1: Diagnose Build Error                                     │
│  Command: /build-fix                                              │
│                                                                   │
│  What happens:                                                    │
│  - Analyzes build output                                          │
│  - Identifies root cause                                          │
│  - Proposes fixes                                                 │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 2: Apply Fixes                                              │
│  (Claude implements fixes)                                        │
│                                                                   │
│  What happens:                                                    │
│  - Fixes type errors                                              │
│  - Resolves missing dependencies                                  │
│  - Corrects syntax issues                                         │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  STEP 3: Verify Build                                             │
│  (Claude runs build again)                                        │
│                                                                   │
│  What happens:                                                    │
│  - Confirms build passes                                          │
│  - Checks for new errors                                          │
└──────────────────────────────────────────────────────────────────┘
```

---

## Workflow 9: Phase & Milestone Management

Manage larger project structures.

```
┌──────────────────────────────────────────────────────────────────┐
│  ADDING PHASES                                                    │
│                                                                   │
│  /gsd:add-phase      → Add phase at the end                       │
│  /gsd:insert-phase   → Insert at specific position                │
│  /gsd:remove-phase   → Remove a phase                             │
└──────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────┐
│  RESEARCHING PHASES                                               │
│                                                                   │
│  /gsd:research-phase → Deep research before planning              │
│  /gsd:discuss-phase  → Discuss details and assumptions            │
└──────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────┐
│  MILESTONE WORKFLOW                                               │
│                                                                   │
│  /gsd:new-milestone       → Create milestone grouping phases      │
│  /gsd:audit-milestone     → Check milestone progress              │
│  /gsd:complete-milestone  → Mark milestone done                   │
└──────────────────────────────────────────────────────────────────┘
```

---

## Workflow 10: Progress Tracking

Monitor your project status.

```
┌──────────────────────────────────────────────────────────────────┐
│  CHECK PROGRESS                                                   │
│  Command: /gsd:progress                                           │
│                                                                   │
│  Shows:                                                           │
│  - Current phase and status                                       │
│  - Completed vs remaining tasks                                   │
│  - Milestone progress                                             │
│  - Overall project health                                         │
└──────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────┐
│  TASK MANAGEMENT                                                  │
│                                                                   │
│  /gsd:check-todos  → View pending tasks                           │
│  /gsd:add-todo     → Add a new task                               │
└──────────────────────────────────────────────────────────────────┘
```

---

# Quick Reference

## Most Used Commands

| When you want to... | Use this command |
|---------------------|------------------|
| Start a new project | `/gsd:new-project` |
| Plan next phase | `/gsd:plan-phase [n]` |
| Do the work | `/gsd:execute-phase` |
| Check quality | `/gsd:verify-work` |
| Quick small task | `/gsd:quick` |
| See progress | `/gsd:progress` |
| Fix a bug | `/debug` |
| Review code | `/code-review` |
| Take a break | `/gsd:pause-work` |
| Come back | `/gsd:resume-work` |

## Files Generated

| File | Purpose | When Created |
|------|---------|--------------|
| `PROJECT.md` | Project context & requirements | `/gsd:new-project` |
| `ROADMAP.md` | All phases & milestones | `/gsd:new-project` |
| `PLAN.md` | Current phase tasks | `/gsd:plan-phase` |
| `STATE.md` | Current project state | Throughout |
| `CODEBASE.md` | Existing code map | `/gsd:map-codebase` |

## Decision Tree

```
What do you need to do?
│
├─► Start new project
│   └─► /gsd:new-project
│
├─► Work on existing project
│   ├─► First time? → /gsd:map-codebase → /gsd:new-project
│   └─► Already set up? → /gsd:resume-work
│
├─► Small quick task
│   └─► /gsd:quick
│
├─► Fix a bug
│   └─► /debug
│
├─► Review code quality
│   └─► /code-review → /tdd → /gsd:verify-work
│
├─► Build is broken
│   └─► /build-fix
│
├─► Need to stop working
│   └─► /gsd:pause-work
│
└─► Check where I am
    └─► /gsd:progress
```

---

## File Structure

```
.claude/
├── agents/                 # 23 AI agent definitions
├── commands/               # 48 CLI commands
│   └── gsd/               # GSD-specific commands
├── skills/                # 16 reusable knowledge modules
├── rules/                 # 8 behavioral guidelines
├── hooks/                 # Session lifecycle hooks
├── get-shit-done/         # GSD framework
│   ├── templates/         # Project templates
│   ├── references/        # Reference materials
│   └── workflows/         # Workflow definitions
└── settings.json          # Core configuration
```

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
