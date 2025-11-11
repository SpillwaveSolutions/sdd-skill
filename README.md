# Spec-Driven Development (SDD) Skill

A comprehensive Claude Code skill for guiding users through GitHub's Spec-Kit and the Spec-Driven Development methodology.

## What is Spec-Driven Development?

Spec-Driven Development flips traditional software development on its head. Instead of treating specifications as temporary scaffolding, SDD makes them **executable** - they directly generate working implementations rather than just guiding them.

## New: Brownfield Support

This skill now includes comprehensive support for **existing codebases**! You can reverse-engineer existing projects into SDD format, generate constitutions from existing code, and integrate new features into legacy systems.

## Quick Start

To use this skill, simply mention any of these trigger words in your conversation with Claude:

**General SDD:**
- "spec-driven development", "sdd", "speckit"
- "specify cli", "/speckit"
- "executable specifications"

**For New Projects (Greenfield):**
- "new project", "from scratch"
- "specify init"

**For Existing Projects (Brownfield):**
- "brownfield", "existing codebase"
- "legacy code", "modernization"
- "reverse engineer", "codebase analysis"

## What This Skill Provides

### 1. Installation Guidance
- Persistent installation (recommended) using `uv tool install`
- One-time usage with `uvx`
- Installation verification with `specify check`
- Troubleshooting for common issues

### 2. Complete Workflow Support

**Greenfield Workflow** (New Projects - 6 steps):
1. **Initialize Project**: `specify init`
2. **Establish Principles**: `/speckit.constitution`
3. **Create Specification**: `/speckit.specify`
4. **Technical Planning**: `/speckit.plan`
5. **Task Breakdown**: `/speckit.tasks`
6. **Implementation**: `/speckit.implement`

**Brownfield Workflow** (Existing Projects - 7 steps):
1. **Analyze Codebase**: `/speckit.brownfield`
2. **Initialize SDD**: `specify init --here --force`
3. **Generate Constitution**: `/speckit.analyze-codebase`
4. **Choose Strategy**: `/speckit.reverse-engineer`
5. **Document Features**: (optional, based on strategy)
6. **Specify New Feature**: `/speckit.specify`
7. **Integration Planning**: `/speckit.integration-plan`

### 3. Optional Enhancement Commands

- `/speckit.clarify` - Clarify underspecified areas
- `/speckit.analyze` - Consistency & coverage analysis
- `/speckit.checklist` - Generate quality validation checklists

### 4. Validation Commands (Brownfield)

- `/speckit.validate-reverse-engineering` - Verify reverse-engineering accuracy
- `/speckit.coverage-check` - Check documentation coverage
- `/speckit.validate-constitution` - Validate constitution consistency
- `/speckit.trace [feature]` - Spec-to-code traceability

### 5. Development Phase Support

- **Greenfield (0-to-1)**: Build new projects from scratch
- **Brownfield (Existing)**: Reverse-engineer and enhance existing codebases
- **Creative Exploration**: Try multiple tech stacks in parallel
- **Legacy Modernization**: Systematically upgrade old systems

### 6. Best Practices

- For new users: Start small, follow the sequence
- For experienced users: Parallel exploration, custom checklists
- For enterprise teams: Establish constitution early, version control everything

## Artifacts Generated

After running SDD commands, expect these artifacts:

```
project-name/
├── .speckit/
│   ├── constitution.md      # Project principles
│   ├── features/
│   │   └── 001-feature-name/
│   │       ├── specify.md    # Requirements
│   │       ├── plan.md       # Technical plan
│   │       ├── tasks.md      # Task breakdown
│   │       └── checklist.md  # Quality gates
│   └── .claude/
│       └── commands/         # Slash commands
└── [application code]
```

## Supported AI Agents

Works with Claude Code, GitHub Copilot, Cursor, Windsurf, Gemini CLI, and many others (see skill.md for full list).

## Prerequisites

Users need:
- `uv` for package management
- Python 3.11+
- Git
- A supported AI coding agent

## Example Usage

```bash
# Install specify-cli
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git

# Initialize project
specify init my-app --ai claude

# Then in the AI agent:
/speckit.constitution Create principles for production-ready web apps...
/speckit.specify Build a task management app with drag-and-drop...
/speckit.plan Use React with TypeScript, Vite, and Tailwind CSS...
/speckit.tasks
/speckit.implement
```

## Files in This Skill

- **skill.md**: Lean orchestration document with decision tree
- **skill.json**: Metadata and trigger keywords (including brownfield triggers)
- **README.md**: This file - quick reference
- **CLAUDE.md**: Repository guidance for AI agents
- **references/**: Detailed workflow documentation
  - **sdd_install.md**: Installation and setup guide
  - **greenfield.md**: Complete greenfield workflow (6 steps)
  - **brownfield.md**: Complete brownfield workflow (7 steps)

## Resources

- GitHub Spec-Kit: https://github.com/github/spec-kit
- Issues/Support: https://github.com/github/spec-kit/issues

## Philosophy

Remember: This is **AI-native development**. Specifications aren't just documentation - they're executable artifacts that directly drive implementation. The AI agent uses them to generate working code that matches the intent defined in the specs.

---

**Maintained by**: Based on GitHub Spec-Kit by Den Delimarsky (@localden) and John Lam (@jflam)
**License**: MIT
