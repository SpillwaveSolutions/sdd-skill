# Greenfield Workflow Quick Start

## Token Budget

**Tier 1**: 100 tokens (already loaded)
**Tier 2**: 2,000 tokens (already loaded)
**Tier 3 (this guide)**: ~1,500 tokens

**Additional resources available**:
- Step details: `references/guides/greenfield-step-details.md` (+750 tokens)
- Examples: `references/examples/greenfield-examples.md` (+500 tokens)
- 10-point summary template: `references/templates/10-point-summary-template.md` (+500 tokens)

**Current total**: 3,600 tokens
**Remaining budget**: 6,400 tokens ✅

---

## When to Use Greenfield Workflow

Use this workflow when:
- Starting a brand new project (0-to-1 development)
- Building a proof-of-concept or prototype
- Creating a new microservice or application component
- No existing codebase exists yet

**For existing codebases**, use [Brownfield Workflow](brownfield-quick-start.md) instead.

---

## The 6-Step Workflow

### Step 1: Initialize Project

```bash
# Basic initialization
specify init my-project --ai claude

# Or in current directory
specify init --here --ai claude
```

**What this does**: Creates `.speckit/` directory structure and sets up slash commands for your AI agent.

---

### Step 2: Establish Project Principles

```
/speckit.constitution
```

**Purpose**: Define project's governing principles and development guidelines.

**Example prompt**:
```
/speckit.constitution Create principles focused on code quality, testing standards, user experience consistency, and performance requirements
```

**What gets created**: `.speckit/constitution.md` with:
- Core development principles
- Coding standards and conventions
- Testing requirements
- Quality expectations

**After this command**: Load `references/templates/10-point-summary-template.md` and summarize the constitution.

---

### Step 3: Create the Specification

```
/speckit.specify
```

**Purpose**: Describe WHAT to build (focus on requirements, not tech stack).

**Example prompt**:
```
/speckit.specify Build an application that helps me organize photos in albums. Albums are grouped by date and can be reorganized by drag-and-drop. Within each album, photos are previewed in a tile interface.
```

**What gets created**: `.speckit/features/[number]-[name]/specify.md` with:
- Functional requirements
- User stories
- Success criteria
- Constraints

**After this command**:
1. Load `references/templates/10-point-summary-template.md` and summarize
2. Ask: "Do you have multiple features planned?" (for feature tracking)

---

### Step 4: Create Technical Implementation Plan

```
/speckit.plan
```

**Purpose**: Define HOW to build it (tech stack, architecture, dependencies).

**Example prompt**:
```
/speckit.plan Use React with TypeScript, Vite build tool, and Tailwind CSS. Keep dependencies minimal. Use local storage for data.
```

**What gets created**: `.speckit/features/[number]-[name]/plan.md` with:
- Technology stack choices
- Architecture decisions
- Key dependencies
- Implementation phases

**After this command**: Load `references/templates/10-point-summary-template.md` and summarize.

---

### Step 5: Break Down into Tasks

```
/speckit.tasks
```

**Purpose**: Create actionable task list from the implementation plan.

**What gets created**: `.speckit/features/[number]-[name]/tasks.md` with:
- Numbered task list
- Task categories (UI, backend, testing, etc.)
- Dependencies between tasks
- Complexity estimates

**After this command**: Load `references/templates/10-point-summary-template.md` and summarize.

---

### Step 6: Execute Implementation

```
/speckit.implement
```

**Purpose**: Execute all tasks and build the feature.

**What happens**: AI agent works through the task list, writing code according to the plan and constitution.

---

## Optional Enhancement Commands

Use these for additional quality and validation:

### Clarify Underspecified Areas

```
/speckit.clarify
```

**When**: After `/speckit.specify`, before `/speckit.plan`
**Purpose**: Identify and clarify ambiguous requirements

### Analyze Consistency & Coverage

```
/speckit.analyze
```

**When**: After `/speckit.tasks`, before `/speckit.implement`
**Purpose**: Cross-artifact consistency and coverage analysis
**Uses**: Analysis scripts from `scripts/` directory

### Generate Quality Checklists

```
/speckit.checklist
```

**Purpose**: Create custom quality checklists for validation

---

## Managing Multiple Features

**After specifying first feature**, if you have more features planned:

1. Tell Claude about all features: "I also want to build [feature 2], [feature 3]"
2. Claude will track them automatically
3. You'll see feature status in every summary:
   ```
   📊 Feature Status: photo-albums (Planned) → Next: user-authentication
   Progress: [●●○○○] 40% | Completed: 0 of 3 features
   ```

**To manage features**:
- Add: "Add a new feature for [description]"
- Reorder: "Move feature X before Y"
- Remove: "Remove feature Z"
- Status: "Show feature status" or option [D]

→ **For detailed feature management**, load `references/guides/feature-management-quick.md`

---

## Common Questions

**Q: Can I run multiple features in parallel?**
A: Yes, but complete one feature's workflow before starting another to maintain clarity.

**Q: What if I need to change the constitution mid-project?**
A: Edit `.speckit/constitution.md` directly and re-run `/speckit.analyze` to check consistency.

**Q: Can I skip steps?**
A: Not recommended. Each step builds on the previous one. Skipping steps leads to incomplete specifications.

**Q: What if implementation fails?**
A: Check prerequisites (tools installed), verify task clarity, review constitution for conflicts.

---

## Troubleshooting

**If command not recognized**:
1. Verify `specify init` completed successfully
2. Check `.claude/commands/` directory exists
3. Restart AI agent

**If artifacts not generated**:
1. Check `.speckit/` directory structure
2. Verify write permissions
3. Check AI agent logs for errors

**If unclear about next step**:
1. Review the workflow overview above
2. Load `references/guides/greenfield-step-details.md` for comprehensive guidance
3. Check `references/examples/greenfield-examples.md` for examples

---

## Related Resources

**Need more details?**
- Step-by-step guide: `references/guides/greenfield-step-details.md`
- Complete examples: `references/examples/greenfield-examples.md`
- Summary template: `references/templates/10-point-summary-template.md`
- Feature management: `references/guides/feature-management-quick.md`

**Installation help**: `references/sdd_install.md`
**Existing codebase**: `references/workflows/brownfield-quick-start.md`
