# Greenfield Workflow Examples

Real-world examples of complete greenfield workflows.

## Token Budget

**Tier 1**: 100 tokens (already loaded)
**Tier 2**: 2,000 tokens (already loaded)
**Tier 3 (this guide)**: ~500 tokens

**Current total**: 2,600 tokens
**Remaining budget**: 7,400 tokens ✅

---

## Example 1: Photo Album Organizer (React + TypeScript)

### Complete Workflow

```bash
# Step 1: Initialize
specify init photo-organizer --ai claude

# Step 2: Constitution
```

```
/speckit.constitution Create principles focused on:
- Modern React best practices (hooks, functional components)
- TypeScript strict mode for type safety
- Performance (60fps interactions, <3s initial load)
- Accessibility (WCAG 2.1 AA)
- Testing coverage 80%+
```

Generated constitution emphasizes:
- Component reusability and composition
- Minimal dependencies (prefer platform APIs)
- Progressive Web App capabilities
- Offline-first architecture

```
# Step 3: Specify
```

```
/speckit.specify Build a photo album organizer with these features:
- Import photos from local device
- Auto-group photos by date (EXIF data)
- Manual album creation and editing
- Drag-and-drop photo reorganization
- Grid thumbnail view with lazy loading
- Support up to 10,000 photos per album
- Export albums as zip files
- Offline functionality with local storage
```

Generated specify.md includes:
- 8 user stories covering photographer workflows
- 15 functional requirements with acceptance criteria
- Success metrics (upload <2s, drag latency <100ms)
- Constraints (browser support, storage limits)

```
# Step 4: Plan
```

```
/speckit.plan Technology stack:
- React 18 with TypeScript 5
- Vite for fast development and builds
- Tailwind CSS for styling
- dnd-kit for drag-and-drop
- IndexedDB for local storage
- Vitest + React Testing Library for tests
- Virtualized list (react-window) for performance

Architecture:
- Component-based with presentational/container split
- Zustand for state management
- Custom hooks for photo operations
- Service layer for IndexedDB operations
```

Generated plan.md defines:
- Component hierarchy (App → AlbumList → Album → PhotoGrid → PhotoTile)
- State management strategy (albums, photos, UI state)
- Data model (Album, Photo, Tag entities)
- Implementation phases (4 phases over 3 days)

```
# Step 5: Tasks
```

Generated tasks.md with 28 tasks:

**Scaffolding (Tasks 1-6)**:
1. Initialize Vite + React + TypeScript
2. Install Tailwind, dnd-kit, zustand, react-window
3. Set up folder structure
4. Configure Vitest
5. Create IndexedDB wrapper utilities
6. Set up ESLint + Prettier

**Core UI (Tasks 7-16)**:
7. Build PhotoGrid with virtualization
8. Create PhotoTile component
9. Implement drag-and-drop
10. Build Album component
11. Create AlbumList navigation
12. Add photo upload functionality
... (16 total UI tasks)

**Features (Tasks 17-24)**:
17. EXIF data extraction
18. Auto-grouping by date
19. Search functionality
20. Zip export feature
21. Offline sync logic
... (8 total feature tasks)

**Testing & Polish (Tasks 25-28)**:
25. Unit tests for components
26. Integration tests for workflows
27. Performance optimization
28. Accessibility audit

```
# Step 6: Implement
```

```
/speckit.implement
```

Result: Working photo organizer app with all features implemented.

---

## Example 2: Task Management API (Node.js + Express)

### Complete Workflow

```bash
specify init task-api --ai claude
```

**Constitution**:
```
/speckit.constitution API design principles:
- RESTful resource-based endpoints
- OpenAPI 3.1 documentation
- JWT authentication + role-based access
- PostgreSQL for data persistence
- Redis for caching and sessions
- 99.9% uptime SLA
- <100ms average response time
- Comprehensive error handling
```

**Specification**:
```
/speckit.specify Build a task management API with:
- User authentication (register, login, JWT refresh)
- Task CRUD (create, read, update, delete)
- Task assignment to users
- Task status workflow (todo → in_progress → done)
- Due date reminders
- Task filtering and pagination
- Rate limiting (100 req/min per user)
- API versioning (v1)
```

**Plan**:
```
/speckit.plan Stack:
- Node.js 20+ with TypeScript
- Express 4.x for routing
- Prisma ORM for PostgreSQL
- ioredis for Redis
- Passport.js for auth
- express-rate-limit for rate limiting
- Winston for logging
- Jest for testing

Architecture:
- Layered architecture (routes → controllers → services → repositories)
- Middleware chain (auth → validation → rate-limit → routes)
- Database migrations with Prisma
- Environment-based configuration
```

**Tasks** (32 tasks):
1. Initialize Node.js + TypeScript project
2. Set up Express server with basic middleware
3. Configure Prisma + PostgreSQL
4. Create database schema (users, tasks tables)
5. Implement JWT authentication
6. Build user registration endpoint
7. Build user login endpoint
8. Create task CRUD endpoints
9. Add task assignment logic
10. Implement status workflow validation
... (32 total)

**Implement**:
```
/speckit.implement
```

Result: Production-ready task API with documentation.

---

## Example 3: E-commerce Product Catalog (Vue.js)

### Abbreviated Workflow

**Constitution**: Focus on SEO, performance, mobile-first design

**Specification**:
- Product listing with filtering (price, category, rating)
- Product detail pages with image gallery
- Shopping cart (add, remove, update quantities)
- Checkout flow (guest + registered users)
- Order history for registered users

**Plan**:
- Vue 3 with Composition API + TypeScript
- Nuxt 3 for SSR/SEO
- Pinia for state management
- Tailwind for responsive design
- Stripe for payments
- MongoDB for product catalog

**Key Tasks**:
- SSR setup with Nuxt
- Product listing with server-side filters
- Image optimization and lazy loading
- Shopping cart state management
- Stripe payment integration
- Order confirmation emails

**Result**: SEO-optimized e-commerce site

---

## Example 4: Real-Time Chat Application (WebSockets)

### Abbreviated Workflow

**Constitution**: Real-time performance, scalability, security

**Specification**:
- User authentication and profiles
- One-on-one messaging
- Group chat rooms
- Typing indicators
- Read receipts
- Message history and search
- File sharing (images, documents)

**Plan**:
- React + TypeScript frontend
- Node.js + Socket.io backend
- PostgreSQL for message persistence
- Redis for pub/sub and presence
- MinIO for file storage
- JWT + refresh tokens for auth

**Key Tasks**:
- WebSocket connection management
- Real-time message delivery
- Typing indicator implementation
- Message read status tracking
- File upload and streaming
- Reconnection and offline handling

**Result**: Production-grade chat app

---

## Example 5: Mobile Fitness Tracker (React Native)

### Abbreviated Workflow

**Constitution**: Cross-platform (iOS + Android), offline-first, battery efficient

**Specification**:
- Activity tracking (steps, distance, calories)
- Workout logging (runs, gym sessions)
- Progress charts and analytics
- Goal setting and notifications
- Social features (share workouts, challenges)
- Integration with health APIs (Apple Health, Google Fit)

**Plan**:
- React Native + TypeScript
- Expo for build tooling
- SQLite for local data
- AsyncStorage for settings
- React Navigation for routing
- Victory Native for charts
- expo-notifications for reminders

**Key Tasks**:
- Pedometer integration
- Workout tracking UI
- Chart components with Victory
- Health API integration
- Background location tracking
- Push notifications
- Data sync to cloud

**Result**: Cross-platform fitness app

---

## Common Patterns Across Examples

### Constitution Themes
- Testing requirements (80%+ coverage common)
- Performance targets (load time, response time, fps)
- Technology constraints (versions, platforms)
- Quality standards (accessibility, security, documentation)

### Specification Patterns
- User stories in "As a [role], I want [goal], so that [benefit]" format
- Functional requirements with measurable acceptance criteria
- Non-functional requirements (performance, security, scalability)
- Constraints and assumptions explicitly stated

### Planning Patterns
- Clear technology stack with rationale
- Layered or component-based architecture
- Implementation phases (scaffolding → core → polish)
- Risk assessment and mitigation strategies

### Task Breakdown Patterns
- 20-40 tasks typical for medium features
- Grouped by category (scaffolding, UI, features, testing)
- Dependencies explicitly noted
- Complexity estimates (simple, medium, complex)

---

## Lessons Learned

### What Works Well
1. **Detailed specifications** lead to clearer plans and implementations
2. **Technology constraints in constitution** prevent plan conflicts
3. **Phase-based task organization** leads to logical implementation order
4. **Explicit success criteria** enable validation and testing

### Common Pitfalls
1. **Vague specifications** → AI guesses, may not match intent
2. **Over-constrained constitution** → Limits flexibility in planning
3. **Too many tasks** → Overwhelming, hard to track progress
4. **Skipping optional commands** → Miss opportunities for clarification and validation

---

## Next Steps

- **Try a greenfield workflow** yourself with a small feature
- **Compare your results** to these examples
- **Iterate on prompts** to get better specifications and plans
- **Load feature management guide** if working with multiple features

→ Feature management: `references/guides/feature-management-quick.md`
