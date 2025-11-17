# SDD Command Reference

Quick reference for all Spec-Kit slash commands.

## Core Workflow Commands

### Greenfield (New Projects)

| Command | Purpose | When to Use | Generates |
|---------|---------|-------------|-----------|
| `/speckit.constitution` | Define project principles | After `specify init`, before first feature | `.speckit/constitution.md` |
| `/speckit.specify` | Define feature requirements | After constitution, for each new feature | `.speckit/features/NNN-name/specify.md` |
| `/speckit.plan` | Create technical plan | After specify | `.speckit/features/NNN-name/plan.md` |
| `/speckit.tasks` | Break down into tasks | After plan | `.speckit/features/NNN-name/tasks.md` |
| `/speckit.implement` | Execute implementation | After tasks | Working code |

**Typical greenfield flow**:
```bash
specify init my-project --ai claude
# Then in AI agent:
/speckit.constitution
/speckit.specify
/speckit.plan
/speckit.tasks
/speckit.implement
```

---

### Brownfield (Existing Projects)

| Command | Purpose | When to Use | Generates |
|---------|---------|-------------|-----------|
| `/speckit.brownfield` | Analyze existing codebase | Before init, to understand current state | Analysis report |
| `/speckit.analyze-codebase` | Generate constitution from code | After `specify init --here` | `.speckit/constitution.md` |
| `/speckit.reverse-engineer` | Document existing features | After constitution, to document legacy code | Specs for existing features |
| `/speckit.integration-plan` | Plan integration with existing code | After specify, before tasks | Integration strategy |

**Typical brownfield flow**:
```bash
# In existing project directory:
/speckit.brownfield              # Analyze first
specify init --here --force      # Initialize in current dir
/speckit.analyze-codebase        # Generate constitution
/speckit.specify                 # New feature spec
/speckit.integration-plan        # How it integrates
/speckit.tasks                   # Break down (includes integration tasks)
/speckit.implement               # Execute
```

---

## Optional Enhancement Commands

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `/speckit.clarify` | Identify ambiguous requirements | After specify, before plan |
| `/speckit.analyze` | Check consistency & coverage | After tasks, before implement |
| `/speckit.checklist` | Generate quality checklists | Any time for validation |

---

## Validation Commands

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `/speckit.validate-reverse-engineering` | Verify reverse-engineered specs | After reverse-engineer (brownfield) |
| `/speckit.coverage-check` | Check documentation coverage | After reverse-engineer (brownfield) |
| `/speckit.validate-constitution` | Verify constitution consistency | After any constitution generation |
| `/speckit.trace [feature]` | Map specs to code | After implementation |

---

## Feature Management Commands

These are natural language interactions, not slash commands:

| Action | What to Say | Effect |
|--------|-------------|--------|
| Add feature | "Add a new feature for [description]" | Adds to feature pipeline |
| Reorder | "Move [feature-x] before [feature-y]" | Reorders pipeline |
| Remove | "Remove [feature-name]" | Removes from pipeline |
| Show status | "Show feature status" or "What's the progress?" | Displays dashboard |
| Switch feature | "Let's work on [feature-name] next" | Changes active feature |

---

## CLI Commands (Not Slash Commands)

These are terminal commands, not AI agent commands:

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `specify init [project] --ai [agent]` | Initialize new project | Starting new greenfield project |
| `specify init --here --force --ai [agent]` | Initialize in existing dir | Starting brownfield in existing project |
| `specify check` | Verify installation | After installing specify-cli |
| `uv tool install specify-cli --from git+https://github.com/github/spec-kit.git` | Install specify-cli | Initial setup |

---

## Command Arguments

### Common Arguments

**AI Agent Selection** (`--ai [agent]`):
- `--ai claude` - Claude Code
- `--ai copilot` - GitHub Copilot
- `--ai cursor` - Cursor
- `--ai windsurf` - Windsurf
- `--ai gemini` - Gemini CLI
- (See full list in installation guide)

**Initialization Flags**:
- `--here` - Initialize in current directory (don't create subdirectory)
- `--force` - Override warnings about existing files
- `--ai [agent]` - Specify which AI agent you're using

---

## Command Aliases

Some commands have shorter aliases:

| Full Command | Alias | Notes |
|--------------|-------|-------|
| `/speckit.constitution` | `/constitution` | If configured |
| `/speckit.specify` | `/specify` | If configured |
| `/speckit.plan` | `/plan` | If configured |
| `/speckit.tasks` | `/tasks` | If configured |
| `/speckit.implement` | `/implement` | If configured |

**Note**: Aliases depend on your AI agent's configuration. Use full `/speckit.*` commands if unsure.

---

## Command Chaining

You can sometimes chain commands by providing explicit instructions:

```
/speckit.specify Create a user authentication feature with OAuth2 support

# Then immediately:
/speckit.plan Use JWT tokens, Passport.js, and PostgreSQL for user storage
```

However, **best practice** is to wait for each command to complete, review the generated artifact, and then proceed to the next step.

---

## Error Recovery Commands

If something goes wrong:

| Problem | Solution |
|---------|----------|
| Command not recognized | Verify `specify init` was run, restart AI agent |
| Artifacts not generated | Check `.speckit/` directory exists, verify write permissions |
| Constitution conflicts | Edit `.speckit/constitution.md` manually, re-run `/speckit.analyze` |
| Implementation fails | Check prerequisites (tools installed), review task clarity, verify constitution |
| Integration conflicts | Load `references/guides/integration-planning.md`, consider adapter layer |

---

## Command Availability by AI Agent

| Command Type | Claude Code | Copilot | Cursor | Windsurf | Gemini CLI | Amazon Q |
|--------------|-------------|---------|--------|----------|------------|----------|
| `/speckit.*` slash commands | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes | ⚠️ Limited |
| Custom arguments | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes | ❌ No |
| Natural language feature mgmt | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes |

**Amazon Q Note**: Amazon Q Developer CLI doesn't support custom arguments for slash commands. Use alternative phrasing or manual workflow steps.

---

## Quick Reference Tables

### By Project Type

**Greenfield** (6 steps):
```
init → constitution → specify → plan → tasks → implement
```

**Brownfield** (7-8 steps):
```
brownfield → init --here → analyze-codebase → [optional: reverse-engineer] →
specify → integration-plan → tasks → implement
```

### By Phase

| Phase | Greenfield Command | Brownfield Command |
|-------|-------------------|-------------------|
| Setup | `specify init` | `specify init --here --force` |
| Principles | `/speckit.constitution` | `/speckit.analyze-codebase` |
| Discovery | - | `/speckit.brownfield`, `/speckit.reverse-engineer` |
| Requirements | `/speckit.specify` | `/speckit.specify` |
| Planning | `/speckit.plan` | `/speckit.integration-plan` |
| Breakdown | `/speckit.tasks` | `/speckit.tasks` |
| Execution | `/speckit.implement` | `/speckit.implement` |

---

## Resources

- **Installation Guide**: `references/sdd_install.md`
- **Greenfield Workflow**: `references/workflows/greenfield-quick-start.md`
- **Brownfield Workflow**: `references/workflows/brownfield-quick-start.md`
- **GitHub Spec-Kit**: https://github.com/github/spec-kit
- **Feature Management**: `references/guides/feature-management-quick.md`
