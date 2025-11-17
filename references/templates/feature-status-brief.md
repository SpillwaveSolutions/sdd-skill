# Feature Status Brief Template

Concise single-line status format for embedding in summaries after SDD commands.

## Template Format

```markdown
📊 Feature Status: [current-feature] ([phase]) → Next: [next-feature]
Progress: [●●●○○] [percentage]% | Completed: [X] of [Y] features
```

---

## Examples

### Single Feature In Progress
```markdown
📊 Feature Status: photo-albums (Planning) → Next: None
Progress: [●●○○○] 40% | Completed: 0 of 1 feature
```

### Multiple Features - Constitution Phase
```markdown
📊 Feature Status: user-authentication (Constitution) → Next: photo-albums, social-sharing
Progress: [●○○○○] 20% | Completed: 0 of 3 features
```

### Multiple Features - Mid-Implementation
```markdown
📊 Feature Status: photo-albums (Tasks) → Next: user-authentication, social-sharing
Progress: [●●●●○] 80% | Completed: 0 of 3 features
```

### One Feature Complete, Others Pending
```markdown
📊 Feature Status: user-authentication (Specify) → Next: photo-albums, social-sharing
Progress: [●●●○○○] 50% | Completed: 1 of 3 features
```

### All Features Complete
```markdown
📊 Feature Status: All features complete ✅
Progress: [●●●●●] 100% | Completed: 3 of 3 features
```

---

## Phase Labels

Use these phase labels based on the last completed command:

- **Constitution** - After `/speckit.constitution`
- **Specified** - After `/speckit.specify`
- **Planned** - After `/speckit.plan`
- **Tasks Ready** - After `/speckit.tasks`
- **In Progress** - During `/speckit.implement`
- **Complete** - After `/speckit.implement` finishes successfully

### Brownfield-Specific Phases
- **Analyzed** - After `/speckit.brownfield` or `/speckit.analyze-codebase`
- **Reverse-Engineered** - After `/speckit.reverse-engineer`
- **Integration Planned** - After `/speckit.integration-plan`

---

## Progress Bar Rules

Calculate progress based on workflow completion:

**Greenfield (6 steps)**:
- Constitution: 1/6 = 17% → [●○○○○○]
- Specify: 2/6 = 33% → [●●○○○○]
- Plan: 3/6 = 50% → [●●●○○○]
- Tasks: 4/6 = 67% → [●●●●○○]
- Implement start: 5/6 = 83% → [●●●●●○]
- Implement complete: 6/6 = 100% → [●●●●●●]

**Brownfield (8 steps including analysis)**:
- Analyze: 1/8 = 12% → [●○○○○○○○]
- Constitution: 2/8 = 25% → [●●○○○○○○]
- Reverse-engineer: 3/8 = 37% → [●●●○○○○○]
- Specify: 4/8 = 50% → [●●●●○○○○]
- Integration plan: 5/8 = 62% → [●●●●●○○○]
- Tasks: 6/8 = 75% → [●●●●●●○○]
- Implement start: 7/8 = 87% → [●●●●●●●○]
- Implement complete: 8/8 = 100% → [●●●●●●●●]

**Multiple Features**:
- Average progress across all features
- Example: Feature 1 (100%), Feature 2 (50%), Feature 3 (0%) → Average = 50%

---

## When to Show Status

### Always Show
- After any `/speckit.*` command completes
- When user asks about progress or status
- When switching between features

### Don't Show
- During initial installation
- When no features have been specified yet
- When answering general questions about SDD methodology

---

## Usage in Summaries

Place the status line at the TOP of every summary after SDD commands:

```markdown
## Constitution Summary

📊 Feature Status: photo-albums (Constitution) → Next: user-authentication
Progress: [●○○○○○] 17% | Completed: 0 of 2 features

### 🎯 What Was Created
[rest of summary...]
```

This keeps users oriented about overall project progress while reviewing specific artifacts.
