---
name: sdd
description: This skill should be used when users want guidance on Spec-Driven Development methodology using GitHub's Spec-Kit. Guide users through executable specification workflows for both new projects (greenfield) and existing codebases (brownfield). After any SDD command generates artifacts (constitution, specs, plans, tasks), automatically summarize the created content and present it to the user for feedback before proceeding to the next step. This keeps users in the loop while maintaining agile velocity.
version: 2.0.0
triggers:
  - spec-driven development
  - spec kit
  - speckit
  - sdd
  - specify cli
  - specification driven
  - github spec-kit
  - /speckit
  - constitution
  - specify init
  - executable specifications
  - intent-driven development
  - brownfield
  - existing codebase
  - legacy code
  - legacy system
  - add features to existing
  - modernize
  - modernization
  - existing project
  - reverse engineer
  - codebase analysis
  - iterative enhancement
author: Based on GitHub Spec-Kit by Den Delimarsky and John Lam
license: MIT
tags:
  - development-methodology
  - ai-native-development
  - spec-driven
  - github
  - project-management
  - workflow
  - requirements
  - planning
---

# Spec-Driven Development (SDD) Skill

Guide users through GitHub's Spec-Kit for Spec-Driven Development - a methodology that flips traditional software development by making specifications executable and directly generating working implementations.

## Core Philosophy

Spec-Driven Development emphasizes:
- **Intent-driven development**: Define the "what" before the "how"
- **Rich specification creation**: Use guardrails and organizational principles
- **Multi-step refinement**: Not one-shot code generation
- **AI-native**: Heavy reliance on advanced AI capabilities

Remember: This is **AI-native development**. Specifications aren't just documentation - they're executable artifacts that directly drive implementation. The AI agent uses them to generate working code that matches the intent defined in the specs.

## Quick Decision Tree

### Is this a new project (greenfield)?
→ **See [Greenfield Workflow](references/greenfield.md)** for the complete 6-step process

### Is this an existing codebase (brownfield)?
→ **See [Brownfield Workflow](references/brownfield.md)** for reverse-engineering and integration guidance

### Need installation help?
→ **See [Installation Guide](references/sdd_install.md)** for setup and troubleshooting

## Installation Quick Start

**Recommended (Persistent):**
```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
```

**One-time Usage:**
```bash
uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME>
```

**Verify:**
```bash
specify check
```

For detailed installation options, troubleshooting, and environment variables, see [Installation Guide](references/sdd_install.md).

## Supported AI Agents

Works with:
- ✅ Claude Code
- ✅ GitHub Copilot
- ✅ Gemini CLI
- ✅ Cursor
- ✅ Qwen Code
- ✅ opencode
- ✅ Windsurf
- ✅ Kilo Code
- ✅ Auggie CLI
- ✅ CodeBuddy CLI
- ✅ Roo Code
- ✅ Codex CLI
- ✅ Amp
- ⚠️ Amazon Q Developer CLI (doesn't support custom arguments for slash commands)

## Artifact Summarization and Feedback Loop

**CRITICAL WORKFLOW**: After any SDD command generates or modifies artifacts, automatically follow this feedback loop to keep the user engaged:

### After Each Command Completes

1. **Detect Artifact Changes**
   - Identify which artifacts were created or modified:
     - `constitution.md` (project principles)
     - `spec.md` (requirements specification)
     - `plan.md` (technical implementation plan)
     - `tasks.md` (actionable task breakdown)
     - Analysis reports from brownfield workflows

2. **Read and Summarize**
   - Read the relevant artifact(s)
   - Extract key information:
     - **For constitution.md**: Core principles, coding standards, constraints
     - **For spec.md**: Main requirements, user stories, success criteria
     - **For plan.md**: Tech stack choices, architecture decisions, milestones
     - **For tasks.md**: Number of tasks, major task categories, dependencies
     - **For analysis reports**: Current patterns, tech debt, integration points

3. **Present Concise Summary**
   - Highlight the most important decisions/content (3-5 bullet points)
   - Keep summary focused and actionable
   - Use clear headings for each artifact type

4. **Offer Feedback Options**
   - **Option A**: "Looks good, proceed to next step"
   - **Option B**: "I'd like to modify [specific section]"
   - **Option C**: "Regenerate with these changes: [user input]"
   - **Option D**: "Explain why [specific decision] was made"

### Example Summarization After \`/speckit.specify\`

\`\`\`
## Specification Created ✓

I've generated spec.md with the following key requirements:

**Core Features:**
- Photo album organization with drag-and-drop interface
- Date-based grouping (no nested albums)
- Tile-based preview within albums

**Success Criteria:**
- Albums load within 2 seconds
- Drag-and-drop supports 100+ photos without lag
- Accessible keyboard navigation (WCAG 2.1 AA)

**Key Constraints:**
- No photo uploads to external servers
- Local SQLite for metadata storage

**Next Step:** Run \`/speckit.plan\` to define technical architecture

How does this look? Would you like to:
A) Proceed to planning phase
B) Modify any requirements
C) Add additional success criteria
\`\`\`

### When to Skip Summarization

Only skip the summarization step when:
- User explicitly requests "skip summaries" or "run all steps automatically"
- Re-running a command without artifact changes
- Command fails or produces errors (troubleshoot instead)

### Benefits of This Workflow

- **Keeps user engaged**: No "black box" artifact generation
- **Enables early feedback**: Catch misunderstandings before implementation
- **Maintains agility**: Quick review, not lengthy approval processes
- **Builds trust**: User sees the AI's reasoning and decisions

## How to Use This Skill

### When User Asks About SDD

1. Explain core philosophy: Executable specifications, intent-driven, AI-native
2. Verify prerequisites: \`uv\`, Python 3.11+, Git, AI agent
3. Determine project type: New (greenfield) vs existing (brownfield)
4. Guide to appropriate workflow:
   - Greenfield → [Greenfield Workflow](references/greenfield.md)
   - Brownfield → [Brownfield Workflow](references/brownfield.md)

### When User Wants to Start a New Project

1. Guide installation → [Installation Guide](references/sdd_install.md)
2. Initialize project:
   \`\`\`bash
   specify init my-project --ai claude
   \`\`\`
3. Follow greenfield workflow → [Greenfield Workflow](references/greenfield.md)
4. **After each step**: Summarize artifacts and get user feedback

### When User Has an Existing Codebase

1. Check for \`.speckit/\` directory
2. **If missing** → Guide through [Brownfield Workflow](references/brownfield.md):
   - Analyze existing code
   - Generate constitution from existing patterns
   - Choose artifact generation strategy
   - Add new features with SDD
3. **If present** → Determine next step based on current progress
4. **After each step**: Summarize artifacts and get user feedback

### When User Wants to Add a Feature

**To greenfield project:**
1. Navigate to [Greenfield Workflow](references/greenfield.md)
2. Follow steps 3-6 (specify → plan → tasks → implement)
3. Summarize each artifact before proceeding

**To brownfield/existing project:**
1. Navigate to [Brownfield Workflow](references/brownfield.md)
2. Follow steps 6-7 (specify → integration planning → tasks → implement)
3. Summarize each artifact before proceeding

### When User Encounters Issues

1. **Installation issues** → [Installation Guide](references/sdd_install.md) troubleshooting section
2. **Workflow issues** → Check appropriate workflow guide:
   - [Greenfield troubleshooting](references/greenfield.md)
   - [Brownfield troubleshooting](references/brownfield.md)
3. **Feature detection** → Set \`SPECIFY_FEATURE\` environment variable (see [Installation Guide](references/sdd_install.md))

## Workflow Overview

### Greenfield (New Projects)

\`\`\`
specify init → /speckit.constitution → [SUMMARIZE] →
/speckit.specify → [SUMMARIZE] → /speckit.plan → [SUMMARIZE] →
/speckit.tasks → [SUMMARIZE] → /speckit.implement
\`\`\`

**Full details:** [Greenfield Workflow](references/greenfield.md)

### Brownfield (Existing Projects)

\`\`\`
specify init --here → /speckit.brownfield → [SUMMARIZE] →
/speckit.analyze-codebase → [SUMMARIZE] →
/speckit.reverse-engineer → [SUMMARIZE] → /speckit.specify → [SUMMARIZE] →
/speckit.integration-plan → [SUMMARIZE] → /speckit.tasks → [SUMMARIZE] →
/speckit.implement
\`\`\`

**Full details:** [Brownfield Workflow](references/brownfield.md)

## Development Phases Supported

### 0-to-1 Development ("Greenfield")
Start with high-level requirements, generate specifications from scratch, plan implementation steps, build production-ready applications.

**→ [Greenfield Workflow](references/greenfield.md)**

### Iterative Enhancement ("Brownfield")
Add features iteratively to existing codebases, modernize legacy systems, adapt processes for evolving requirements, reverse-engineer existing code into SDD format.

**→ [Brownfield Workflow](references/brownfield.md)**

### Creative Exploration
Explore diverse solutions in parallel, support multiple technology stacks & architectures, experiment with UX patterns.

**→ [Greenfield Workflow](references/greenfield.md) - Multi-Stack Exploration section**

## Key Commands Reference

### Installation & Setup
\`\`\`bash
specify init <project>              # New project
specify init --here --force         # Existing project
specify check                       # Verify installation
\`\`\`

### Greenfield Workflow
\`\`\`
/speckit.constitution               # Project principles → SUMMARIZE
/speckit.specify                    # Define requirements → SUMMARIZE
/speckit.plan                       # Technical planning → SUMMARIZE
/speckit.tasks                      # Break down tasks → SUMMARIZE
/speckit.implement                  # Execute
\`\`\`

### Brownfield Workflow
\`\`\`
/speckit.brownfield                 # Analyze existing code → SUMMARIZE
/speckit.analyze-codebase          # Deep analysis & constitution → SUMMARIZE
/speckit.reverse-engineer          # Document existing features → SUMMARIZE
/speckit.integration-plan          # Plan new feature integration → SUMMARIZE
\`\`\`

### Optional Enhancement Commands
\`\`\`
/speckit.clarify                   # Clarify ambiguous requirements
/speckit.analyze                   # Cross-artifact consistency check
/speckit.checklist                 # Generate quality checklists
\`\`\`

## Analysis Scripts

The SDD skill includes analysis scripts for deep quality validation and progress tracking:

### \`scripts/phase_summary.sh\`
Generates a comprehensive progress report across all phases in a tasks.md file:
- Shows completion percentage for each phase
- Lists pending tasks per phase
- Highlights simplified/modified tasks
- Provides overall progress statistics
- Supports any SDD feature's tasks.md file

**Usage:**
\`\`\`bash
~/.claude/skills/sdd/scripts/phase_summary.sh specs/003-keyboard-shortcuts/tasks.md
\`\`\`

**Output:** Markdown-formatted phase-by-phase progress report with:
- Phase-by-phase completion percentages
- Pending task lists (up to 5 per phase)
- Simplified task warnings
- Overall feature progress summary

**When to Use:**
- Check progress on any SDD feature
- Get quick overview of what's complete vs pending
- Identify phases that need attention
- Generate status reports for stakeholders

### \`scripts/analyze-requirements.py\`
Analyzes requirement coverage across spec.md and tasks.md:
- Maps functional requirements (FR-001, FR-002, etc.) to implementation tasks
- Identifies uncovered requirements (gaps in task coverage)
- Flags vague requirements lacking measurable criteria
- Calculates coverage percentage

**Usage:**
\`\`\`bash
python3 ~/.claude/skills/sdd/scripts/analyze-requirements.py
\`\`\`

**Output:** JSON with coverage metrics, uncovered requirements, vague requirements

### \`scripts/analyze-success-criteria.py\`
Analyzes success criteria verification coverage:
- Maps success criteria (SC-001, SC-002, etc.) to verification tasks
- Validates measurability of each criterion
- Identifies criteria without verification tasks
- Groups by metric type (performance, accessibility, usability)

**Usage:**
\`\`\`bash
python3 ~/.claude/skills/sdd/scripts/analyze-success-criteria.py
\`\`\`

**Output:** JSON with coverage summary, verification task mapping

### \`scripts/analyze-edge-cases.py\`
Analyzes edge case coverage across specifications:
- Maps edge cases to explicit task coverage
- Identifies implicitly covered cases (handled by general logic)
- Flags uncovered edge cases requiring attention
- Categorizes coverage type (EXPLICIT, IMPLICIT, UNCOVERED)

**Usage:**
\`\`\`bash
python3 ~/.claude/skills/sdd/scripts/analyze-edge-cases.py
\`\`\`

**Output:** JSON with coverage breakdown, uncovered edge case details

**When to Use:**
These scripts are automatically invoked during \`/speckit.analyze\` to provide deep consistency validation. They help identify:
- Requirements without task coverage
- Success criteria without verification
- Edge cases that need test coverage
- Ambiguous requirements needing clarification

### Validation Commands (Brownfield)
\`\`\`
/speckit.validate-reverse-engineering  # Verify spec accuracy
/speckit.coverage-check                # Check documentation coverage
/speckit.validate-constitution         # Verify constitution consistency
/speckit.trace [feature]               # Map specs to code
\`\`\`

## Detailed Documentation

- **[Installation Guide](references/sdd_install.md)**: Installation methods, troubleshooting, environment variables
- **[Greenfield Workflow](references/greenfield.md)**: Complete 6-step workflow for new projects
- **[Brownfield Workflow](references/brownfield.md)**: Complete 7-step workflow for existing codebases

## Integration with Other Skills

This skill works well with:
- **project-memory**: Document SDD decisions and patterns
- **design-doc-mermaid**: Visualize architecture from plan.md
- **github-workflows**: Automate SDD artifact validation
- **code-quality-reviewer**: Review generated implementation

## Resources

- GitHub Spec-Kit Repository: https://github.com/github/spec-kit
- Issues/Support: https://github.com/github/spec-kit/issues
- License: MIT

## Maintainers

- Den Delimarsky (@localden)
- John Lam (@jflam)
