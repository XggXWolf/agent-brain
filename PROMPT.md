━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
        OBSIDIAN BRAIN SETUP
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

PHASE 0 — DETECT SITUATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Answer these questions:

1. Is there a project in the current directory?
   Look for: package.json, requirements.txt,
   Cargo.toml, go.mod, pom.xml, composer.json
   - Found → SITUATION A
   - Not found → SITUATION B

2. Did the user specify a directory?
   - Yes → scan that directory → SITUATION A
   - No → check current directory → apply above

SITUATION A — Project exists:
  → Continue from PHASE 1

SITUATION B — No project yet:
  → Build only brain/ skeleton and AGENTS.md
  → Create all files with default content
  → Write in activeContext.md:
       Status: Waiting. No project added yet.
       Brain is ready. Once the project is added,
       run: 'update the brain'.
  → Skip to PHASE 8

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PHASE 1 — PROJECT ANALYSIS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Scan the project from top to bottom.
Skip: node_modules, dist, build, .git, .cache,
coverage, __pycache__, .next, .nuxt, vendor

Identify and record:

→ Technology stack (language, framework, runtime)
→ Package manager and key dependencies with versions
→ Folder structure — single-sentence purpose per folder
→ Monorepo or single app?
   - Monorepo: identify workspaces/packages
   - Single app: identify feature groups
→ Entry points (main file, server bootstrap, root component)
→ Single-sentence purpose of every non-trivial file
→ Exported functions, classes, and component names per file
→ Inter-file dependencies:
   which files import which other files (top 15 most-imported)
→ Repeating code patterns (named and noted)
→ Configuration decisions (env vars, feature flags, constants)
→ Lines containing TODO, FIXME, HACK, workaround
→ Complex, fragile, or non-obvious code blocks (1-line note)
→ Data models, schemas, and their relationships
→ External API calls and third-party integrations
→ Auth / permission boundaries (if any)
→ Test coverage gaps (folders or features with no tests)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PHASE 2 — INTERMEDIATE NODE STRATEGY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Choose a grouping strategy based on analysis:

Monorepo:
  Intermediate node = each package/workspace
  Example: apps-web, apps-admin, packages-api

Single app:
  Intermediate node = each feature group
  Example: feature-auth, feature-dashboard

Small project (fewer than 20 files):
  No intermediate nodes needed
  Components link directly to INDEX

Rule:
  If any single file receives more than
  10 incoming links → create an intermediate node

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PHASE 3 — FOLDER STRUCTURE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

brain/
├── INDEX.md
├── activeContext.md
├── architecture.md
├── data-models.md        ← only if data models exist
├── integrations.md       ← only if external APIs exist
├── components/
│   └── [group-name]/
│       └── [component-name].md
├── decisions/
│   ├── [intermediate-node-name].md
│   └── [decision-name].md
├── gotchas/
│   └── [gotcha-name].md
├── patterns/
│   └── [pattern-name].md
└── logs/

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PHASE 4 — FILE FORMAT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Every file must start with:

---
date: YYYY-MM-DD
type: component | decision | gotcha | pattern
      | architecture | integration
status: active | deprecated | needs-review
---

Rules:
- Dates strictly in YYYY-MM-DD format
- Every file: 30–40 lines maximum
- If a file exceeds 40 lines → split it
- File names: lowercase, hyphen-separated,
  no special characters
- Link related files with [[wikilinks]]
- No personal commentary — reflect project as-is
- Every file must have at least 1 incoming
  [[wikilink]] — no orphan files allowed
- Mark status: needs-review on any file containing
  a TODO, FIXME, HACK, or known fragile code

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PHASE 5 — FILE CONTENTS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

INDEX.md
→ Single-sentence purpose of the project
→ Technology stack summary (stack + versions)
→ Entry points (main file / bootstrap)
→ [[wikilinks]] to all intermediate nodes
→ [[wikilinks]] to the 3–5 most critical gotchas
→ [[activeContext]] and [[architecture]] links
→ Quick-reference: top 3 patterns, top 3 decisions

architecture.md
→ Folder structure with one-line purpose per folder
→ Data flow (request lifecycle or event flow)
→ Auth/permission model (if any)
→ External dependencies and integrations
→ Test coverage status (covered / partial / none)
→ [[wikilinks]] to intermediate nodes
→ [[integrations]] link (if file exists)

data-models.md (if applicable)
→ Each model: name, fields, relationships
→ Cardinality (1:1, 1:N, N:M)
→ Validation rules and constraints (1 line each)
→ Extract only from existing schema/model files —
  never invent or assume fields
→ [[wikilinks]] to related components and patterns

integrations.md (if applicable)
→ Each external API or service: name + purpose (1 line)
→ Auth method used (API key, OAuth, etc.)
→ Which components call it → [[wikilinks]]
→ Known rate limits or error modes (if documented)

components/[group]/[component].md
→ Single purpose of the component (1–2 sentences)
→ List of exported functions/props (names only)
→ Key dependencies: which files this imports
→ Key dependents: which files import this
→ Side effects or global state touched (if any)
→ [[wikilinks]] to dependent components
→ [[wikilinks]] to related patterns or decisions
→ [[wikilink]] to its intermediate node

decisions/[intermediate-node].md
→ Single-sentence purpose of this group
→ Dominant pattern(s) used in this group
→ [[wikilinks]] to components it contains
→ [[wikilinks]] to related decisions
→ Any known gotchas scoped to this group

decisions/[decision].md
→ What was decided (1 sentence)
→ Why this choice was made
→ Why alternatives were rejected
→ Trade-offs accepted
→ [[wikilinks]] to affected intermediate nodes

gotchas/[gotcha].md
→ What is the problem (1 sentence)
→ Why it occurs
→ How to prevent / fix it
→ Affected scope (file, feature, or global)
→ [[wikilinks]] to related files
→ After creating:
   - Add [[gotcha-name]] to the most relevant
     component or intermediate node file
   - If critical, add [[gotcha-name]] to
     INDEX.md gotcha list (max 5 entries)

patterns/[pattern].md
→ When to use this pattern
→ When NOT to use it (anti-pattern note)
→ Code example: maximum 10–15 lines
→ [[wikilinks]] to components using this pattern
→ After creating:
   - Add [[pattern-name]] to every component
     file that uses it

activeContext.md
→ Status: Idle. No active task assigned.
→ Current focus: (empty until first task)
→ Last updated: YYYY-MM-DD
→ Next steps: (empty until first task)
→ Open questions: (empty — filled during sessions)
→ Past Logs: (leave empty, logs linked here)

logs/
→ Create the folder, leave it empty

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PHASE 6 — WIKILINK HIERARCHY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Strictly follow this hierarchy:

INDEX
  └→ decisions/[intermediate-node]
       └→ components/[group]/[component]

Forbidden:
✗ Components must not link directly to INDEX
✗ Components must not link to a top-level decision
✗ No single file should receive more than 10 links

Orphan prevention:
✗ No file may exist without at least 1 incoming link
✓ Every new file → immediately update its parent
  to include a [[wikilink]] to it
✓ New gotcha or pattern → add link in the most
  relevant component or intermediate node file

Cross-links allowed (use sparingly):
✓ gotchas/ ↔ patterns/ (if directly related)
✓ data-models/ ↔ components/ (for model consumers)
✓ integrations/ ↔ components/ (for API callers)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PHASE 7 — AGENTS.md
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Write the following into AGENTS.md:

# Session Start
Read at the start of every session (in order):
1. brain/INDEX.md
2. brain/activeContext.md

Read on demand based on the task:
- Component change →
  open the relevant intermediate node,
  then the specific component file
- New feature →
  brain/patterns/ + brain/decisions/
- Debugging →
  brain/gotchas/ (only open when needed)
- Architecture question →
  brain/architecture.md
- Database / schema work →
  brain/data-models.md
- External API work →
  brain/integrations.md

# Session End
Before closing every session:
1. Update changed components in brain/components/
2. Add new decisions in brain/decisions/
3. Add discovered gotchas in brain/gotchas/
   → Add [[gotcha-name]] to the most relevant
     component or intermediate node
   → If critical, add to INDEX.md (max 5)
4. Add new patterns in brain/patterns/
   → Add [[pattern-name]] to every component
     file that uses this pattern
5. Update brain/integrations.md if any
   external API was added or changed
6. Create brain/logs/YYYY-MM-DD.md with:
   - Files changed
   - Decisions made
   - Open questions unresolved
   - Unfinished work
   → Add [[YYYY-MM-DD]] to activeContext.md
     under "Past Logs"
7. Update brain/activeContext.md:
   - Current focus
   - Next steps
   - Open questions
   - Last updated: YYYY-MM-DD

# General Rules
- All dates must strictly follow YYYY-MM-DD
- Open source files for details —
  never copy source code into the brain
- Every file: 30–40 lines max — split if larger
- If a file receives more than 10 incoming links →
  create an intermediate node
- Maintain [[wikilink]] hierarchy at all times
- No personal commentary — reflect project as-is
- Every new file must immediately receive
  at least 1 incoming [[wikilink]] — no orphans
- Set status: needs-review on any file that
  documents a known bug, TODO, or fragile code

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PHASE 8 — FINAL CHECK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

When finished, report:

Detected project type:
- Monorepo / Single app / No project

File counts:
- Component files: N
- Decision files: N
- Gotcha files: N
- Pattern files: N
- Integration files: N
- Intermediate nodes: N

Coverage check:
- Every entry point documented?
- Every external API in integrations.md?
- Every TODO/FIXME captured in a gotcha?

Link check:
- Any file with more than 10 incoming links?
- Any broken [[wikilinks]]?
- Any orphan (unlinked) files?
- Any referenced but uncreated files?
- Any file with status: needs-review?
