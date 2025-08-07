# Low-code platform

# How We Built Scotty for Lower Cognitive Load, Simpler Development, Fewer Bugs, and True Platform Power

> **It looks like Scotty has too many features. It does.**  
> But most capabilities emerge naturally from our novel low-code architecture—they're not hardcoded add-ons. This is why Scotty serves non-developers, experienced developers, and enterprises equally well, without trying to be everything to everyone.

Below is how it actually works—each capability is unique in today's development world, yet all stem from the same core engine...

## 1. Goal: Maximum Simplicity, Minimum Mistakes

* Everything is designed for the simplest possible app development—no unnecessary steps, minimal learning curve, almost zero room for errors.
* All the “wiring” is hidden—users configure nothing, the engine connects everything automatically.
* Every component comes instantly with everything you need (tests, worker, global store, state)—already prepared and linked.

## 2. Instant Deployment, Zero Builds

* Every change is live instantly—app, API, or component gets a fresh URL the second you hit save.
* Preview URLs for every branch, environment, or even single component—test in isolation, no build step.
* Rollbacks and switching between versions/branches is one click. No builds, no waiting.

## 3. Strict Separation of Concerns

* Each component has its own template (structure), styles (visuals), logic (behavior), state (data), tests, and worker.
* Everything is separated = **drastically lower cognitive load** and safe, targeted AI edits only where needed.

## 4. Evolving the Tools Devs Know—Modernized for AI

* We took the best of Vue, Pug, CSS, Tailwind, Prisma, Tanstack, etc.—then stripped the legacy and complexity.
* Optimized for fast, effective development by both humans and AI agents.
* Syntax is lean, direct, readable—no need to study docs.
* **Result: New users (and AIs) instantly get how to write or edit apps.**

## 5. Styles = Real CSS + Tailwind + TypeScript Functions

* Styles are pure CSS but support Tailwind utilities (written as CSS, not as class names in the template) and direct TS functions from your logic.
* **Extremely easy** to override styles—even deep inside nested components—no prop drilling.

## 6. Components: Everything Connected & Reusable

* Each component has its template, styles, logic, store, worker, and tests—already wired up.
* **Reusability & Marketplace:** Any component can be **forked, versioned, shared, and sold** (or just used) across all projects—works platform-wide.
* Components are **isolated (shadow URLs)** and instantly testable.
* **Visual version control & merge conflict UI:** Resolve conflicts visually, no need to read diffs.

## 7. Levels of Editing: From Vibe Coding to Full Control

* **Vibe coding:** Chat with the AI, describe what you want, and your app is live online on its own URL right away.
* **Editor:** Click through smart forms or write code directly.
* **Full code access:** When needed, everything is editable in the component.

## 8. Data & Schema: Single Source of Truth, No Codegen

* **Schema** = the only source of truth (data, API, permissions, strategies, validation, auto-forms…)
* No “codegen”—define it in schema, and it just works everywhere (API, forms, tests, validation, FE/BE).
* **No desync errors**, nothing to patch in documentation.

## 9. Backend (Query): Clear Layers, Everything Linked, Visual Orchestration

* Each backend module (“Query”) has its own:
  * **Schema** (types, validation, permissions, API)
  * **Step Flow** (visual/yaml workflow—every step can be custom TypeScript)
  * **Methods** (logic)
  * **Tests** (built right in)
  * **Executions** (logs, runs)
  * **Metrics** (telemetry, reporting)
* **Visual editor for backend flows** (not just code).
* Everything connected, no wiring.

## 10. Atomic Edits (AI Native)

* **AI orchestration:** Agents **don’t write new code for everything**, they propose atomic changes—move blocks, tweak params, edit properties at the API/component level.
* **Audit trail, validation, safe merging:** Every change is audited, validated, and safely merged (AI can’t overwrite what it shouldn’t).
* **Automated migration:** AI agents can migrate code and APIs from old platforms in minutes.

## 11. Safe Merging by Schema (No Data Leaks)

* **Merge engine** ensures no data leaks or overwrites of invisible data.
* Merging is schema-driven, with **field-level permissions** (every field can have its own access rules).

## 12. Data: Strategies, Security, Offline, Granular Permissions

* **Data strategies:** CACHE, SYNC, STREAM, LOCAL (includes offline-first, with sync when online).
* **Offline-first** architecture, encrypted browser databases (asymmetric crypto), ability to remote-wipe data.
* **Field-level security:** Permissions on each (deep) field, not just collection/table.
* **AutoForm from schema, supports deep nesting.**

## 13. Remote Debugging, Testing & Perf Tools

* **Real Chrome DevTools, even for mobile—no cables.**
* **Shadow URLs:** Isolated testing and debugging for every component, preview for each branch/env.
* **Perf profiling, state inspector, live monitoring.**
* **Automated UI and functional tests** (in every component).
* **CDN delivery, OTA updates:** Deployment optimized with CDN, instant updates across platforms.

## 14. Forking, Branching, A/B Testing

* Every fork, branch, or A/B test has its own URL.
* Switching between versions is instant (no builds).
* A/B tests and multi-env setups are config-only, never a build step.
* **Audit logs, roles, private marketplace:** Everything tracked and secure, built for teams and enterprises.

## 15. Deployment Targets: Web, Mobile, Desktop, IoT

* **Single architecture, deploy anywhere:**
  * Web (PWA), mobile (Capacitor), desktop (Electron), IoT, BLE, OTA updates on all platforms.
* **Marketplace for deployment targets:** Pick your target, everything adapts under the hood.

***

          