# Greenfield Step-by-Step Details

Complete reference for each step in the greenfield workflow.

## Token Budget

**Tier 1**: 100 tokens (already loaded)
**Tier 2**: 2,000 tokens (already loaded)
**Tier 3 (this guide)**: ~750 tokens

**Current total**: 2,850 tokens
**Remaining budget**: 7,150 tokens ✅

---

## Step 1: Initialize Project

### Basic Initialization

```bash
# Create new project directory
specify init my-project --ai claude

# Initialize in current directory
specify init --here --ai claude
```

### Advanced Options

```bash
# With specific AI assistant
specify init my-project --ai cursor-agent
specify init my-project --ai windsurf
specify init my-project --ai copilot

# With PowerShell scripts (Windows/cross-platform)
specify init my-project --ai copilot --script ps

# Skip git initialization
specify init my-project --ai gemini --no-git

# Debug mode (verbose output)
specify init my-project --ai claude --debug

# With GitHub token (corporate environments)
specify init my-project --ai claude --github-token ghp_your_token_here
```

### What Gets Created

```
my-project/
├── .speckit/
│   ├── constitution.md.template
│   └── features/
├── .claude/
│   └── commands/
│       ├── speckit.constitution.md
│       ├── speckit.specify.md
│       ├── speckit.plan.md
│       ├── speckit.tasks.md
│       └── speckit.implement.md
└── .git/ (unless --no-git specified)
```

### Troubleshooting

| Problem | Solution |
|---------|----------|
| Command not found | Install specify-cli: `uv tool install specify-cli --from git+https://github.com/github/spec-kit.git` |
| Permission denied | Check directory permissions, try with sudo (not recommended) or in user directory |
| Git initialization fails | Use `--no-git` flag, initialize git manually later |
| AI agent not recognized | Check supported agents list, use generic name if your agent not listed |

---

## Step 2: Establish Project Principles

### Command

```
/speckit.constitution
```

### Purpose

Define your project's governing principles, coding standards, and quality expectations. This becomes the foundation for all future decisions.

### Example Prompts

**For Web Apps**:
```
/speckit.constitution Create principles focused on:
- Modern web standards (ES2024+, Web Components)
- Accessibility (WCAG 2.1 AA minimum)
- Performance (Core Web Vitals targets)
- Testing (unit + integration + e2e)
```

**For APIs**:
```
/speckit.constitution Create principles focused on:
- RESTful design patterns
- OpenAPI 3.1 documentation
- Authentication/authorization standards
- Performance SLAs (99.9% uptime, <100ms response)
```

**For Mobile Apps**:
```
/speckit.constitution Create principles focused on:
- Cross-platform (iOS + Android)
- Offline-first architecture
- Battery efficiency
- App store compliance (Apple HIG, Material Design)
```

### What Gets Generated

`.speckit/constitution.md` containing:
- Core development principles
- Technology constraints and standards
- Quality expectations
- Testing requirements
- Performance targets

### After This Command

Use `references/templates/10-point-summary-template.md` to summarize the constitution for the user.

---

## Step 3: Create the Specification

### Command

```
/speckit.specify
```

### Purpose

Describe WHAT to build, focusing on requirements and user needs, not technical implementation.

### Example Prompts

**Feature Description**:
```
/speckit.specify Build a photo album organizer that:
- Groups photos by date automatically
- Allows drag-and-drop reorganization
- Displays thumbnails in grid layout
- Supports albums up to 10,000 photos
- Works offline with local storage
```

**User Story Format**:
```
/speckit.specify As a photographer, I want to organize my photos into albums by event and date, so I can quickly find and share specific photo collections. Key requirements:
- Auto-grouping by EXIF date
- Manual album creation and editing
- Fast search across all albums
- Export album as zip file
```

### What Gets Generated

`.speckit/features/001-[feature-name]/specify.md` containing:
- Feature description
- User stories
- Functional requirements
- Success criteria
- Constraints and assumptions

### Key Guidelines

**Do Focus On**:
- What users need to accomplish
- Business requirements and goals
- Success metrics
- Constraints (performance, compatibility, etc.)

**Don't Focus On**:
- Technology choices (save for planning step)
- Implementation details
- Database schemas or API designs
- Library or framework selections

### After This Command

Use `references/templates/10-point-summary-template.md` to summarize the specification.

If you have multiple features planned, ask: "Do you have additional features to specify?"

---

## Step 4: Create Technical Implementation Plan

### Command

```
/speckit.plan
```

### Purpose

Define HOW to build the feature: technology stack, architecture, dependencies, and implementation approach.

### Example Prompts

**Tech Stack Specification**:
```
/speckit.plan Use:
- React 18+ with TypeScript
- Vite for build tooling
- Tailwind CSS for styling
- IndexedDB for local storage
- Vitest for testing
Keep dependencies minimal, avoid unnecessary abstractions
```

**Architecture Guidance**:
```
/speckit.plan Design a component-based architecture with:
- Presentational/Container component split
- Context API for state management
- Custom hooks for business logic
- Service layer for data access
Focus on testability and maintainability
```

### What Gets Generated

`.speckit/features/001-[feature-name]/plan.md` containing:
- Technology stack choices with rationale
- Architecture and design patterns
- Key dependencies
- Implementation phases
- Risk assessment

### Key Guidelines

**Technology Choices Should Consider**:
- Constitution constraints
- Team expertise
- Project requirements
- Performance needs
- Maintainability

**Architecture Should Define**:
- Component/module structure
- Data flow patterns
- State management approach
- API/service boundaries
- Testing strategy

### After This Command

Use `references/templates/10-point-summary-template.md` to summarize the plan.

---

## Step 5: Break Down into Tasks

### Command

```
/speckit.tasks
```

### Purpose

Create an actionable task list with clear implementation steps, dependencies, and complexity estimates.

### What Gets Generated

`.speckit/features/001-[feature-name]/tasks.md` containing:
- Numbered task list
- Task categories (scaffolding, UI, backend, testing, etc.)
- Dependencies between tasks
- Complexity estimates
- Acceptance criteria per task

### Task Organization

Tasks typically organized by:
1. **Scaffolding** - Project setup, dependencies, folder structure
2. **Core Implementation** - Main feature functionality
3. **Polish** - Error handling, edge cases, performance
4. **Testing** - Unit tests, integration tests, e2e tests

### Example Task Structure

```markdown
## Scaffolding (Tasks 1-5)
1. Initialize Vite + React + TypeScript project
2. Install and configure Tailwind CSS
3. Set up IndexedDB wrapper utilities
4. Create folder structure (components/, hooks/, services/)
5. Configure Vitest and testing library

## Core UI (Tasks 6-12)
6. Build PhotoGrid component with virtualization
7. Implement drag-and-drop with dnd-kit
8. Create Album component with thumbnail view
9. Build AlbumList navigation component
...
```

### After This Command

Use `references/templates/10-point-summary-template.md` to summarize the tasks.

---

## Step 6: Execute Implementation

### Command

```
/speckit.implement
```

### Purpose

Execute all tasks in sequence, writing code according to the plan and constitution.

### What Happens

The AI agent:
1. Works through tasks sequentially
2. Writes code files
3. Installs dependencies
4. Runs tests
5. Handles errors and edge cases
6. Verifies against success criteria

### Monitoring Progress

Watch for:
- Task completion messages
- Test results
- Build output
- Error messages or warnings

### Intervention Points

You may need to:
- Clarify ambiguous requirements
- Provide missing credentials or API keys
- Resolve unexpected errors
- Adjust plans based on discovered constraints

### After Implementation

1. Run the application locally
2. Verify all requirements met
3. Review code quality
4. Consider next feature (if multi-feature project)

---

## Optional Enhancement Commands

### Clarify Underspecified Areas

```
/speckit.clarify
```

**When**: After `/speckit.specify`, before `/speckit.plan`
**Purpose**: Identify and clarify ambiguous or incomplete requirements

### Analyze Consistency & Coverage

```
/speckit.analyze
```

**When**: After `/speckit.tasks`, before `/speckit.implement`
**Purpose**: Cross-artifact consistency check and coverage analysis
**Uses**: Analysis scripts from `scripts/` directory

### Generate Quality Checklists

```
/speckit.checklist
```

**Purpose**: Create custom quality validation checklists

---

## Best Practices

### For New Users

1. **Start small** - One simple feature first to learn the workflow
2. **Review each artifact** - Don't rush through steps
3. **Use examples** - Provide concrete example prompts to AI
4. **Iterate** - Regenerate if first pass doesn't match your vision

### For Experienced Users

1. **Leverage constitution** - Strong principles lead to consistent implementations
2. **Be specific in plans** - Detailed tech stack guidance prevents surprises
3. **Group tasks logically** - Well-organized tasks lead to cleaner code
4. **Use optional commands** - Clarify, analyze, and checklist add quality

### For Enterprise Teams

1. **Establish team constitution** - Shared principles across projects
2. **Document architecture patterns** - Consistent designs across features
3. **Integrate with CI/CD** - Automate quality checks from SDD artifacts
4. **Version control artifacts** - Commit `.speckit/` alongside code

---

## Troubleshooting

### Commands Not Working

**Problem**: `/speckit.*` commands not recognized
**Solutions**:
1. Verify `specify init` ran successfully
2. Check `.claude/commands/` directory exists
3. Restart AI agent
4. Re-run `specify init` if needed

### Artifacts Not Generated

**Problem**: Constitution or specs not created
**Solutions**:
1. Check `.speckit/` directory exists and has write permissions
2. Review AI agent output for error messages
3. Verify command syntax (correct slash command)
4. Try with `--debug` flag during init

### Implementation Fails

**Problem**: `/speckit.implement` encounters errors
**Solutions**:
1. Review task clarity - vague tasks lead to errors
2. Check constitution for conflicts with plan
3. Verify all tools and dependencies available
4. Break complex tasks into smaller steps
5. Provide more specific technical guidance in plan

---

## Next Steps

After completing first feature:
- **Multiple features?** Load `references/guides/feature-management-quick.md`
- **Need examples?** Load `references/examples/greenfield-examples.md`
- **Existing codebase?** Switch to `references/workflows/brownfield-quick-start.md`
