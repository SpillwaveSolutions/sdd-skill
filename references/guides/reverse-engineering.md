# Reverse-Engineering Existing Code

How to document existing features in SDD format for brownfield projects.

## Token Budget

**Tier 1**: 100 tokens (already loaded)
**Tier 2**: 2,000 tokens (already loaded)
**Tier 3 (this guide)**: ~1,250 tokens

**Current total**: 3,350 tokens
**Remaining budget**: 6,650 tokens ✅

---

## When to Reverse-Engineer

Use reverse-engineering when you need to:
- **Document existing features** in SDD format
- **Understand legacy code** before making changes
- **Create baseline specs** for existing functionality
- **Maintain documentation** alongside code
- **Onboard new team members** with executable specs

**Don't reverse-engineer** when:
- Only adding small feature to existing code (use integration plan instead)
- Codebase is disposable or being replaced
- Time-constrained and only need constitution

---

## Reverse-Engineering Command

```
/speckit.reverse-engineer
```

**Purpose**: Analyze existing code and generate SDD artifacts (specify.md, plan.md) for discovered features.

### What Gets Created

For each discovered feature:
```
.speckit/features/
├── 001-user-authentication/
│   ├── specify.md       # Requirements reverse-engineered from code
│   ├── plan.md          # Technical details extracted from implementation
│   └── mapping.md       # Links to actual source files
├── 002-task-management/
│   ├── specify.md
│   ├── plan.md
│   └── mapping.md
└── 003-notification-system/
    ├── specify.md
    ├── plan.md
    └── mapping.md
```

---

## Reverse-Engineering Strategies

### Strategy 1: Constitution Only

**Use when**: Just adopting SDD, focusing on future features only

**Process**:
1. Run `/speckit.analyze-codebase` to generate constitution
2. Skip `/speckit.reverse-engineer`
3. Start adding new features with SDD workflow

**Pros**:
- Fastest approach
- Low initial investment
- Future features immediately benefit

**Cons**:
- Existing features undocumented
- No baseline for comparison
- Integration points unclear

---

### Strategy 2: Baseline Specs for Key Features

**Use when**: Need documentation for critical features, but not entire codebase

**Process**:
1. Generate constitution
2. Run `/speckit.reverse-engineer --features "auth,payments,core-workflow"`
3. Manually review and enhance generated specs
4. Use specs as reference for new features

**Pros**:
- Documents critical paths
- Manageable scope
- Provides integration context

**Cons**:
- Incomplete picture
- Manual feature selection required
- May miss important integrations

---

### Strategy 3: Full Reverse-Engineering

**Use when**: Complete documentation needed, large migration, or comprehensive modernization

**Process**:
1. Generate constitution
2. Run `/speckit.reverse-engineer` (no filters, analyze all features)
3. Review all generated specs
4. Enhance with domain knowledge
5. Use as complete SDD baseline

**Pros**:
- Complete documentation
- All integration points mapped
- Baseline for refactoring
- Onboarding reference

**Cons**:
- Time-consuming
- May generate specs for trivial features
- Requires manual cleanup

---

## Reverse-Engineering Process

### Step 1: Feature Discovery

**Automatic discovery** looks for:
- Route definitions (Express, Flask, Django, etc.)
- Controller/handler classes
- API endpoints
- UI components
- Database models/schemas
- Business logic modules

**Example output**:
```markdown
## Discovered Features (12 total)

### High Confidence
1. **User Authentication** (15 files, 2,300 lines)
2. **Task Management** (22 files, 3,800 lines)
3. **Notification System** (8 files, 1,200 lines)

### Medium Confidence
4. **File Upload** (5 files, 600 lines)
5. **Search** (3 files, 400 lines)

### Low Confidence (might be infrastructure)
6. **Database Migrations** (12 files, 800 lines)
7. **Logging Utilities** (4 files, 300 lines)
```

### Step 2: Requirements Extraction

For each feature, generate `specify.md`:

**Extracted from**:
- Route handlers → Functional requirements
- Validation logic → Constraints
- Test cases → Success criteria
- Error handling → Edge cases
- Comments/docs → User stories (if available)

**Example** (User Authentication feature):
```markdown
# Feature: User Authentication

## Description
System for user registration, login, and session management.

## Functional Requirements (Extracted)

### FR1: User Registration
**Evidence**: POST /api/users/register endpoint in routes/users.js:15
**Logic**: Creates new user with email, password, and optional profile data
**Validation**: Email format check, password strength (8+ chars, 1 number, 1 special)
**Success**: Returns 201 with JWT token and user object

### FR2: User Login
**Evidence**: POST /api/auth/login endpoint in routes/auth.js:42
**Logic**: Validates credentials, generates JWT token
**Sessions**: Token valid for 24 hours, refresh token for 30 days

### FR3: Password Reset
**Evidence**: POST /api/auth/reset endpoint in routes/auth.js:89
**Logic**: Email-based reset flow, tokens expire in 1 hour

## Success Criteria (From Tests)
- ✅ User can register with valid email and password (auth.test.js:23)
- ✅ Login returns valid JWT token (auth.test.js:67)
- ✅ Invalid credentials return 401 (auth.test.js:91)
- ✅ Password reset email contains valid token (auth.test.js:142)

## Constraints
- Passwords hashed with bcrypt (10 rounds)
- JWT secret in environment variable
- Email service requires SendGrid API key
- Rate limit: 5 login attempts per minute per IP
```

### Step 3: Technical Plan Extraction

For each feature, generate `plan.md`:

**Extracted from**:
- File structure → Architecture
- Import statements → Dependencies
- Implementation → Technology choices
- Patterns → Design decisions

**Example** (User Authentication feature):
```markdown
# Technical Plan: User Authentication

## Architecture

**Layered Architecture**:
```
routes/auth.js (Express routes)
  ↓
controllers/authController.js (Request handling)
  ↓
services/authService.js (Business logic)
  ↓
repositories/userRepository.js (Data access)
  ↓
models/User.js (Prisma model)
```

## Technology Stack

**Backend**:
- Express 4.18.2 (routing)
- Passport.js 0.6.0 (auth strategies)
- jsonwebtoken 9.0.1 (JWT generation)
- bcrypt 5.1.0 (password hashing)

**Database**:
- PostgreSQL (via Prisma ORM)
- Users table with email, password_hash, created_at

**Email**:
- SendGrid (password reset emails)

## Key Dependencies

**Authentication Flow**:
1. User → POST /api/auth/login
2. authController validates input
3. authService.authenticate() checks credentials
4. userRepository.findByEmail() queries DB
5. bcrypt.compare() validates password
6. jwt.sign() generates token
7. Return token + user object

## Implementation Phases (Reconstructed)

**Phase 1: Core Auth** (implemented)
- User model and repository
- Registration endpoint
- Login endpoint
- JWT generation

**Phase 2: Security** (implemented)
- Password hashing
- Token refresh
- Rate limiting

**Phase 3: Password Reset** (implemented)
- Reset token generation
- Email integration
- Reset confirmation
```

### Step 4: Create File Mappings

For each feature, generate `mapping.md`:

**Links specs to actual code**:

```markdown
# Code Mapping: User Authentication

## Requirements → Code

**FR1: User Registration**
- Endpoint: `routes/users.js:15-42`
- Controller: `controllers/authController.js:23-67`
- Service: `services/authService.js:45-89`
- Validation: `middleware/validation.js:12-28`
- Tests: `tests/auth.test.js:23-56`

**FR2: User Login**
- Endpoint: `routes/auth.js:42-58`
- Controller: `controllers/authController.js:89-132`
- Service: `services/authService.js:105-145`
- Tests: `tests/auth.test.js:67-103`

**FR3: Password Reset**
- Endpoint: `routes/auth.js:89-112`
- Service: `services/authService.js:178-234`
- Email template: `templates/password-reset.html`
- Tests: `tests/auth.test.js:142-189`

## Dependencies

**Internal**:
- User model: `models/User.js`
- Email service: `services/emailService.js`
- Validation middleware: `middleware/validation.js`

**External**:
- jsonwebtoken: Token generation
- bcrypt: Password hashing
- SendGrid: Email delivery
```

---

## Validation Commands

After reverse-engineering, validate the output:

### Validate Accuracy

```
/speckit.validate-reverse-engineering
```

**Checks**:
- Do specs match actual code behavior?
- Are all requirements covered by code?
- Are dependencies correctly identified?
- Do tests validate all requirements?

### Check Coverage

```
/speckit.coverage-check
```

**Reports**:
- % of codebase documented
- Undocumented features (if any)
- Missing integration points
- Gaps in requirement mapping

### Trace Feature to Code

```
/speckit.trace user-authentication
```

**Shows**:
- All files implementing this feature
- Integration points with other features
- Test coverage for feature
- Documentation completeness

---

## Enhancing Reverse-Engineered Specs

Automated reverse-engineering is good but not perfect. Enhance with:

### Add Domain Knowledge

**Automated spec says**:
```markdown
### FR1: User Registration
Creates new user with email and password.
```

**Enhanced with domain knowledge**:
```markdown
### FR1: User Registration
**User Story**: As a new visitor, I want to create an account so I can save my work and access it from any device.

**Business Rule**: Email must be unique across system. Users with duplicate emails are prompted to login instead.

**Integration**: After successful registration, user is automatically logged in and redirected to onboarding flow.

**Rationale**: Reduces friction by avoiding separate login step after registration.
```

### Clarify Implicit Constraints

**Automated spec may miss**:
- Business rules not in code
- Manual processes
- External dependencies
- Assumed knowledge

**Add explicitly**:
```markdown
## Constraints (Enhanced)

**From Code**:
- Password must be 8+ characters with 1 number and 1 special character

**From Business**:
- Users under 13 cannot register (COPPA compliance)
- Email domains on blocklist rejected (spam prevention)

**From Operations**:
- SendGrid monthly email limit: 100,000
- Database has 1M user capacity (upgrade at 800k)
```

### Add Success Metrics

**Code doesn't specify**, but business cares about:
```markdown
## Success Metrics

**Performance**:
- Registration completes in <2 seconds
- Login response <500ms

**Business**:
- Registration completion rate >70%
- Email verification rate >60%
- First-week retention >40%

**Security**:
- Zero password breaches
- <0.1% fraudulent accounts
```

---

## Brownfield-Specific Considerations

### Integration Documentation

Unlike greenfield, brownfield features integrate with existing code:

```markdown
## Integration Points (Critical for Brownfield)

**Consumes**:
- Email service (for verification emails)
- Logging service (audit trail)
- Analytics service (track registrations)

**Consumed By**:
- Task management (requires authenticated user)
- Notification system (user preferences)
- Profile management (user data CRUD)

**Shared State**:
- JWT token (used by all protected endpoints)
- User session (stored in Redis)
```

### Migration Notes

Document how feature evolved:

```markdown
## Migration History

**v1.0 (2020)**: Basic username/password auth
**v2.0 (2021)**: Added OAuth2 (Google, GitHub)
**v2.5 (2022)**: Added 2FA via TOTP
**v3.0 (2023)**: Migrated to Passport.js from custom auth

**Current State**: Mixed auth strategies (legacy password + OAuth + 2FA)
**Future Plan**: Consolidate under single Passport.js strategy
```

---

## Troubleshooting

### Reverse-Engineering Fails

**Too many features discovered**:
- Use `--features` filter to target specific features
- Example: `/speckit.reverse-engineer --features "auth,tasks"`

**Features not detected**:
- Codebase uses non-standard patterns
- Manually create specify.md and mapping.md
- Submit pattern examples to Spec-Kit project

**Specs are inaccurate**:
- Validate with `/speckit.validate-reverse-engineering`
- Manually review and correct
- Add domain knowledge (see "Enhancing" section)

### Coverage Gaps

**Code without tests**:
- Success criteria will be incomplete
- Supplement with manual testing or user stories

**Undocumented business rules**:
- Interview stakeholders
- Review product docs or wiki
- Add to constraints section

**External dependencies unclear**:
- Check environment variables
- Review deployment configs
- Document in plan.md integrations section

---

## After Reverse-Engineering

### Use Specs as Reference for New Features

When adding new features to brownfield codebase:
1. Review reverse-engineered specs for similar features
2. Identify integration points in mapping.md
3. Follow existing patterns (from plan.md)
4. Ensure consistency with constitution

### Keep Specs Updated

As code evolves:
- Re-run `/speckit.reverse-engineer [feature]` to refresh specs
- Update mapping.md if file structure changes
- Add new requirements to specify.md
- Track migration history in plan.md

---

## Next Steps

- **Integration planning**: Load `references/guides/integration-planning.md`
- **Feature management**: Load `references/guides/feature-management-quick.md`
- **Brownfield workflow**: Return to `references/workflows/brownfield-quick-start.md`
