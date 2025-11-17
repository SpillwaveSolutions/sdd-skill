# Codebase Analysis Guide

How to analyze existing codebases before applying Spec-Driven Development.

## Token Budget

**Tier 1**: 100 tokens (already loaded)
**Tier 2**: 2,000 tokens (already loaded)
**Tier 3 (this guide)**: ~1,250 tokens

**Current total**: 3,350 tokens
**Remaining budget**: 6,650 tokens ✅

---

## Analysis Depth Options

Choose analysis depth based on project size and goals:

### Surface Analysis (~5 minutes)

**What it covers**:
- File structure and organization
- Technology stack identification
- Basic pattern recognition (MVC, layered, etc.)
- Dependency overview

**Best for**:
- Quick overview needed
- Small codebases (<5,000 lines)
- Familiar tech stack
- Simple feature additions

**Command**:
```
/speckit.brownfield --depth surface
```

**Output example**:
```markdown
## Surface Analysis Report

### Project Structure
- Backend: src/server/ (Node.js + Express)
- Frontend: src/client/ (React + TypeScript)
- Tests: tests/ (Jest)

### Tech Stack
- Runtime: Node.js 18
- Framework: Express 4.x
- Database: PostgreSQL via Prisma
- Frontend: React 18, Vite

### Patterns Detected
- Layered architecture (routes → controllers → services)
- RESTful API design
- JWT authentication
```

---

### Moderate Analysis (~15 minutes)

**What it covers**:
- Everything in Surface Analysis, plus:
- Architecture patterns in detail
- Coding standards extraction
- Dependency mapping and versions
- Technical debt identification
- Performance baseline
- Security practices

**Best for**:
- Standard brownfield adoption
- Medium codebases (5,000-50,000 lines)
- Complex feature additions
- Modernization projects

**Command**:
```
/speckit.brownfield --depth moderate
```

**Output example**:
```markdown
## Moderate Analysis Report

[... Surface analysis content ...]

### Architecture Details
- **Routes Layer**: Express routers with route-level middleware
- **Controller Layer**: Request/response handling, input validation
- **Service Layer**: Business logic, orchestrates repositories
- **Repository Layer**: Data access via Prisma ORM
- **Middleware**: Auth, logging, error handling, rate limiting

### Coding Standards
- **TypeScript**: Strict mode enabled, no implicit any
- **Testing**: Jest + Supertest, ~70% coverage
- **Linting**: ESLint (Airbnb config), Prettier
- **Documentation**: JSDoc for public APIs

### Dependencies (32 total)
**Production**:
- express@4.18.2
- prisma@5.2.0
- jsonwebtoken@9.0.1
- bcrypt@5.1.0
[... more dependencies ...]

**Development**:
- typescript@5.1.6
- jest@29.6.2
- eslint@8.46.0
[... more dependencies ...]

### Technical Debt
1. **High Priority**:
   - Missing error handling in authentication middleware
   - No retry logic for database operations
   - Hardcoded configuration values

2. **Medium Priority**:
   - Inconsistent error response formats
   - Some controllers are too large (>200 lines)
   - Limited test coverage in service layer

3. **Low Priority**:
   - Outdated dependencies (5 minor version updates available)
   - Missing API documentation (no OpenAPI spec)

### Performance Baseline
- Average response time: 120ms
- Database query time: 40ms average
- Memory usage: 250MB steady state
- No caching layer detected
```

---

### Deep Analysis (~30+ minutes)

**What it covers**:
- Everything in Moderate Analysis, plus:
- Comprehensive feature inventory
- Complete reverse-engineering
- Integration point mapping
- Data flow analysis
- Security audit
- Compliance check
- Migration path recommendations

**Best for**:
- Large migration projects
- Enterprise adoption
- Complex legacy systems
- Comprehensive documentation needed

**Command**:
```
/speckit.brownfield --depth deep
```

**Output example**:
```markdown
## Deep Analysis Report

[... Moderate analysis content ...]

### Feature Inventory (12 features discovered)

**Authentication Module**:
- User registration
- Login/logout
- JWT token management
- Password reset flow

**User Management**:
- User profile CRUD
- Role-based access control
- User search and filtering

**Task Management**:
- Task CRUD
- Task assignment
- Status workflow
- Due date reminders
- Task search/filter

**Notification System**:
- Email notifications
- In-app notifications
- Notification preferences

### Integration Point Mapping

**External Services**:
- SendGrid (email delivery)
- AWS S3 (file storage)
- Stripe (payments) - partially integrated

**Internal Dependencies**:
```
User Module
  ↓
  ├─→ Auth Module (dependency)
  ├─→ Notification Module (uses)
  └─→ Task Module (references)

Task Module
  ↓
  ├─→ User Module (references)
  └─→ Notification Module (uses)
```

### Data Flow Analysis

**User Registration Flow**:
1. POST /api/users/register
2. Controller validates input
3. Service checks for existing user
4. Service hashes password (bcrypt)
5. Repository creates user in DB
6. Service triggers welcome email (SendGrid)
7. Controller returns JWT token

**Critical Flows**:
- Authentication: 15 requests/second peak
- Task creation: 8 requests/second average
- File upload: 2 requests/second average

### Security Audit

**Strengths**:
- JWT authentication with refresh tokens
- Password hashing with bcrypt (salt rounds: 10)
- SQL injection prevention (Prisma ORM)
- HTTPS enforced
- Rate limiting on auth endpoints

**Vulnerabilities**:
- ⚠️ **High**: Missing CSRF protection
- ⚠️ **High**: JWT tokens never expire (no max lifetime)
- ⚠️ **Medium**: No input sanitization for file uploads
- ⚠️ **Medium**: Sensitive data in logs (tokens, passwords)
- ⚠️ **Low**: Missing security headers (HSTS, CSP)

### Compliance Check

**GDPR**:
- ✅ User data deletion endpoint exists
- ✅ Data export functionality
- ❌ Missing consent tracking
- ❌ No data retention policy

**Accessibility (WCAG 2.1)**:
- ⚠️ Limited analysis (backend-only project)
- Recommend frontend audit

### Migration Path Recommendations

**Short Term (1-2 weeks)**:
1. Fix high-priority security vulnerabilities
2. Add CSRF protection
3. Implement JWT expiration
4. Update critical dependencies

**Medium Term (1-2 months)**:
1. Improve test coverage to 85%+
2. Extract configuration to environment variables
3. Add OpenAPI documentation
4. Implement caching layer (Redis)

**Long Term (3-6 months)**:
1. Migrate to microservices architecture (if scaling needed)
2. Add event-driven architecture for notifications
3. Implement comprehensive audit logging
4. GDPR compliance enhancements
```

---

## Choosing the Right Depth

### Decision Matrix

| Codebase Size | Feature Complexity | Goal | Recommended Depth |
|--------------|-------------------|------|------------------|
| <5k lines | Simple addition | Add feature | Surface |
| <5k lines | Major refactor | Modernize | Moderate |
| 5k-50k lines | Simple addition | Add feature | Moderate |
| 5k-50k lines | Major refactor | Modernize | Deep |
| 50k+ lines | Any change | Any goal | Deep |
| Legacy system | Unknown | Document | Deep |

### Time vs. Value Tradeoff

**Surface** (5 min):
- Value: Basic understanding, quick start
- Limitation: May miss technical debt, integration complexity

**Moderate** (15 min):
- Value: Comprehensive overview, identifies risks
- Limitation: May not discover all integration points

**Deep** (30+ min):
- Value: Complete picture, migration planning
- Limitation: Time-consuming, may be overkill for simple features

---

## Analysis Report Sections

### Every Report Includes

1. **Project Structure**: Directory layout, organization
2. **Tech Stack**: Languages, frameworks, tools
3. **Architecture Patterns**: High-level design patterns
4. **Next Steps**: Recommended actions based on findings

### Moderate Reports Add

5. **Coding Standards**: Style guides, conventions
6. **Dependencies**: Full dependency tree with versions
7. **Technical Debt**: Prioritized list of issues
8. **Performance Baseline**: Current metrics

### Deep Reports Add

9. **Feature Inventory**: Complete list of existing features
10. **Integration Mapping**: Internal and external dependencies
11. **Data Flow**: Critical business flows
12. **Security Audit**: Vulnerabilities and recommendations
13. **Compliance**: Regulatory requirements (GDPR, HIPAA, etc.)
14. **Migration Path**: Phased modernization plan

---

## After Analysis

### Use Report to Generate Constitution

```
/speckit.analyze-codebase --from-analysis report.md
```

This creates `.speckit/constitution.md` that:
- Acknowledges existing patterns and standards
- Identifies improvement opportunities
- Sets direction for new features

### Use Report to Plan Integration

When specifying new features:
- Reference integration points from analysis
- Account for discovered technical debt
- Align with existing architecture patterns
- Plan for identified security vulnerabilities

---

## Troubleshooting

### Analysis Fails

**Codebase too large (>100k lines)**:
- Use `--scope` to analyze specific directories
- Example: `/speckit.brownfield --scope src/api --depth moderate`

**Permissions errors**:
- Ensure read access to all files
- Check if any files are locked or encrypted

**Unclear architecture**:
- Start with surface analysis
- Manually explore key files
- Re-run with moderate depth after understanding

### Analysis Incomplete

**Missing features**:
- Deep analysis may still miss undocumented features
- Supplement with interviews, user stories, or manual exploration

**Wrong technology identified**:
- Verify analysis output against known facts
- Correct in constitution.md if needed

**Outdated dependencies not flagged**:
- Run `npm outdated` or equivalent separately
- Add findings to technical debt list manually

---

## Integration with Greenfield Workflow

After brownfield analysis and constitution generation, the workflow converges with greenfield:

```
[Brownfield Analysis] → [Constitution from Code] →
[Specify New Feature] → [Plan] → [Tasks] → [Implement]
                ↑
                └─── Same workflow as greenfield from here
```

Key difference: Constitution acknowledges existing patterns, new features integrate with existing code.

---

## Next Steps

- After analysis, load: `references/workflows/brownfield-quick-start.md`
- For integration planning, load: `references/guides/integration-planning.md`
- For reverse engineering features, load: `references/guides/reverse-engineering.md`
