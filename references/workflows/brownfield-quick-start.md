# Brownfield Workflow Quick Start

## Token Budget

**Tier 1**: 100 tokens (already loaded)
**Tier 2**: 2,000 tokens (already loaded)
**Tier 3 (this guide)**: ~1,500 tokens

**Additional resources available**:
- Codebase analysis: `references/guides/codebase-analysis.md` (+1,250 tokens)
- Reverse engineering: `references/guides/reverse-engineering.md` (+1,250 tokens)
- Integration planning: `references/guides/integration-planning.md` (+1,250 tokens)

**Current total**: 3,600 tokens
**Remaining budget**: 6,400 tokens ✅

---

## When to Use Brownfield Workflow

Use this workflow when:
- Adding features to an existing codebase
- Modernizing or refactoring legacy systems
- Adopting SDD methodology in an ongoing project
- Reverse-engineering existing code into SDD format
- Migrating from traditional development to spec-driven

**For new projects from scratch**, use [Greenfield Workflow](greenfield-quick-start.md) instead.

---

## The 7-Step Workflow

### Step 1: Analyze Existing Codebase

```
/speckit.brownfield
```

**Purpose**: Analyze existing code to understand architecture, patterns, and tech stack.

**What this does**: Scans codebase and identifies:
- Architecture and design patterns
- Technology stack and dependencies
- Coding standards and conventions
- Technical debt and opportunities

**After this command**: Load `references/templates/10-point-summary-template.md` and summarize analysis.

→ **For analysis depth options**, load `references/guides/codebase-analysis.md`

---

### Step 2: Initialize SDD in Existing Project

```bash
specify init --here --force
```

**What this does**: Creates `.speckit/` directory structure in existing project without conflicting with existing files.

**Flags explained**:
- `--here`: Initialize in current directory
- `--force`: Override warnings about existing files

---

### Step 3: Generate Constitution from Existing Code

```
/speckit.analyze-codebase
```

**Purpose**: Create constitution.md that acknowledges existing patterns and standards.

**What gets created**: `.speckit/constitution.md` with:
- Architectural principles (derived from existing code)
- Established patterns and conventions
- Technology constraints and standards
- Future direction or planned migrations

**After this command**: Load `references/templates/10-point-summary-template.md` and summarize.

---

### Step 4: Choose Documentation Strategy

**Interactive decision point** - Choose based on your needs:

#### Option A: Constitution Only
Generate constitution.md only, use for new features going forward.
→ **Best for**: Teams adopting SDD for future work only.

#### Option B: Constitution + Baseline Specs
Generate constitution.md and high-level specs for existing major features.
→ **Best for**: Partial documentation, focus on key features.

#### Option C: Full Reverse-Engineering
Document all existing features comprehensively.
→ **Best for**: Complete documentation, migration to SDD.

---

### Step 5: Reverse-Engineer (Optional)

```
/speckit.reverse-engineer
```

**Purpose**: Document existing features in SDD format.

**What gets created**: For each discovered feature:
- `specify.md`: Requirements reverse-engineered from code
- Mapping to existing code files
- Integration points

**After this command**: Load `references/templates/10-point-summary-template.md` and summarize.

→ **For detailed guidance**, load `references/guides/reverse-engineering.md`

---

### Step 6: Specify New Feature

```
/speckit.specify
```

**Purpose**: Define new feature to add to existing codebase.

**Same as greenfield**, but emphasize:
- Integration points with existing code
- Dependencies on existing features
- Constraints from existing architecture

**After this command**: Load `references/templates/10-point-summary-template.md` and summarize.

---

### Step 7a: Create Integration Plan

```
/speckit.integration-plan
```

**Purpose**: Plan how new feature integrates with existing codebase.

**What gets created**: Integration plan with:
- Integration points (where new code touches existing)
- Required modifications to existing code
- Sequencing and dependencies
- Risk assessment

**After this command**: Load `references/templates/10-point-summary-template.md` and summarize.

→ **For integration strategies**, load `references/guides/integration-planning.md`

---

### Step 7b: Break Down into Tasks

```
/speckit.tasks
```

**Purpose**: Create task list including both new code and integration work.

**Brownfield-specific tasks include**:
- Integration tasks (modifying existing files)
- Compatibility tasks (ensuring new code works with old)
- Migration tasks (if refactoring existing code)

**After this command**: Load `references/templates/10-point-summary-template.md` and summarize.

---

### Step 8: Execute Implementation

```
/speckit.implement
```

**Purpose**: Execute all tasks including integration work.

**Brownfield considerations**:
- Respect existing patterns
- Minimize breaking changes
- Test integration thoroughly
- Consider gradual rollout

---

## Analysis Depth Options

### Surface Analysis (~5 min)
- File structure and organization
- Technology stack identification
- Basic pattern recognition

→ **Choose when**: Quick overview needed, small codebase

### Moderate Analysis (~15 min)
- Architecture patterns in detail
- Coding standards extraction
- Dependency mapping
- Technical debt identification

→ **Choose when**: Standard brownfield adoption, medium codebase

### Deep Analysis (~30+ min)
- Comprehensive feature inventory
- Complete reverse-engineering
- Integration point mapping
- Performance baseline

→ **Choose when**: Large migration, enterprise adoption, complex codebase

→ **For choosing depth**, load `references/guides/codebase-analysis.md`

---

## Validation Commands

After documenting existing code, validate the reverse-engineering:

```
/speckit.validate-reverse-engineering   # Verify spec accuracy
/speckit.coverage-check                 # Check documentation coverage
/speckit.validate-constitution          # Verify constitution consistency
/speckit.trace [feature]                # Map specs to code
```

---

## Common Brownfield Scenarios

### Scenario 1: Add Single Feature to Existing App
```
/speckit.brownfield              # Analyze
specify init --here --force      # Initialize
/speckit.analyze-codebase        # Generate constitution
/speckit.specify                 # Specify new feature
/speckit.integration-plan        # Plan integration
/speckit.tasks                   # Break down
/speckit.implement               # Execute
```

### Scenario 2: Modernize Legacy System
```
/speckit.brownfield              # Deep analysis
/speckit.reverse-engineer        # Document existing
/speckit.specify                 # Modern replacement feature
/speckit.integration-plan        # Migration strategy
/speckit.tasks                   # Include migration tasks
```

### Scenario 3: Extract Microservice
```
/speckit.brownfield              # Analyze monolith
/speckit.reverse-engineer        # Document target functionality
/speckit.specify                 # New microservice spec
/speckit.integration-plan        # Service boundaries, API contracts
/speckit.tasks                   # Extraction + integration tasks
```

---

## Best Practices for Brownfield

1. **Respect existing patterns** - Constitution should acknowledge current architecture
2. **Incremental adoption** - Don't try to document everything at once
3. **Focus on integration** - New features must play well with existing code
4. **Test thoroughly** - Integration points are high-risk areas
5. **Gradual refactoring** - Use new features to gradually improve architecture

---

## Troubleshooting

**If analysis fails**:
1. Check if codebase too large (>100k lines may need manual scoping)
2. Verify read permissions on all files
3. Try surface analysis first, then moderate

**If integration conflicts**:
1. Review constitution for architecture constraints
2. Load `references/guides/integration-planning.md` for strategies
3. Consider creating adapter layer

**If unclear about strategy**:
1. Start with Constitution Only (Option A)
2. Add reverse-engineering later if needed
3. Focus on new features first

---

## Related Resources

**Need more details?**
- Codebase analysis strategies: `references/guides/codebase-analysis.md`
- Reverse-engineering guide: `references/guides/reverse-engineering.md`
- Integration planning: `references/guides/integration-planning.md`
- Summary template: `references/templates/10-point-summary-template.md`
- Feature management: `references/guides/feature-management-quick.md`

**New project**: `references/workflows/greenfield-quick-start.md`
**Installation help**: `references/sdd_install.md`
