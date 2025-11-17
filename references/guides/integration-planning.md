# Integration Planning for Brownfield Projects

How to plan integration of new features with existing codebases.

## Token Budget

**Tier 1**: 100 tokens (already loaded)
**Tier 2**: 2,000 tokens (already loaded)
**Tier 3 (this guide)**: ~1,250 tokens

**Current total**: 3,350 tokens
**Remaining budget**: 6,650 tokens ✅

---

## When to Create Integration Plans

Use integration planning when:
- Adding new feature to existing codebase
- New feature depends on existing features
- New feature will be consumed by existing code
- Modifying existing features as part of implementation
- Risk of breaking existing functionality

**Skip integration planning** when:
- Greenfield project (no existing code)
- Fully isolated microservice (no shared code)
- POC/prototype that won't interact with production code

---

## Integration Plan Command

```
/speckit.integration-plan
```

**Run after**: `/speckit.specify` (requirements defined)
**Run before**: `/speckit.tasks` (task breakdown)

**Purpose**: Identify and plan how new feature integrates with existing codebase.

---

## Integration Plan Contents

### 1. Integration Points

**Where new code touches existing code**:

```markdown
## Integration Points

### Consumes Existing Code
- **User Service** (`services/userService.js`)
  - Calls: `userService.findById(userId)`
  - Reason: New feature needs authenticated user data
  - Risk: Medium (user service is stable, widely used)

- **Email Service** (`services/emailService.js`)
  - Calls: `emailService.send(template, recipient, data)`
  - Reason: Send notification emails for new feature
  - Risk: Low (well-documented API)

### Consumed By Existing Code
- **Dashboard** (`components/Dashboard.tsx`)
  - Integration: Dashboard will display new feature's data
  - Modification needed: Add new widget component
  - Risk: Low (additive change only)

- **API Gateway** (`routes/api.js`)
  - Integration: Register new feature's routes
  - Modification needed: Add route imports
  - Risk: Low (standard pattern)

### Shared Resources
- **Database** (PostgreSQL via Prisma)
  - New tables: `tasks`, `task_assignments`
  - Foreign keys: References `users` table
  - Migrations: Required before deployment
  - Risk: Medium (schema changes require coordination)

- **Redis Cache**
  - New keys: `task:${id}`, `user:${id}:tasks`
  - Namespace: `tasks:*` for feature-specific keys
  - TTL: 5 minutes for task data
  - Risk: Low (separate namespace)
```

### 2. Required Modifications to Existing Code

**Changes to existing files**:

```markdown
## Modifications to Existing Code

### High Priority (Blocking)

**1. User Model** (`models/User.js`)
- **Change**: Add `hasTasks()` method
- **Why**: Dashboard needs to check if user has tasks
- **Impact**: Low (additive method, no breaking changes)
- **Files affected**: 1
- **Tests needed**: Unit test for new method

**2. Database Schema** (`prisma/schema.prisma`)
- **Change**: Add `Task` and `TaskAssignment` models
- **Why**: New feature requires task storage
- **Impact**: Medium (requires migration, affects production DB)
- **Files affected**: 1
- **Migration script**: `prisma migrate dev --name add_tasks`
- **Tests needed**: Integration tests for new relationships

### Medium Priority (Important)

**3. API Gateway** (`routes/api.js`)
- **Change**: Register `/api/tasks/*` routes
- **Why**: Expose new feature's endpoints
- **Impact**: Low (additive change)
- **Files affected**: 1
- **Tests needed**: Route registration test

### Low Priority (Nice to Have)

**4. Dashboard** (`components/Dashboard.tsx`)
- **Change**: Add `<TaskWidget />` component
- **Why**: Display tasks on main dashboard
- **Impact**: Low (optional UI enhancement)
- **Files affected**: 2 (Dashboard.tsx, new TaskWidget.tsx)
- **Tests needed**: Component render test
```

### 3. Sequencing and Dependencies

**Implementation order**:

```markdown
## Implementation Sequence

### Phase 1: Database Foundation (Day 1)
1. Create Prisma migration for Task models
2. Run migration on dev database
3. Test database constraints and relationships
4. **Blocking**: Must complete before Phase 2

### Phase 2: Core Feature (Day 2)
5. Implement task service layer
6. Create task API endpoints
7. Add task repository
8. **Depends on**: Phase 1 (database schema)
9. **Blocking**: Must complete before Phase 3

### Phase 3: Integration (Day 3)
10. Modify User model to add `hasTasks()`
11. Register task routes in API gateway
12. **Depends on**: Phase 2 (task endpoints exist)

### Phase 4: UI Integration (Day 4)
13. Create TaskWidget component
14. Integrate TaskWidget into Dashboard
15. **Depends on**: Phase 2 (API available)
16. **Optional**: Can ship without this phase

**Critical Path**: Phase 1 → Phase 2 → Phase 3 (3 days minimum)
**Full Feature**: Phase 1 → Phase 2 → Phase 3 → Phase 4 (4 days)
```

### 4. Risk Assessment

**Potential issues and mitigation**:

```markdown
## Integration Risks

### High Risk

**R1: Database Migration Failure**
- **Impact**: Production downtime, data loss
- **Probability**: Low (Prisma handles migrations well)
- **Mitigation**:
  1. Test migration on staging database first
  2. Take database backup before production migration
  3. Have rollback script ready
  4. Schedule migration during low-traffic window

**R2: Breaking Changes to User Model**
- **Impact**: 15+ files use User model, potential widespread breakage
- **Probability**: Medium (adding method is generally safe, but...)
- **Mitigation**:
  1. Make new method optional (return `null` if feature disabled)
  2. Add feature flag to control new behavior
  3. Run full test suite before merging
  4. Gradual rollout with feature flag

### Medium Risk

**R3: API Route Conflicts**
- **Impact**: Existing routes might conflict with `/api/tasks/*`
- **Probability**: Low (route namespace available)
- **Mitigation**:
  1. Check existing routes for conflicts
  2. Use unique prefix if needed (`/api/v2/tasks/`)

**R4: Performance Impact on Dashboard**
- **Impact**: Adding TaskWidget may slow dashboard load
- **Probability**: Medium (additional API call + rendering)
- **Mitigation**:
  1. Lazy load TaskWidget (only render when visible)
  2. Cache task data in Redis (5 min TTL)
  3. Pagination for task list (show max 10 recent)

### Low Risk

**R5: Redis Key Collision**
- **Impact**: Cache keys conflict with existing features
- **Probability**: Very Low (using namespace)
- **Mitigation**:
  1. Use `tasks:*` namespace consistently
  2. Document key patterns in integration plan
```

---

## Integration Strategies

### Strategy 1: Adapter Pattern

**Use when**: New feature's API doesn't match existing patterns

**Example**:
```markdown
## Integration Strategy: Adapter Pattern

**Problem**: Existing User Service expects synchronous calls, but new Task Service is async.

**Solution**: Create adapter layer
```typescript
// adapters/userServiceAdapter.ts
export class UserServiceAdapter {
  async getUserTasks(userId: string) {
    const user = await userService.findById(userId); // existing sync call
    const tasks = await taskService.findByUser(userId); // new async call
    return { user, tasks };
  }
}
```

**Benefits**:
- Isolates new feature from existing code patterns
- Easier to test
- Can be removed later if existing services refactored

**Costs**:
- Additional layer adds complexity
- Slight performance overhead
```

### Strategy 2: Feature Flags

**Use when**: Want to deploy without immediately exposing new feature

**Example**:
```markdown
## Integration Strategy: Feature Flags

**Implementation**:
```typescript
// config/features.ts
export const features = {
  tasks: process.env.FEATURE_TASKS === 'true',
};

// components/Dashboard.tsx
{features.tasks && <TaskWidget />}

// routes/api.js
if (features.tasks) {
  app.use('/api/tasks', taskRoutes);
}
```

**Benefits**:
- Deploy code without exposing to users
- Gradual rollout (enable for 10%, 50%, 100% of users)
- Quick rollback if issues discovered

**Deployment Plan**:
1. Day 1: Deploy with flag OFF (smoke test in production)
2. Day 2: Enable for internal users only
3. Day 3: Enable for 10% of users
4. Day 4: Enable for 50% of users
5. Day 5: Enable for 100% of users
```

### Strategy 3: Parallel Endpoints

**Use when**: Replacing existing functionality with new implementation

**Example**:
```markdown
## Integration Strategy: Parallel Endpoints

**Problem**: Replacing old task management with new approach.

**Solution**: Run both old and new endpoints in parallel

**Old Endpoints** (keep during migration):
- GET /api/tasks (legacy)
- POST /api/tasks (legacy)

**New Endpoints** (new implementation):
- GET /api/v2/tasks (new)
- POST /api/v2/tasks (new)

**Migration Path**:
1. Deploy new endpoints (v2)
2. Update frontend to use v2 endpoints
3. Monitor both endpoints for parity
4. After 2 weeks of v2 usage, deprecate v1
5. After 4 weeks, remove v1 endpoints

**Validation**: Shadow traffic - send requests to both v1 and v2, compare responses
```

### Strategy 4: Strangler Fig Pattern

**Use when**: Gradually migrating legacy feature to new implementation

**Example**:
```markdown
## Integration Strategy: Strangler Fig

**Problem**: Old task system tightly coupled to entire codebase.

**Solution**: Gradually replace old with new, route-by-route

**Phase 1**: New endpoints for new functionality
- `/api/tasks/assignments` (new feature, not in old system)

**Phase 2**: Reimplement read endpoints
- `/api/tasks` GET (reimplemented, same API contract)
- `/api/tasks/:id` GET (reimplemented)

**Phase 3**: Reimplement write endpoints
- `/api/tasks` POST (reimplemented)
- `/api/tasks/:id` PUT (reimplemented)

**Phase 4**: Migrate data and remove old code
- Migrate legacy task data to new schema
- Remove old task system entirely

**Timeline**: 3-6 months for complete migration
```

---

## Integration Testing

### Test Integration Points

```markdown
## Integration Tests Required

### User Service Integration
```typescript
// tests/integration/user-task-integration.test.ts
test('user can retrieve their tasks', async () => {
  const user = await createTestUser();
  const task = await createTestTask({ assignedTo: user.id });

  const tasks = await user.getTasks(); // new method

  expect(tasks).toHaveLength(1);
  expect(tasks[0].id).toBe(task.id);
});
```

### Database Integration
```typescript
// tests/integration/database.test.ts
test('task references valid user', async () => {
  const user = await createTestUser();

  const task = await prisma.task.create({
    data: { title: 'Test', assignedTo: user.id }
  });

  expect(task.assignedTo).toBe(user.id);

  // Test foreign key constraint
  await expect(prisma.task.create({
    data: { title: 'Test', assignedTo: 'invalid-id' }
  })).rejects.toThrow();
});
```

### API Integration
```typescript
// tests/integration/api.test.ts
test('task API routes registered', async () => {
  const response = await request(app).get('/api/tasks');

  expect(response.status).not.toBe(404); // route exists
});
```
```

---

## After Integration Planning

### Include Integration Tasks in Task Breakdown

When running `/speckit.tasks`, ensure:
- Integration modifications are separate tasks
- Dependencies are explicit (e.g., "Depends on Task 5")
- Risk mitigation steps are included

**Example task structure**:
```markdown
## Integration Tasks

### Task 12: Modify User Model
**Type**: Integration
**Priority**: High
**Depends on**: Tasks 8-11 (core task service implemented)
**Files**: `models/User.js`
**Changes**: Add `async hasTasks()` method
**Tests**: `tests/models/User.test.js`
**Risk**: Low (additive change)
**Mitigation**: Make method optional, feature flag controlled

### Task 13: Database Migration
**Type**: Integration
**Priority**: High (blocking)
**Depends on**: Nothing (can run first)
**Files**: `prisma/schema.prisma`
**Changes**: Add Task and TaskAssignment models
**Migration**: `prisma migrate dev --name add_tasks`
**Tests**: `tests/integration/database.test.js`
**Risk**: Medium (schema change)
**Mitigation**: Test on staging, backup before prod migration
```

---

## Troubleshooting

### Integration Conflicts

**Existing code breaks after integration**:
1. Check if modifications followed adapter pattern
2. Review test coverage for integration points
3. Use feature flags to isolate new code
4. Consider parallel endpoints during migration

**Performance degradation**:
1. Check if new code introduces N+1 queries
2. Add caching at integration boundaries
3. Use lazy loading for UI components
4. Profile API endpoints before/after integration

**Dependency cycles**:
1. New feature depends on existing code that depends on new feature
2. Solution: Introduce interface/abstraction to break cycle
3. Or: Refactor existing code to remove dependency

---

## Next Steps

- Return to brownfield workflow: `references/workflows/brownfield-quick-start.md`
- Create task breakdown: Run `/speckit.tasks` (will include integration tasks)
- Review reverse-engineering: `references/guides/reverse-engineering.md` (for discovering integration points)
