# Feature Management Quick Guide

Natural language feature management for SDD projects.

## Token Budget

**Tier 1**: 100 tokens (already loaded)
**Tier 2**: 2,000 tokens (already loaded)
**Tier 3 (this guide)**: ~1,000 tokens

**Current total**: 3,100 tokens
**Remaining budget**: 6,900 tokens ✅

---

## Overview

Claude automatically tracks features and provides natural language management - no manual tracking needed.

**Works for**: Both greenfield and brownfield projects
**When**: After first `/speckit.specify` or when planning multiple features

---

## Natural Language Commands

### Add Features

**Just describe what you want**:
- "Add a new feature for user notifications"
- "We need email integration"
- "Let's add an admin dashboard"

**Claude will**:
1. Detect the feature request
2. Ask: Priority? Dependencies? Description?
3. Create feature entry
4. Show updated status

**Example**:
```
You: "Add a feature for user notifications"

Claude: I'll add "user-notifications". A few questions:
1. Priority: High/Medium/Low?
2. Dependencies: Depends on any existing features?
3. Brief description?

[You answer...]

Claude:
✅ Feature added: user-notifications

📊 Updated Feature List:
1. user-authentication (In Progress - 80%)
2. profile-management (Pending)
3. user-notifications (Pending) ← NEW
```

---

### Reorder Features

**Natural commands**:
- "Move user-notifications before profile-management"
- "Let's do admin-dashboard first"
- "Prioritize email integration"

**Example**:
```
You: "Let's do user-notifications before profile-management"

Claude:
Current: auth → profile → notifications
Proposed: auth → notifications → profile ← MOVED UP

This will update dependencies if needed.
Confirm? (yes/no)

[You: yes]

✅ Feature order updated!
📊 Next: user-notifications
```

---

### Remove Features

**Natural commands**:
- "Remove the reporting feature"
- "Delete admin-dashboard"
- "We don't need email integration"

**Example**:
```
You: "Remove the reporting feature"

Claude:
⚠️ Warning: Remove 'reporting'?

Impact:
- Depending features: None
- Progress lost: 0% (not started)
- Artifacts: None

Confirm? (yes/no)

[You: yes]

✅ Feature 'reporting' removed
```

---

### Show Status

**Natural commands**:
- "Show feature status"
- "What's the current progress?"
- "Show me the feature dashboard"

**Displays**:
```
📊 Project Feature Status Dashboard

🎯 CURRENT FEATURE
├─ profile-management (Planning - 40%)
│  ├─ ✅ Requirements specified
│  ├─ 🔄 Implementation plan in progress
│  ├─ ⏸️  Tasks not started
│  └─ ⏸️  Implementation not started
│  Blockers: None

📋 FEATURE PIPELINE
┌─────────────┬───────┬──────────┬─────────────┐
│ Feature     │ Phase │ Progress │ Status      │
├─────────────┼───────┼──────────┼─────────────┤
│ auth        │ Done  │ [●●●●●●]│ ✅ Complete │
│ profile     │ Plan  │ [●●○○○○]│ 🔄 Active   │
│ notifications│ Queue│ [○○○○○○]│ ⏹️  Queued  │
│ admin       │ Queue │ [○○○○○○]│ ⏹️  Queued  │
└─────────────┴───────┴──────────┴─────────────┘

🔗 DEPENDENCIES
- notifications depends on auth (satisfied ✅)
- admin depends on auth (satisfied ✅)

⚠️ BLOCKERS: None
```

---

## Automatic Tracking

### After Every SDD Command

Claude automatically:
1. Detects which feature you're working on
2. Updates progress based on completed step
3. Shows brief status line in summary

**Example after `/speckit.plan`**:
```
## Technical Plan Summary

📊 Feature Status: profile-management (Planned) → Next: notifications
Progress: [●●●○○○] 50% | Completed: 1 of 3 features

[rest of summary...]
```

---

## Progress Tracking

### Workflow Phases

**Greenfield** (6 steps = 100%):
- Constitution: 17%
- Specify: 33%
- Plan: 50%
- Tasks: 67%
- Implement start: 83%
- Implement complete: 100%

**Brownfield** (8 steps = 100%):
- Analyze: 12%
- Constitution: 25%
- Reverse-engineer: 37%
- Specify: 50%
- Integration plan: 62%
- Tasks: 75%
- Implement start: 87%
- Implement complete: 100%

### Multiple Features

**Overall progress** = Average across all features

Example:
- Feature 1: 100% (complete)
- Feature 2: 50% (planning)
- Feature 3: 0% (queued)
- **Average**: 50% project complete

---

## Feature Dependencies

### Declaring Dependencies

When adding feature, specify dependencies:
```
You: "Add social sharing feature"

Claude: Dependencies?

You: "Depends on user-authentication"

Claude:
✅ Feature added with dependency

⚠️ Note: social-sharing blocked until auth complete
```

### Auto-Detection

Claude also detects implicit dependencies:
- Reading from same database tables
- Calling same services
- Similar integration points

**Example**:
```
Claude: I noticed 'social-sharing' and 'notifications' both
        use the Email Service. Consider implementing
        notifications first to establish email patterns.

Would you like to reorder? (yes/no)
```

---

## Best Practices

### Start Small
- 1st project: 1-2 features maximum
- Learn workflow before scaling
- Add more features once comfortable

### Plan Dependencies
- Authentication usually first
- Core features before enhancements
- Data models before UI

### Review Before Reordering
- Check dependency impact
- Consider implementation complexity
- Balance business value vs. technical foundation

### Use Status Dashboard
- Request after each completed feature
- Track before starting new feature
- Monitor blockers proactively

---

## Integration with Workflows

### Greenfield
```
specify init →
/speckit.constitution →
/speckit.specify [Feature 1] →
  "Add features: [F2], [F3]" ← Feature management starts
  /speckit.plan [Feature 1] →
  /speckit.tasks [Feature 1] →
  /speckit.implement [Feature 1] →
"Show status" → [F1 complete, start F2]
/speckit.specify [Feature 2] →
...
```

### Brownfield
```
/speckit.brownfield →
specify init --here →
/speckit.analyze-codebase →
/speckit.specify [New Feature 1] →
  "Add features: [NF2], [NF3]" ← Feature management
  /speckit.integration-plan [Feature 1] →
  /speckit.tasks [Feature 1] →
  /speckit.implement [Feature 1] →
...
```

---

## Troubleshooting

### Features Not Tracked

**Problem**: Claude doesn't show feature status
**Solution**:
1. Explicitly mention multiple features: "I want to build auth, profile, and admin features"
2. Or ask: "Can you track these features?"

### Wrong Feature Active

**Problem**: Claude working on wrong feature
**Solution**: "Let's switch to [feature-name]" or "Let's work on [feature-name] next"

### Lost Feature List

**Problem**: Feature list disappeared after restart
**Solution**:
- Features stored in `.speckit/features/` directory
- Ask: "Show feature status" to rebuild list
- Or: "What features have we specified?"

### Dependency Conflicts

**Problem**: Feature X depends on Y, but Y depends on X
**Solution**:
1. Identify circular dependency
2. Refactor: Extract shared logic to new feature Z
3. Both X and Y depend on Z (no cycle)

---

## Feature Metadata

Features tracked with:
- **Name**: Slug format (user-authentication)
- **Priority**: High/Medium/Low
- **Dependencies**: List of feature names
- **Phase**: Constitution/Specify/Plan/Tasks/Implement/Complete
- **Progress**: 0-100%
- **Blockers**: Any blocking issues
- **Artifacts**: Generated `.speckit/features/` files

---

## Next Steps

- **For detailed dashboard format**: Load `references/templates/feature-status-dashboard.md`
- **For brief status format**: Load `references/templates/feature-status-brief.md`
- **Return to workflow**: `references/workflows/greenfield-quick-start.md` or `brownfield-quick-start.md`
