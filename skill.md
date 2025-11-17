---
name: sdd
description: Guide users through GitHub Spec-Kit for executable spec-driven development (greenfield/brownfield workflows with feature tracking).
version: 2.2.0
triggers:
  - sdd
  - speckit
  - spec-driven
  - greenfield
  - brownfield
  - feature status
  - /speckit
author: Based on GitHub Spec-Kit
license: MIT
tier1_token_budget: 100
tier2_token_budget: 2000
---

# Spec-Driven Development (SDD) Skill

Guide users through GitHub's Spec-Kit for Spec-Driven Development - a methodology that makes specifications executable, directly generating working implementations.

## Core Philosophy

Spec-Driven Development emphasizes:
- **Intent-driven**: Define "what" before "how"
- **Executable specs**: Specifications drive implementation, not just document it
- **Multi-step refinement**: Not one-shot code generation
- **AI-native**: Heavy reliance on AI capabilities

## Intent Classification & Routing

**CRITICAL**: Use decision tree to route surgically to Tier 3 resources. Load only what's needed.

### Step 1: Identify User Intent

Analyze user request and classify into ONE primary intent:

**NEW_PROJECT** - Triggers:
- "new project", "from scratch", "greenfield", "specify init", "start fresh"
- User has no existing codebase
- Wants to build something new

**EXISTING_PROJECT** - Triggers:
- "existing", "brownfield", "legacy", "add feature to existing", "current codebase"
- User has existing code
- Wants to enhance or modernize

**FEATURE_MANAGEMENT** - Triggers:
- "feature status", "track features", "add feature", "move feature", "show features"
- "progress", "dependencies", "what's next"
- User managing multiple features

**INSTALLATION** - Triggers:
- "install", "setup", "specify check", "how to install", "prerequisites"
- User needs to set up tools

**EXECUTE_WORKFLOW** - Triggers:
- `/speckit.constitution`, `/speckit.specify`, `/speckit.plan`, `/speckit.tasks`, `/speckit.implement`
- User executing SDD commands
- Need to provide post-command summary

**COMMAND_REFERENCE** - Triggers:
- "what commands", "list commands", "available commands", "slash commands"
- User needs command documentation

### Step 2: Route to Appropriate Resources (Surgical Loading)

**For NEW_PROJECT**:
```
1. Load: references/workflows/greenfield-quick-start.md (~300 lines, ~1,500 tokens)
2. IF user asks for step details → Load: references/guides/greenfield-step-details.md (~150 lines)
3. IF stuck or needs examples → Load: references/examples/greenfield-examples.md (~100 lines)

Token budget: 2,100 + 1,500 = 3,600 tokens (within budget ✅)
```

**For EXISTING_PROJECT**:
```
1. Load: references/workflows/brownfield-quick-start.md (~300 lines, ~1,500 tokens)
2. IF needs codebase analysis → Load: references/guides/codebase-analysis.md (~250 lines)
3. IF needs reverse engineering → Load: references/guides/reverse-engineering.md (~250 lines)
4. IF needs integration planning → Load: references/guides/integration-planning.md (~250 lines)

Token budget: 2,100 + 1,500 + [0-1,250] = 3,600-4,850 tokens
```

**For FEATURE_MANAGEMENT**:
```
1. Load: references/guides/feature-management-quick.md (~200 lines, ~1,000 tokens)
2. IF tracking status → Load: references/templates/feature-status-brief.md (~60 lines)
3. IF detailed dashboard → Load: references/templates/feature-status-dashboard.md (~100 lines)

Token budget: 2,100 + 1,000 + [0-800] = 3,100-3,900 tokens (optimal ✅)
```

**For INSTALLATION**:
```
1. Load: references/sdd_install.md (143 lines, ~715 tokens)

Token budget: 2,100 + 715 = 2,815 tokens (excellent ✅)
```

**For EXECUTE_WORKFLOW** (after SDD command completes):
```
1. Detect which command completed
2. Load: references/templates/10-point-summary-template.md (~100 lines, ~500 tokens)
3. IF feature tracking active → Load: references/templates/feature-status-brief.md (~60 lines)
4. Apply template to generated artifacts

Token budget: 2,100 + 500 + [0-300] = 2,600-2,900 tokens (perfect ✅)
```

**For COMMAND_REFERENCE**:
```
1. Load: references/templates/command-reference.md (~80 lines, ~400 tokens)

Token budget: 2,100 + 400 = 2,500 tokens (minimal ✅)
```

## Token Budget Management

**Total Budget per Request**: <10,000 tokens (target: <7,500)

**Tier Loading Costs**:
- **Tier 1 (YAML)**: 100 tokens (always loaded)
- **Tier 2 (this file)**: 2,000 tokens (always loaded)
- **Tier 3 (on-demand)**: 400-6,000 tokens depending on intent

**Before Loading Tier 3**:
1. ✅ Identify intent (above decision tree)
2. ✅ Select minimal relevant resource
3. ✅ Check cumulative budget (Tier1 + Tier2 + planned Tier3)
4. ⚠️ If approaching 8,000 tokens → Load summary/overview only
5. ❌ If over 10,000 tokens → Stop loading, use inline guidance

**Loading Priority** (when budget constrained):
1. Workflow quick-start (essential)
2. Templates (if command executed)
3. Step details (if user stuck)
4. Examples (last resort)

## Workflow Quick Reference

**Greenfield** (New Projects - 6 steps):
```
specify init → /speckit.constitution → /speckit.specify →
/speckit.plan → /speckit.tasks → /speckit.implement
```
→ **Full guide**: `references/workflows/greenfield-quick-start.md`

**Brownfield** (Existing Projects - 7 steps):
```
/speckit.brownfield → specify init --here → /speckit.analyze-codebase →
/speckit.reverse-engineer → /speckit.specify → /speckit.integration-plan →
/speckit.tasks → /speckit.implement
```
→ **Full guide**: `references/workflows/brownfield-quick-start.md`

## Supported AI Agents

Works with: Claude Code, GitHub Copilot, Cursor, Windsurf, Gemini CLI, Qwen Code, opencode, Roo Code, and others.

⚠️ **Amazon Q Developer CLI** doesn't support custom arguments for slash commands.

→ **Full list**: See README.md

## Resource Loading Policy

**CRITICAL**: Load resources surgically, never proactively.

**Templates** (load ONLY when):
- `/speckit.*` command completes → Load `templates/10-point-summary-template.md`
- User requests commands → Load `templates/command-reference.md`
- Feature tracking active → Load `templates/feature-status-*.md`

**Workflow Guides** (load ONLY when):
- Intent=NEW_PROJECT → Load `workflows/greenfield-quick-start.md`
- Intent=EXISTING_PROJECT → Load `workflows/brownfield-quick-start.md`

**Detail Guides** (load ONLY when):
- User asks specific questions → Load relevant `guides/*.md`
- User is stuck on a step → Load step details
- User requests examples → Load `examples/*.md`

**How to Load**:
```
Use Read tool with specific file path
Extract only relevant sections if file is large
Never load entire directories
Never load "just in case"
```

**Example Loading**:
```
User: "I want to start a new project with SDD"
→ Intent: NEW_PROJECT
→ Read: references/workflows/greenfield-quick-start.md
→ Present overview
→ Wait for next user action
```

## Key Integration Points

**Other Claude Code Skills**:
- `project-memory`: Document SDD decisions and patterns
- `design-doc-mermaid`: Visualize architecture from plan.md
- `github-workflows`: Automate SDD artifact validation

**External Tools**:
- `specify-cli`: Core SDD tool (via uv package manager)
- `uv`: Package manager for specify-cli installation
- Git: Version control for artifacts

**AI Agents**:
- Claude Code (primary)
- GitHub Copilot, Cursor, Windsurf (supported)

## Error Handling

**If Resource Not Found**:
1. Check if file path is correct
2. Fall back to inline basic guidance
3. Direct user to GitHub Spec-Kit docs: https://github.com/github/spec-kit
4. Suggest manual workflow steps

**If Over Token Budget**:
1. Load workflow quick-start ONLY (skip details)
2. Provide summary instead of full examples
3. Offer to load detailed sections on-demand
4. Track and report token usage to user

**If Intent Unclear**:
1. Ask clarifying question: "Are you starting a new project or working with existing code?"
2. Present decision tree options
3. Default to Installation guide if truly unclear

**If Workflow Fails**:
1. Check prerequisites (uv installed, specify-cli installed)
2. Verify command syntax
3. Load troubleshooting from relevant workflow guide
4. Reference GitHub Spec-Kit issues

## Quick Start Guidance

**For absolute beginners**, provide this inline minimal guidance:

### New Project (Greenfield)
```bash
# 1. Install specify-cli
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git

# 2. Initialize project
specify init my-project --ai claude

# 3. In AI agent, run these commands in sequence:
/speckit.constitution    # Define project principles
/speckit.specify         # Define requirements
/speckit.plan            # Technical planning
/speckit.tasks           # Break down tasks
/speckit.implement       # Execute
```

### Existing Project (Brownfield)
```bash
# 1. Install specify-cli (same as above)

# 2. In AI agent:
/speckit.brownfield         # Analyze existing code
specify init --here --force # Initialize in current dir
/speckit.analyze-codebase   # Generate constitution
/speckit.specify            # Specify new feature
/speckit.integration-plan   # Plan integration
/speckit.tasks              # Break down
/speckit.implement          # Execute
```

**After providing this**, route to full workflow guide for details.

## Maintainers

Den Delimarsky (@localden), John Lam (@jflam)

---

**For comprehensive documentation, see**:
- Greenfield: `references/workflows/greenfield-quick-start.md`
- Brownfield: `references/workflows/brownfield-quick-start.md`
- Feature Management: `references/guides/feature-management-quick.md`
- Installation: `references/sdd_install.md`
