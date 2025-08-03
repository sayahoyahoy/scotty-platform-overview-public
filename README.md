# Scotty

**AI-first development platform where software evolves autonomously**

*Complexity cannot be eliminated, but it can be orchestrated.*

---

## What is Scotty?

Scotty is a unified development platform that fundamentally changes how applications are built and operated. Instead of writing code that gets compiled and deployed, you define components and logic that run instantly online. AI agents can autonomously improve your applications 24/7 through real-time experimentation and evolution.

## Core Philosophy

We spent years building infrastructure where:
- **Everything is instantly live** - Save a change, it's online. No build process.
- **Schema drives everything** - One source of truth for frontend, backend, permissions, and AI
- **AI agents are first-class developers** - They use the same tools as humans
- **Software evolves, not deploys** - Continuous micro-experiments with automatic optimization

## Key Innovations

### 🚀 Instant Everything
Every component, API, and change runs immediately on a URL. Branches, A/B tests, and deployments happen in real-time.

### 🧬 Schema as DNA  
A single schema definition generates database models, API validation, TypeScript types, UI forms, and AI tool definitions.

### 🤖 AI-Native Architecture
AI agents aren't just code generators - they're orchestrators that can create, test, monitor, and evolve applications autonomously.

### 🔒 Enterprise Security by Default
Field-level permissions, zero-trust architecture, and safe 3-way merge that never exposes unauthorized data.

### 🎯 Progressive Complexity
Simple tasks require no configuration. Complex scenarios expose full control. The platform grows with your needs.

## Documentation

### Platform Overview
- [Architecture](./docs/architecture.md) - System design and component interaction
- [Philosophy](./docs/philosophy.md) - Why we built Scotty this way
- [Security](./docs/security.md) - Zero-trust model and data protection

### Core Technologies
- [Frontend Engine](./docs/fe-engine.md) - Browser-native bundling and runtime
- [Backend Engine](./docs/be-engine.md) - Lambda-based orchestration  
- [Schema Language](./docs/schema.md) - Unified definition language
- [Query System](./docs/queries.md) - Visual backend workflows

### Developer Experience
- [Components](./docs/components.md) - UI, state, and worker containers
- [Data Layer](./docs/data.md) - Multi-strategy data synchronization
- [Templates & Styles](./docs/templates-styles.md) - Modern DSL for UI
- [AutoForm](./docs/autoform.md) - Schema-driven form generation

### Advanced Features
- [3-Way Merge](./docs/merge.md) - Safe collaborative editing
- [AI Agents](./docs/agents.md) - Autonomous application improvement
- [Marketplace](./docs/marketplace.md) - Component sharing and reuse
- [Deployment](./docs/deployment.md) - Multi-platform distribution

## Quick Examples

### Component Definition
```pug
// Template with clean syntax
my-button(@click="methods.increment")
  span Count: {{ data.count }}
```

### Schema-Driven Everything
```typescript
type User {
  id    ID
  email Email
  role  Role @permissions("admin")
}

routes {
  getUser(GET "/users/:id") {
    output User
  }
}
```

### AI Agent Integration
```yaml
steps:
  analyzePerformance:
    type: AI
    tools: [analytics.get, components.update]
    
  deployIfBetter:
    type: conditional
    condition: performance.improved
    action: deploy(branch: "optimized")
```

## The Future We're Building

Imagine applications that improve themselves while you sleep. Where AI agents run thousands of experiments, finding the optimal user experience for each segment. Where the boundary between development and operation disappears, replaced by continuous evolution.

This isn't about replacing developers - it's about amplifying human creativity by removing friction and enabling software to adapt at the speed of thought.

---

*Welcome to the future of software development.*