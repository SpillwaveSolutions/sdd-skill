# Feature Status Dashboard Template

Detailed multi-feature status display for when users request comprehensive progress overview.

## Template Format

```markdown
## Feature Status Dashboard

### 📊 Overall Progress
[●●●○○○] 50% Complete | 1 of 3 features delivered

---

### 🎯 Current Feature: [feature-name]
**Phase**: [phase-name] ([X] of [Y] steps complete)
**Started**: [date or "just now"]
**Status**: [In Progress | Blocked | Ready for Next Step]

**Artifacts Generated**:
- ✅ constitution.md
- ✅ specify.md
- ✅ plan.md
- ⏳ tasks.md (in progress)
- ⏹️ implementation (not started)

**Next Action**: [Specific command to run next]

---

### 📋 Feature Pipeline

| Feature | Phase | Progress | Status |
|---------|-------|----------|--------|
| [Feature 1] | [Phase] | [●●●●●●] 100% | ✅ Complete |
| [Feature 2] | [Phase] | [●●●○○○] 50% | 🔄 Active |
| [Feature 3] | [Phase] | [○○○○○○] 0% | ⏹️ Queued |

---

### 🔗 Dependencies
[If any features depend on others, show dependency graph or list]

**Example**:
- `social-sharing` depends on `user-authentication` (must complete first)
- `photo-albums` can be built in parallel

---

### ⚠️ Blockers
[List any blockers or issues preventing progress]

**Example**:
- Waiting for API key setup before implementing authentication
- Design review needed for social-sharing UI mockups

---

### 📅 Timeline (if applicable)
- **Week 1**: photo-albums (complete ✅)
- **Week 2**: user-authentication (in progress 🔄)
- **Week 3**: social-sharing (queued ⏹️)
```

---

## Example: Mid-Project Dashboard

```markdown
## Feature Status Dashboard

### 📊 Overall Progress
[●●●●○○] 67% Complete | 1 of 3 features delivered

---

### 🎯 Current Feature: user-authentication
**Phase**: Planning (3 of 6 steps complete)
**Started**: 2 hours ago
**Status**: Ready for Next Step

**Artifacts Generated**:
- ✅ constitution.md (shared across all features)
- ✅ specify.md (requirements documented)
- ✅ plan.md (tech stack: JWT + OAuth2)
- ⏹️ tasks.md (not started)
- ⏹️ implementation (not started)

**Next Action**: Run `/speckit.tasks` to break down implementation

---

### 📋 Feature Pipeline

| Feature | Phase | Progress | Status |
|---------|-------|----------|--------|
| photo-albums | Implemented | [●●●●●●] 100% | ✅ Complete |
| user-authentication | Planning | [●●●○○○] 50% | 🔄 Active |
| social-sharing | Queued | [○○○○○○] 0% | ⏹️ Queued |

---

### 🔗 Dependencies
- `social-sharing` depends on `user-authentication` (blocked until auth complete)
- `photo-albums` was independent (completed first)

**Recommendation**: Complete user-authentication before starting social-sharing to avoid rework.

---

### ⚠️ Blockers
No blockers currently. All dependencies available, tools installed, environment ready.

---

### 📅 Timeline
- **Day 1**: photo-albums (complete ✅)
- **Day 2**: user-authentication (in progress 🔄)
- **Day 3**: social-sharing (planned ⏹️)
```

---

## Example: Project Start Dashboard

```markdown
## Feature Status Dashboard

### 📊 Overall Progress
[●○○○○○] 17% Complete | 0 of 3 features delivered

---

### 🎯 Current Feature: photo-albums
**Phase**: Constitution (1 of 6 steps complete)
**Started**: Just now
**Status**: Ready for Next Step

**Artifacts Generated**:
- ✅ constitution.md (project principles defined)
- ⏹️ specify.md (not started)
- ⏹️ plan.md (not started)
- ⏹️ tasks.md (not started)
- ⏹️ implementation (not started)

**Next Action**: Run `/speckit.specify` to define photo-albums requirements

---

### 📋 Feature Pipeline

| Feature | Phase | Progress | Status |
|---------|-------|----------|--------|
| photo-albums | Constitution | [●○○○○○] 17% | 🔄 Active |
| user-authentication | Queued | [○○○○○○] 0% | ⏹️ Queued |
| social-sharing | Queued | [○○○○○○] 0% | ⏹️ Queued |

---

### 🔗 Dependencies
- No dependencies yet (all features can be built independently)
- Will reassess after specifications are complete

---

### ⚠️ Blockers
No blockers. Project just initialized, ready to proceed.

---

### 📅 Timeline
**Estimated** (based on 6-step workflow per feature):
- **Today**: photo-albums specification + planning
- **Tomorrow**: photo-albums implementation
- **This week**: All 3 features complete
```

---

## When to Show Dashboard

### Show Full Dashboard When:
- User explicitly asks: "show feature status", "what's the progress", "show dashboard"
- User selects option **[D] Status** from feedback options
- Switching context between multiple features
- At project milestones (first feature complete, halfway through pipeline, etc.)

### Don't Show Dashboard When:
- After routine command completion (use brief status instead)
- During installation or setup
- When answering methodology questions
- In the middle of active implementation (would interrupt flow)

---

## Customization Options

### Minimal Dashboard (2 features or less)
Omit the "Feature Pipeline" table, just show current feature details and next feature.

### Large Projects (5+ features)
- Group features by category or epic
- Show only top 5 in pipeline, link to full list
- Add filtering options (by status, by dependency, by timeline)

### Brownfield Projects
Add additional sections:
- **Legacy Code Analysis**: Summary of existing codebase findings
- **Integration Points**: Where new features touch existing code
- **Migration Progress**: If modernizing legacy features

---

## Usage Notes

**Placement**: Show dashboard in response to status requests, not automatically embedded in summaries (too verbose).

**Update Frequency**: Update whenever feature status changes (phase transition, completion, blocking issue).

**Link to Brief**: Always offer brief status line as alternative for users who want quick summary.

Example response pattern:
```markdown
Here's your complete feature status dashboard:

[Full dashboard content]

---

**TL;DR**: [brief status line from feature-status-brief.md]
```
