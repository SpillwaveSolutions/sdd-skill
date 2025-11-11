# Greenfield Workflow: Building from Scratch with SDD

## When to Use Greenfield Workflow

Use this workflow when:
- Starting a brand new project (0-to-1 development)
- Building a proof-of-concept or prototype
- Creating a new microservice or application component
- No existing codebase exists yet

For existing codebases, see [Brownfield Workflow](brownfield.md).

## The 6-Step Greenfield Workflow

### Step 1: Initialize Project

```bash
# Basic initialization
specify init my-project

# With specific AI assistant
specify init my-project --ai claude
specify init my-project --ai cursor-agent
specify init my-project --ai windsurf
specify init my-project --ai copilot

# Initialize in current directory
specify init . --ai claude
# or
specify init --here --ai claude

# With PowerShell scripts (Windows/cross-platform)
specify init my-project --ai copilot --script ps

# Skip git initialization
specify init my-project --ai gemini --no-git

# Debug mode
specify init my-project --ai claude --debug

# With GitHub token (corporate environments)
specify init my-project --ai claude --github-token ghp_your_token_here
```

### Step 2: Establish Project Principles

Launch AI assistant in project directory and use:

```
/speckit.constitution
```

**Purpose**: Create project's governing principles and development guidelines

**Example prompt to give user:**
```
/speckit.constitution Create principles focused on code quality, testing standards, user experience consistency, and performance requirements
```

**After this step - Summarize constitution.md:**

Read `.speckit/constitution.md` and present a summary highlighting:
- Core development principles (3-5 key principles)
- Coding standards and conventions
- Key constraints or requirements
- Testing and quality expectations

**Example summary:**
```
## Constitution Created ✓

I've established the project principles in constitution.md:

**Core Principles:**
- Code quality first: All features must have unit tests (80%+ coverage)
- User experience: Consistent design patterns, WCAG 2.1 AA accessibility
- Performance: Page load under 3 seconds, 60fps interactions
- Simplicity: Prefer vanilla solutions over complex frameworks

**Coding Standards:**
- TypeScript for type safety
- Functional programming patterns preferred
- Comprehensive JSDoc for all public APIs

**Testing Requirements:**
- Unit tests for business logic
- Integration tests for API endpoints
- E2E tests for critical user journeys

Would you like to:
A) Proceed to feature specification
B) Adjust any principles
C) Add additional constraints
```

### Step 3: Create the Specification

```
/speckit.specify
```

**Purpose**: Describe what to build - focus on WHAT and WHY, not tech stack

**Example prompt to give user:**
```
/speckit.specify Build an application that can help me organize my photos in separate photo albums. Albums are grouped by date and can be re-organized by dragging and dropping on the main page. Albums are never in other nested albums. Within each album, photos are previewed in a tile-like interface.
```

**After this step - Summarize specify.md:**

Read `.speckit/features/[feature-number]/specify.md` and present a summary highlighting:
- Main functional requirements (top 3-5 features)
- Key user stories or use cases
- Success criteria and acceptance criteria
- Important constraints or non-functional requirements

**Example summary:**
```
## Specification Created ✓

I've generated specify.md with the following key requirements:

**Core Features:**
- Photo album organization with drag-and-drop interface
- Date-based automatic grouping (no nested albums)
- Tile-based photo preview within albums
- Local-only storage (no cloud uploads)

**User Stories:**
- As a user, I can create albums and organize photos by dragging
- As a user, I can view all photos in an album as tiles
- As a user, I can reorganize albums by date on the main page

**Success Criteria:**
- Albums load within 2 seconds (up to 1000 photos)
- Drag-and-drop supports 100+ photos without lag
- Accessible keyboard navigation (WCAG 2.1 AA)
- Works offline with local SQLite database

**Key Constraints:**
- No photo uploads to external servers
- Metadata stored locally in SQLite
- Support for JPEG, PNG, HEIC formats

**Next Step:** Run `/speckit.plan` to define technical architecture

Would you like to:
A) Proceed to planning phase
B) Modify any requirements
C) Add additional success criteria
D) Use `/speckit.clarify` to explore edge cases
```

### Step 4: Create Technical Implementation Plan

```
/speckit.plan
```

**Purpose**: Provide tech stack and architecture choices

**Example prompt to give user:**
```
/speckit.plan The application uses Vite with minimal number of libraries. Use vanilla HTML, CSS, and JavaScript as much as possible. Images are not uploaded anywhere and metadata is stored in a local SQLite database.
```

**After this step - Summarize plan.md:**

Read `.speckit/features/[feature-number]/plan.md` and present a summary highlighting:
- Technology stack choices and rationale
- Architecture patterns and design decisions
- Key dependencies and libraries
- Implementation milestones or phases

**Example summary:**
```
## Technical Plan Created ✓

I've created plan.md with the following technical approach:

**Technology Stack:**
- Vite (build tool for fast development)
- Vanilla JavaScript (no framework overhead)
- HTML5 Drag-and-Drop API (native functionality)
- SQLite (local database via sql.js)
- CSS Grid + Flexbox (responsive layouts)

**Architecture Decisions:**
- MVC pattern with vanilla JS
- IndexedDB wrapper for photo metadata
- Web Workers for image processing
- Service Worker for offline support

**Key Dependencies:**
- sql.js (SQLite in browser)
- sharp (image thumbnail generation)
- date-fns (date manipulation)

**Implementation Phases:**
1. Core UI scaffolding (3 days)
2. Drag-and-drop functionality (2 days)
3. SQLite integration (2 days)
4. Image loading and caching (2 days)
5. Testing and polish (1 day)

**Next Step:** Run `/speckit.tasks` to break down into actionable tasks

Would you like to:
A) Proceed to task breakdown
B) Adjust technology choices
C) Explore alternative architectures
```

### Step 5: Break Down into Tasks

```
/speckit.tasks
```

**Purpose**: Create actionable task list from implementation plan

**After this step - Summarize tasks.md:**

Read `.speckit/features/[feature-number]/tasks.md` and present a summary highlighting:
- Total number of tasks
- Major task categories
- Critical path or dependencies
- Estimated complexity

**Example summary:**
```
## Tasks Breakdown Created ✓

I've generated tasks.md with 18 actionable tasks:

**Task Categories:**
- **UI Foundation** (5 tasks): App shell, layouts, routing
- **Drag-and-Drop** (4 tasks): DnD handlers, visual feedback, persistence
- **Database Layer** (3 tasks): SQLite setup, schema, CRUD operations
- **Image Handling** (4 tasks): Loading, thumbnails, caching, format support
- **Testing & Polish** (2 tasks): Unit tests, E2E tests, accessibility audit

**Critical Dependencies:**
- Task 3 (Database setup) must complete before Task 7 (Album persistence)
- Task 5 (Image loader) must complete before Task 9 (Thumbnail generation)
- All UI tasks (1-5) should complete before drag-and-drop implementation

**Complexity Estimate:**
- High complexity: 3 tasks (Database integration, DnD state management)
- Medium complexity: 9 tasks
- Low complexity: 6 tasks

**Estimated Timeline:** 10 days for full implementation

**Next Step:** Run `/speckit.implement` to begin execution

Would you like to:
A) Start implementation
B) Reorder or adjust tasks
C) Run `/speckit.analyze` for consistency check
D) Generate quality checklist with `/speckit.checklist`
```

### Step 6: Execute Implementation

```
/speckit.implement
```

**Purpose**: Execute all tasks and build the feature

## Optional Enhancement Commands

Use these for additional quality and validation:

### Clarify Underspecified Areas

```
/speckit.clarify
```

**When to use**: After `/speckit.specify`, before `/speckit.plan`
**Purpose**: Identify and clarify ambiguous requirements

### Analyze Consistency & Coverage

```
/speckit.analyze
```

**When to use**: After `/speckit.tasks`, before `/speckit.implement`
**Purpose**: Cross-artifact consistency and coverage analysis

### Generate Quality Checklists

```
/speckit.checklist
```

**Purpose**: Create custom quality checklists that validate requirements completeness, clarity, and consistency (like "unit tests for English")

## Artifacts Generated

After running SDD commands, the following artifacts are created:

### Project Structure
```
project-name/
├── .speckit/
│   ├── constitution.md      # Project principles
│   ├── features/
│   │   └── 001-feature-name/
│   │       ├── specify.md    # Requirements & user stories
│   │       ├── plan.md       # Technical implementation plan
│   │       ├── tasks.md      # Actionable task list
│   │       └── checklist.md  # Quality validation checklist
│   └── .claude/
│       └── commands/         # Slash command definitions
└── [your application code]
```

### Key Artifacts to Reference

1. **constitution.md**: Project-wide principles and guidelines
2. **specify.md**: Requirements and user stories for current feature
3. **plan.md**: Technical implementation plan with architecture decisions
4. **tasks.md**: Task breakdown for implementation
5. **checklist.md**: Quality validation criteria

## Workflow Best Practices

### For Users New to SDD

1. **Start small**: Begin with a simple feature to learn the workflow
2. **Follow the sequence**: Don't skip steps (constitution → specify → plan → tasks → implement)
3. **Be specific in specify**: The more detailed your requirements, the better the output
4. **Review artifacts**: After each step, review the generated artifacts before proceeding
5. **Use clarify**: Don't hesitate to use `/speckit.clarify` if requirements are unclear

### For Experienced Users

1. **Parallel exploration**: Use creative exploration phase for multiple implementation approaches
2. **Custom checklists**: Define project-specific quality gates with `/speckit.checklist`
3. **Analyze before implement**: Always run `/speckit.analyze` to catch issues early
4. **Iterate on constitution**: Refine project principles as you learn

### For Enterprise Teams

1. **Establish constitution early**: Include organizational constraints, compliance requirements, design systems
2. **Version control everything**: All `.speckit/` artifacts should be in Git
3. **Use feature branches**: Let Git branches drive feature detection
4. **Document tech stack constraints**: Be explicit in `/speckit.plan` about approved technologies

## Advanced Usage Patterns

### Multi-Stack Exploration

For creative exploration of different tech stacks:

```bash
# Create multiple feature branches
git checkout -b feature-001-react
/speckit.plan Use React with TypeScript...
/speckit.tasks
/speckit.implement

git checkout -b feature-001-vue
/speckit.plan Use Vue 3 with Composition API...
/speckit.tasks
/speckit.implement
```

### Corporate/Enterprise Setup

```bash
# Initialize with corporate GitHub token
specify init my-project --ai claude --github-token $GITHUB_TOKEN

# Constitution with enterprise constraints
/speckit.constitution
- Must use approved cloud providers (AWS, Azure)
- Follow internal design system
- Comply with SOC2 requirements
- Use approved open source licenses only
```

## Command Reference

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `specify init` | Initialize project | Start of new project |
| `/speckit.constitution` | Set principles | After init, before any feature work |
| `/speckit.specify` | Define requirements | Start of each feature |
| `/speckit.clarify` | Clarify ambiguities | After specify, if requirements unclear |
| `/speckit.plan` | Create tech plan | After specify (and optional clarify) |
| `/speckit.tasks` | Break down tasks | After plan |
| `/speckit.analyze` | Validate consistency | After tasks, before implement |
| `/speckit.checklist` | Quality gates | Any time to define validation criteria |
| `/speckit.implement` | Execute tasks | After tasks (and optional analyze) |

## Example: Complete Greenfield Workflow

```bash
# Step 1: Install and initialize
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
specify init photo-organizer --ai claude

# Step 2: In your AI agent
/speckit.constitution Create principles focused on:
- Simple, intuitive user interfaces
- Data privacy (no cloud uploads)
- Fast, responsive performance
- Minimal dependencies

# Step 3: Specify the feature
/speckit.specify Build a photo organization app with drag-and-drop albums,
date-based grouping, and tile-based photo previews within albums

# Step 4: Technical planning
/speckit.plan Use Vite, vanilla JS, HTML5 drag-and-drop API,
and SQLite for local storage

# Step 5: Break down tasks
/speckit.tasks

# Step 6: Implement
/speckit.implement
```

## Next Steps

After completing greenfield implementation:
- Run tests and validation
- Review generated code against constitution
- Iterate with additional features following the same workflow
- Consider using `/speckit.checklist` to define quality standards for future work
