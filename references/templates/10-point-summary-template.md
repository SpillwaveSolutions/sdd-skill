# 10-Point Summary Template

Use this template after ANY SDD command completes to summarize generated artifacts and keep users engaged.

## Template Structure

```markdown
## [Artifact Name] Summary

### 🎯 What Was Created
[1-2 sentences describing the artifact that was generated]

### 🔑 Key Decisions
1. **[Decision Category]**: [Brief decision made]
2. **[Decision Category]**: [Brief decision made]
3. **[Decision Category]**: [Brief decision made]

### 📋 Main Sections
- **[Section Name]**: [1-line summary of section content]
- **[Section Name]**: [1-line summary of section content]
- **[Section Name]**: [1-line summary of section content]

### ⚡ Highlights
- [Most important point from artifact]
- [Second most important point]
- [Third most important point]

### 🔄 Next Step
[Clear statement of what happens next in the workflow]

### 💬 Your Feedback
Would you like to:
- **[A] Proceed** - Continue to next step
- **[B] Modify** - Adjust something in this artifact
- **[C] Regenerate** - Start this step over with different input
- **[D] Explain** - Get more details about a specific section
```

---

## Example: Constitution Summary

```markdown
## Constitution Summary

### 🎯 What Was Created
Generated .speckit/constitution.md defining your project's core principles, coding standards, and quality expectations.

### 🔑 Key Decisions
1. **Testing Strategy**: All features require unit tests with 80%+ coverage
2. **Code Style**: TypeScript strict mode, ESLint + Prettier enforcement
3. **Architecture**: Component-based with clear separation of concerns

### 📋 Main Sections
- **Core Principles**: Simplicity, testability, maintainability prioritized
- **Technology Constraints**: React 18+, TypeScript 5+, Vite build tool
- **Quality Standards**: Automated testing, code review, continuous integration

### ⚡ Highlights
- Every feature must be testable in isolation
- Dependencies kept minimal (review any new dependency)
- Performance: Target <100ms initial load, <16ms frame time

### 🔄 Next Step
Run `/speckit.specify` to define your first feature requirements.

### 💬 Your Feedback
Would you like to:
- **[A] Proceed** - Move to feature specification
- **[B] Modify** - Adjust principles or standards
- **[C] Regenerate** - Rewrite constitution with different focus
- **[D] Explain** - Get details about any section
```

---

## Example: Specification Summary

```markdown
## Feature Specification Summary

### 🎯 What Was Created
Generated .speckit/features/001-photo-albums/specify.md with functional requirements for photo organization feature.

### 🔑 Key Decisions
1. **Core Functionality**: Album creation, photo upload, drag-and-drop reorganization
2. **User Experience**: Tile-based preview, date-based grouping, responsive layout
3. **Data Model**: Albums, Photos, Tags (many-to-many relationships)

### 📋 Main Sections
- **User Stories**: 5 stories covering album creation, photo management, organization
- **Functional Requirements**: 12 requirements for core feature behavior
- **Success Criteria**: Measurable goals (upload <2s, drag latency <100ms)
- **Constraints**: Browser compatibility, storage limits, image formats

### ⚡ Highlights
- Support up to 10,000 photos per album
- Lazy loading for performance with large albums
- Offline mode with local-first architecture

### 🔄 Next Step
Run `/speckit.plan` to create technical implementation plan.

### 💬 Your Feedback
Would you like to:
- **[A] Proceed** - Move to technical planning
- **[B] Modify** - Adjust requirements or user stories
- **[C] Regenerate** - Rewrite spec with different focus
- **[D] Explain** - Get details about specific requirements
```

---

## Example: Plan Summary

```markdown
## Technical Plan Summary

### 🎯 What Was Created
Generated .speckit/features/001-photo-albums/plan.md with technical architecture and implementation strategy.

### 🔑 Key Decisions
1. **Tech Stack**: React + TypeScript + Vite + Tailwind CSS
2. **State Management**: Zustand for client state, IndexedDB for persistence
3. **File Handling**: FileReader API + Canvas API for image processing

### 📋 Main Sections
- **Architecture**: Component hierarchy, data flow, state management
- **Key Technologies**: Full stack with rationale for each choice
- **Dependencies**: 8 npm packages (react, zustand, dnd-kit, etc.)
- **Implementation Phases**: 4 phases (scaffolding, core UI, drag-drop, optimization)

### ⚡ Highlights
- Local-first: All data in IndexedDB, no backend required
- Performance: Virtual scrolling for 10k+ photos
- Accessibility: Full keyboard navigation, ARIA labels

### 🔄 Next Step
Run `/speckit.tasks` to break down implementation into actionable tasks.

### 💬 Your Feedback
Would you like to:
- **[A] Proceed** - Move to task breakdown
- **[B] Modify** - Adjust tech choices or architecture
- **[C] Regenerate** - Redesign with different stack
- **[D] Explain** - Get details about specific technologies
```

---

## Example: Tasks Summary

```markdown
## Task Breakdown Summary

### 🎯 What Was Created
Generated .speckit/features/001-photo-albums/tasks.md with 24 actionable tasks organized into 4 categories.

### 🔑 Key Decisions
1. **Task Sequencing**: Scaffolding → UI → Drag-Drop → Polish
2. **Complexity Estimates**: 8 simple, 12 medium, 4 complex tasks
3. **Testing Strategy**: Unit tests + integration tests for each category

### 📋 Main Sections
- **Scaffolding** (Tasks 1-6): Project setup, dependencies, folder structure
- **Core UI** (Tasks 7-14): Components for albums, photos, previews
- **Drag & Drop** (Tasks 15-19): dnd-kit integration, reordering logic
- **Polish & Testing** (Tasks 20-24): Performance, accessibility, tests

### ⚡ Highlights
- Task 1: Initialize Vite + React + TypeScript project
- Task 10: Build photo tile component with lazy loading
- Task 15: Implement drag-and-drop with dnd-kit
- Task 24: End-to-end testing with 10k photos

### 🔄 Next Step
Run `/speckit.implement` to execute all tasks and build the feature.

### 💬 Your Feedback
Would you like to:
- **[A] Proceed** - Start implementation
- **[B] Modify** - Adjust task breakdown or sequencing
- **[C] Regenerate** - Reorganize tasks differently
- **[D] Explain** - Get details about specific tasks
```

---

## Usage Notes

### When to Use This Template
- **After `/speckit.constitution`** - Summarize constitution.md
- **After `/speckit.specify`** - Summarize specify.md
- **After `/speckit.plan`** - Summarize plan.md
- **After `/speckit.tasks`** - Summarize tasks.md
- **After brownfield commands** - Summarize analysis, integration plan, etc.

### Customization
- Adjust the 🔑 Key Decisions count (2-5 decisions typical)
- Expand/contract 📋 Main Sections based on artifact complexity
- Always include ⚡ Highlights (3 most important points)
- Always provide 💬 Your Feedback options (A/B/C/D)

### Benefits
- **Keeps users engaged** - No "black box" AI behavior
- **Enables early feedback** - Catch issues before implementation
- **Maintains agility** - Quick review without deep dive
- **Builds trust** - Transparent reasoning and decision-making
