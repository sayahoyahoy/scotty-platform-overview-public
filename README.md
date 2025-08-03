# Scotty Platform - Comprehensive Overview

**AI-first development platform where software evolves autonomously**

> ⚙️ ***Complexity cannot be eliminated, but it can be orchestrated.***

> "We don't aim for the world that existed so far, but for the one that is just beginning – a world where creativity and the ability to define a problem outweighs the ability to implement it."

- 🧑‍💻 From developers to creators: AI enables anyone with an idea to build applications
- 🚀 AI-first, not no-code: A platform where AI isn't an add-on, but the foundation
- 🧩 Components, not widgets: Everything is reusable, remixable, shareable
- 🛠️ Orchestration, not wiring: Define WHAT, not HOW
- 🤖 AI agent = team colleague, not black box
- 🏪 Marketplace for everything: UI, logic, AI, workflows, instructions
- 🔒 Enterprise security by default

## Core Philosophy
We spent years building infrastructure where:

- Everything is instantly live - Save a change, it's online. No build process.
- Schema drives everything - One source of truth for frontend, backend, permissions, and AI
- AI agents are first-class developers - They use the same tools as humans
- Software evolves, not deploys - Continuous micro-experiments with automatic optimization

## The Future We're Building
Imagine applications that improve themselves while you sleep. Where AI agents run thousands of experiments, finding the optimal user experience for each segment. Where the boundary between development and operation disappears, replaced by continuous evolution.

This isn't about replacing developers - it's about amplifying human creativity by removing friction and enabling software to adapt at the speed of thought.

Welcome to the future of software development.

## Key Innovations

🚀 **Instant Everything**  
Every component, API, and change runs immediately on a URL. Branches, A/B tests, and deployments happen in real-time.

🧬 **Schema as DNA**  
A single schema definition generates database models, API validation, TypeScript types, UI forms, and AI tool definitions.

🤖 **AI-Native Architecture**  
AI agents aren't just code generators - they're orchestrators that can create, test, monitor, and evolve applications autonomously.

🔒 **Enterprise Security by Default**  
Field-level permissions, zero-trust architecture, and safe 3-way merge that never exposes unauthorized data.

🎯 **Progressive Complexity**  
Simple tasks require no configuration. Complex scenarios expose full control. The platform grows with your needs.

---

## 🚀 What is Scotty?

Scotty is a platform designed to change how people build applications. Instead of you or AI spending time setting up tools and writing code that someone has written thousands of times before, you simply define what you want, and it works. Immediately. Online.

This isn't another "no-code" tool for drag&drop amateurs. Nor a complex framework for senior engineers. Scotty is built for the new generation of **Creators** - people who know nothing about programming and let AI do the programming for them.

### 🚀 Quick Jumps

**Main sections:**
- [Technical Solution](#️-what-we-had-to-build-and-why) - Frontend + Backend meta framework
- [AI Architecture](#-why-ai-first-architecture) - Why AI works differently than elsewhere  
- [Practical Workflow](#-how-it-works-in-practice) - Concrete use cases
- [Platform Features](#scotty-platform-features) - Complete feature overview

**Technical details:**
- [Template Language](#1-template-language) - Declarative syntax for creators
- [Styling System](#2-styling-system) - CSS + Tailwind harmony
- [Schema Language](#3-schema-language) - Single source of truth
- [3-way Merge](#4-intelligent-merge) - Safe merging according to schema
- [AutoForm](#5-autoform) - Forms without logic duplication
- [AI Integration](#6-ai-as-flow-step) - AI as native part of applications
- [Marketplace](#7-marketplace) - Living memory of the platform
- [Unified Data](#8-unified-data) - One hook for all data strategies

---

## 🛠️ What we had to build (and why)

## Frontend

### Meta framework for the Creator era

We couldn't build Scotty on React, Vue, or any other existing framework. **All these tools are designed only for programmers.** Even though AI can generate React code, the result is still a pile of hooks, useEffect, useState, context providers, and other noise that regular people don't understand.

We needed a **meta framework** - something that works above current technologies but hides their complexity. We took proven syntaxes and approaches, trimmed everything unnecessary, and modernized it for people who don't want to be programmers, while maintaining a programmer-like approach.

**Our approach:**
- **Inside = Vue 3** (but that's just an implementation detail users don't see)
- **Interface = Simple templates + JavaScript + styles** (like jQuery era, but modernized)
- **No hooks, reactivity, lifecycle** - just `data.something = newValue` and it works
- **Replaceable core** - we can completely rewrite, user code remains

It's like a **return to simplicity**, but with the power of modern tools under the hood.

## Backend

### Orchestration instead of architecture

**Problem:** Traditional backend means dozens of decisions - which framework, database, ORM, authentication, validation, deployment, scaling. And then connecting everything together. Most time is spent "wiring" - connecting things that don't even relate to each other.

**Our solution:** We created an orchestration layer where you define **what** you want, not **how** it should run. Every parameter in this flow is JavaScript code that actually executes. Code runs isolated in lambda functions directly from the database. No build process, no deploy, no servers.

```yaml
steps:
  validateInput:
    type: validate
    schema: CreateUser
    
  checkExists:
    type: query
    operation: users.findByEmail
    
  createUser:
    type: database
    operation: insert
    model: User
```

**Why it's cool:**
- **No wiring** - security, validation, database is already connected
- **Instant deployment** - save → runs in production in seconds
- **Visual flows** - backend logic like Make.com, but with code
- **Real JavaScript** - no expressions or formulas, but actual code everywhere
- **Schema-driven** - single source of truth for entire stack
- **Lambda isolation** - every run is safe and scalable

---

## To achieve this, we had to solve fundamental problems:

### 🔗 Jump to:
- [Template Language](#1-template-language) - Declarative syntax for creators
- [Styling System](#2-styling-system) - CSS + Tailwind harmony
- [Schema Language](#3-schema-language) - Single source of truth
- [3-way Merge](#4-intelligent-merge) - Safe merging according to schema
- [AutoForm](#5-autoform) - Forms without logic duplication
- [AI Integration](#6-ai-as-flow-step) - AI as native part of applications
- [Marketplace](#7-marketplace) - Living memory of platform with upstream connectivity
- [Unified Data](#8-unified-data) - One hook for all data strategies


### 1. Template Language
because we needed declarative syntax

**Problem:** We chose Vue because it solves many things well for us. But we needed templates that would be truly declarative and simple. Pug is used with Vue, but it's an old Node.js tool that isn't optimized for Vue specifics.

**Our solution:** We took the proven Pug syntax and enhanced it directly for Vue - added slots, variants, pattern matching, and other things Pug can't do.
```pug
my-dialog.dialog[variant="compact"]
    +header({close})
        my-button(@click="close") ×
    +body
        match message
            with {type: 'success'}
                p Great!
            else  
                p Something went wrong
```

**Why it's cool:**
- **No HTML noise** - just structure and logic
- **AI friendly** - agent immediately understands what's happening  
- **Slot-first** - completely eliminates prop drilling
- **Pattern matching** - functional approach instead of if/else branching
- **Separated styles** - `[variant="compact"]` automatically reflects into CSS, without prop drilling

→ **[Complete syntax reference](./raw/template.md)** - all template language possibilities  
→ **[Template AI Editor](./raw/template-ai-editor.md)** - how AI edits templates with atomic changes

### 2. Styling System
because CSS vs Tailwind is a false choice

**Problem:** Either you write CSS (verbose, hard to maintain) or Tailwind in templates (messy, non-overridable).

**Our solution:**
We combined CSS and Tailwind into one language. Added the ability to override styles deep into components.

```stylus
.root
  &:variant(red)
    --main-color red
  
.header  
  color var(--main-color)
  bg-blue-100 hover:bg-blue-800 hover:text-white
  px-4 py-2

.dialog::footer::okButton
  font-bold hover:text-blue-400
```

**Why it's cool:**
- **Best of both worlds** - clean syntax + Tailwind utilities
- **Deep override** - style components from inside without prop drilling
- **Auto-grouping** - Tailwind organizes itself into logical blocks
- **Component variables** - CSS variables scoped to component

→ **[Styles documentation](./raw/styles.md)** - deep overrides and CSS+Tailwind combination

### 3. Schema Language
because duplication is evil

**Problem:** You define the same data in database, API validation, frontend types, forms. One source, four places where it can break.

**Our solution:** We took the proven Prisma syntax and extended it with everything you need for the entire stack - API routes, frontend data strategies, permissions, validation.
```typescript
type User {
  id        ID
  email     Email  
  role      Role    @permissions("admin")
  createdAt DateTime @default.now
}

routes {
  getUser(GET "/users/:id") {
    output User
  }
}

data users {
  getAll(CACHE pageable) {
    output User[]
  }
}
```

**Why it's cool:**
- **Single source of truth** - define once, works everywhere
- **Auto-generation** - database, API, types, forms create themselves
- **Granular permissions** - permissions down to individual field level
- **AI understands context** - agent knows exactly what it can do with what

→ **[Schema language reference](./raw/schema.md)** - complete DSL syntax and possibilities  
→ **[Schema AI Editor](./raw/schema-ai-editor.md)** - programmatic API for AI schema edits

### 4. Intelligent Merge
because classic Git merge can't do enterprise

**Problem:** Traditional line-by-line merge can reveal secret data in conflicts. When you have field-level permissions and user edits only part of document, Git merge can show fields they don't have access to.

**Our solution:** We created a 3-way merge algorithm that merges according to data schema, not lines. It knows what's a field, what's an object, what are the permissions.

```typescript
// User sees only their fields
const userView = {
  name: "John",
  email: "john@example.com"
  // no access to salary, role
}

// Merge knows about entire structure, but reveals only what's allowed
merge(mine, theirs, base, schema, permissions)
```

**Why it's cool:**
- **Enterprise security** - never reveals unauthorized data
- **Marketplace updates** - safely merge components you've customized
- **Smart conflict resolution** - understands data types, not just text
- **Field-level permissions** - permissions down to individual fields
- **Safe collaboration** - teams can edit simultaneously without data leaks

→ **[3-way diff algorithm](./raw/diff.md)** - technical details of safe merge

### 5. AutoForm
because forms shouldn't duplicate logic

**Problem:** Traditional form libraries force you to define data structure twice - once in database/API, second time in form. Then manually write validations, mapping, error handling. And when you change data model, you must update the form too.

**Our solution:** AutoForm generates forms directly from schema. You just define how individual fields should look, we handle the rest.

```pug
// Schema already exists, form creates automatically
AutoForm(model="userData" path="$.profile")
  +name({value, update})
    input(type="text" :value="value" @input="update")
  
  +email({value, update})
    custom-email-field(:value="value" @change="update")
  
  +address
    // Nested object renders automatically
    AutoFormYield
```

**Why it's cool:**
- **Schema-driven** - structure, validation and permissions already exist
- **No duplication** - don't need to write validations again
- **Unlimited UI** - not just classic form, can be card, list, anything
- **Complex structures** - object arrays, nested structures work automatically
- **Multiple instances** - one model, multiple forms in different places
- **Dev mode** - when you don't define UI, debug form shows automatically

→ **[AutoForm complete documentation](./raw/forms.md)** - advanced forms and reusable patterns

---

## 🤖 Why AI-first Architecture

Current AI tools generate code as black boxes. You write a prompt, get 5000 lines of code you don't understand and can't maintain.

**Scotty is different:**
- **Atomic changes** - AI doesn't do "rewrite entire file", but "add style", "change parameter"
- **Structured understanding** - agent understands every component, knows what it does and why
- **Same tools as humans** - AI uses same APIs as developers
- **Full audit trail** - every change is logged and revertible

**Example AI workflow:**
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

AI agent can autonomously optimize your application while you sleep. But unlike current tools, you know exactly what it did and why.

### 6. AI as Flow Step
because AI should be part of application, not external tool

**Problem:** Current AI tools are separate from your applications. You must export data, call APIs, import results. AI doesn't understand context of your application and has no access to your data or functions.

**Our solution:** AI is a regular `step` in your flows. It has access to all your data, can call your functions, understands schema. Tools for AI are simply your Scotty queries.

```yaml
steps:
  getUserData:
    type: query
    operation: users.getById
    
  analyzeContent:
    type: AI
    model: gpt-4
    tools: [content.analyze, sentiment.get, users.updatePreference]
    prompt: "Analyze content for user {{getUserData.name}}"
    
  updateRecommendations:
    type: query 
    operation: recommendations.update
    input: "{{analyzeContent.suggestions}}"
```

**Why it's cool:**
- **Native integration** - AI is part of your application, not external service
- **Tool calling** - AI can call your own functions with permissions
- **Context aware** - AI knows about your data, schema, users
- **Atomic operations** - AI doesn't do "rewrite file", but "change parameter"
- **Memory & audit** - every AI action is logged and revertible
- **Custom agents** - you can make AI agents for your applications and for Scotty itself

### 7. Marketplace
because shadcn is good idea, but not enough

**Problem:** shadcn showed the right direction - copying components into project instead of dependencies. But has limitations: only UI components, no upstream updates, you can't change styling without touching logic, no monetization.

**Our solution:** Marketplace for everything - components, queries, flows, AI agents, even instructions for agents. With upstream connectivity, deep styling overrides and cross-app synchronization.

```pug
// You import Netflix login component
netflix-login.myLogin
  
// You can remix it without touching logic
.myLogin
  --brand-color blue
  &::submitButton
    bg-gradient-to-r from-blue-500 to-purple-600
```

```typescript
// You import AI workflow from marketplace
import aiContentGenerator from '@marketplace/content-ai-v2'

// Use in your own application with your own data
steps:
  generateContent:
    type: marketplace
    component: aiContentGenerator
    tools: [myBrand.getVoice, myProducts.getInfo]
```

**Why it's cool:**
- **Everything is shareable** - UI, logic, AI agents, workflows, instructions
- **Upstream connectivity** - you get updates, but only those you want
- **Deep remixing** - change styling without touching logic thanks to separated styles
- **Cross-app sync** - edit component in one app, changes everywhere you have it
- **Monetization ready** - publish and earn from your components
- **Private marketplace** - company components stay internal
- **Living memory** - marketplace is long-term memory and skills of entire platform

### 8. Unified Data
because React hooks vs fetch vs local state is chaos

**Problem:** In the frontend world you have dozens of ways to work with data - fetch, React Query, Zustand, Redux, localStorage, sessionStorage, IndexedDB. Each approach has different APIs, different rules, different behavior. Developer must decide: where to store data, how to synchronize it, when to revalidate.

**Our solution:** One `useData()` hook solves everything. Based on schema definition it automatically knows which strategy to use, how to cache data, when to synchronize with backend.

```typescript
// One hook handles everything - cache, validation, types, revalidation
const users = useData('users.getAll')
const userDraft = useData('users.detail', { 
  id: '123', 
  fork: 'editUser' // draft mode automatically
})

// Schema defines behavior:
data users {
  getAll(SYNC pageable) {    // → local database + sync
    output User[]
  }
}
```

**Why it's cool:**
- **Zero configuration** - developer just calls `useData('query')`, schema handles the rest
- **Multi-strategy** - CACHE, SYNC, LOCAL, STREAM in one API
- **Auto-typing** - TypeScript types generate directly from schema
- **Draft mode** - fork data for safe editing without affecting original
- **Smart merging** - when you save draft, safely merges according to permissions
- **Offline-first** - SYNC strategy enables fully offline applications
- **Real-time ready** - STREAM strategy for live data without extra setup

---

## 💡 How it Works in Practice

### Creator workflow - from idea to production in minutes

**Scenario:** You want to make CRM for your agency.

**Step 1: Conversation with AI (2 minutes)**
```
You: "I need CRM for marketing agency - clients, projects, invoices"
AI: "I'll create a foundation for you. You'll need these entities..." 
    *AI creates schema, basic components, flow*
```

**Step 2: Live URL immediately**
AI generates application → you immediately get URL → application runs, you can test

**Step 3: Marketplace adjustments (5 minutes)**
- Login panel from marketplace → fork → edit logo
- Billing module from Stripe → integration with your account  
- Dashboard layout from another user → customization

**Step 4: AI optimization (runs in background)**
- AI monitors how users use application
- Suggests UX improvements: "Users click wrong button"
- Automatically tests variants, deploys better version

**Result:** Functional CRM in 10 minutes that improves itself.

### Enterprise workflow - safe collaboration

**Scenario:** Team of 5 people developing company application with sensitive data.

**Schema-driven permissions:**
```typescript
type Employee {
  id        ID
  name      String
  salary    Float    @permissions("hr-only")
  manager   String   @permissions("manager-level")
}
```

**Parallel editing:**
- Designer edits UI components  
- Backend dev adds API endpoints
- Frontend dev changes logic
- 3-way merge resolves conflicts without revealing salary data

**AI assistant for team:**
```yaml
# AI agent monitors code quality
steps:
  analyzeChanges:
    type: AI
    tools: [codebase.analyze, tests.run]
    
  suggestRefactor:
    type: conditional
    if: duplicateCode > 3
    action: createPullRequest("Refactor duplicate components")
```

### Marketplace ecosystem

**For creators:**
- Use existing components instead of coding from scratch
- Customize them (it's your code, not black box)
- Publish improved versions back

**For companies:**
- Private marketplace for internal components
- Standardized UI patterns across applications
- Knowledge sharing between teams

**Example:** Netflix login component → your marketing website → your improvements → someone else uses your version

### Multi-platform deployment

**One code, everywhere:**
```pug
// This component runs identically:
user-dashboard
  +sidebar
    navigation-menu
  +content  
    analytics-charts
```

- **Web:** PWA with offline features
- **Mobile:** Native iOS/Android app (Capacitor)
- **Desktop:** Electron app with native integration
- **Kiosk mode:** Full-screen application for iPad

**Zero configuration** - press "Generate mobile app" button → in 30 seconds you have .ipa/.apk file.

# Scotty Platform Features

## Core Platform
- **Zero-configuration fullstack development** - Complete application stack without setup
- **Unified schema-driven architecture** - Single source of truth for frontend, backend, and AI
- **Real-time collaborative development** - Multiple developers editing simultaneously
- **Instant deployment pipeline** - One-click deployment from development to production
- **Progressive complexity disclosure** - Simple start, full power when needed

## AI-Native Development
- **Conversational application building** - Natural language to working applications
- **Context-aware code generation** - AI understands your entire project structure
- **Intelligent component recommendations** - Smart suggestions from marketplace and patterns
- **AI agent tool integration** - Agents use same APIs as human developers
- **Automated testing and optimization** - AI-powered quality assurance

## Component Development
- **Isolated component development** - Storybook-like component isolation and testing
- **Visual component editor** - Click-to-configure with code generation
- **Template system with slots** - Flexible composition without prop drilling
- **Custom styling system** - Tailwind integration with component-scoped variables
- **Hot reload across devices** - Instant preview on web, mobile, and desktop
- **Component marketplace integration** - Share and reuse across projects

## Development & Testing
- **Framework-agnostic function testing** - Test business logic without Vue instances
- **Visual UI testing** - Automated UI testing in component isolation
- **Shadow URL system** - Every component gets its own testable URL
- **Application-level testing** - Full-stack testing with real data flows
- **Live debugging across devices** - Chrome DevTools forwarded to mobile devices
- **Performance profiling tools** - Built-in optimization and monitoring

## Data Architecture
- **Multi-strategy data access** - CACHE, SYNC, LOCAL, STREAM in unified API
- **Offline-first with automatic sync** - Local-first architecture with server coordination
- **Data forking for safe editing** - Draft mode with smart merge capabilities
- **Real-time collaboration with conflict resolution** - Multi-user editing with 3-way merge
- **Schema-based form generation** - AutoForm with complex nested structure support
- **Granular permission control** - Field-level access control with security-aware merging

## Backend Orchestration
- **Visual workflow designer** - No-code backend logic with step-by-step flows
- **Schema-driven API generation** - Automatic REST APIs from data models
- **Serverless execution at scale** - Global lambda deployment with automatic scaling
- **Multi-environment support** - Development, staging, production with data isolation
- **Built-in authentication & permissions** - Enterprise-grade security by default
- **External service integration** - Connect to databases, APIs, and third-party services

## Cross-Platform Deployment
- **Progressive Web Apps** - Automatic PWA generation with offline capabilities
- **Native mobile compilation** - iOS/Android apps from single codebase
- **Desktop application generation** - Electron-based cross-platform desktop apps
- **IoT and Bluetooth integration** - Connect to hardware devices and sensors
- **Over-the-air updates** - Instant app updates without app store approval
- **Platform-specific optimizations** - Native UI patterns and performance tuning

## Marketplace & Collaboration  
- **Component sharing ecosystem** - Public and private component marketplaces
- **Cross-project component editing** - Edit shared components from any project
- **Version control with visual merging** - Git-like workflows with UI-based conflict resolution
- **Team collaboration tools** - Real-time editing, commenting, and review workflows
- **Smart component discovery** - AI-powered recommendations based on usage patterns
- **License and access management** - Fine-grained control over component sharing

## Enterprise & Production
- **Branch-based development workflows** - Feature branches with isolated deployments
- **Custom domain and branding** - White-label deployment with custom domains
- **Advanced security and compliance** - SOC2, GDPR, enterprise authentication
- **Audit trails and change tracking** - Complete history of all modifications
- **Team permission management** - Role-based access control across projects
- **Private marketplace hosting** - Internal component libraries and governance

## Performance & Infrastructure
- **Intelligent caching strategies** - Multi-layer caching from memory to CDN
- **Component lazy loading** - Load only what's needed, when it's needed
- **Automatic code optimization** - Bundle splitting and performance tuning
- **Edge deployment optimization** - CDN distribution with geographic optimization
- **Real-time performance monitoring** - Built-in metrics and alerting
- **Memory-efficient data handling** - Smart resource management and cleanup

