━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DUAL OBSIDIAN BRAIN SETUP: ARCHITECTURE & BUGS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

PHASE 0 — DETECT & INTEGRATE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

First, assess the current workspace:

1. Verify the existence of the primary brain:
* Look for `brain/INDEX.md` and `brain/activeContext.md`.
* If missing, halt and request the user to run the standard "Obsidian Brain Setup" first.


2. Check for the bug brain:
* Look for `bug-brain/INDEX.md`.
* Found → SITUATION A (Update mode)
* Not found → SITUATION B (Init mode)



SITUATION A — Dual Brains active:
→ Continue from PHASE 1

SITUATION B — Initializing Bug Brain:
→ Build the `bug-brain/` skeleton.
→ Create all default folders and files.
→ Rewrite `AGENTS.md` at the project root to support DUAL-BRAIN operations (See PHASE 7).
→ Write in `bug-brain/activeHunt.md`:
Status: Waiting. Bug tracker initialized alongside primary brain.
Run command 'scan for bugs' to populate.
→ Skip to PHASE 8 (final check).

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PHASE 1 — VULNERABILITY & BUG ANALYSIS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Scan the project, specifically cross-referencing components already documented in `brain/components/`.
Skip: node_modules, dist, build, .git, .cache

Identify the following to populate the bug brain:

→ Code blocks containing TODO, FIXME, HACK
→ Unhandled exceptions or brittle error boundaries
→ Race conditions (e.g., dropped Socket.io events, overlapping React state updates)
→ Performance bottlenecks (e.g., redundant database queries, O(n^2) loops)
→ Type safety violations in TypeScript or overuse of 'any'
→ Memory leaks (e.g., uncleared intervals, unclosed NestJS connections)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PHASE 2 — DOMAIN & CROSS-BRAIN STRATEGY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Group bugs by matching them to the intermediate nodes already established in the primary `brain/`.

Domain-Based Grouping (Mirrors Architecture):
Intermediate node = related system domain
Example: domain-socketio, domain-nestjs-gateway, domain-react-client

Rule:
Every bug must logically map to at least one component documented in the primary `brain/`.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PHASE 3 — FOLDER STRUCTURE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Ensure this structure sits adjacent to the existing `brain/` directory:

bug-brain/
├── INDEX.md
├── activeHunt.md
├── bugs/
│   └── [domain-name]/
│       └── [bug-name].md
├── root-causes/
│   └── [cause-name].md
├── proposed-fixes/
│   └── [fix-name].md
├── reproduction-steps/
│   └── [repro-name].md
└── logs/

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PHASE 4 — FILE FORMAT & CROSS-LINKING
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Template for all `bug-brain/` files:

---

## date: YYYY-MM-DD
type: bug | domain | root-cause | fix | reproduction
severity: critical | high | medium | low | none
status: open | investigating | fixed | none

Rules:

* All dates must strictly follow YYYY-MM-DD
* Max 30-40 lines per file
* File names: lowercase, hyphen-separated
* **CROSS-BRAIN RULE:** Use standard [[wikilinks]] to reference architectural components. Obsidian handles global namespaces, so `[[game-board-component]]` will successfully link a bug to a component in the primary brain.
* Every `bug-brain` file must have at least 1 incoming [[wikilink]].

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PHASE 5 — FILE CONTENTS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

bug-brain/INDEX.md
→ System health summary (1-2 sentences)
→ Tally of open critical/high severity bugs
→ [[wikilinks]] to all intermediate bug domain nodes
→ [[activeHunt]] link

bugs/[domain]/[bug-name].md
→ Symptoms of the bug (1-2 sentences)
→ Affected files
→ **CRITICAL:** [[wikilink]] to the specific component(s) in the primary `brain/components/` causing the issue
→ [[wikilink]] to its [[reproduction-steps]], [[root-cause]], and [[proposed-fix]]

bugs/[domain]/[domain-node].md
→ Single-sentence purpose of this domain
→ [[wikilinks]] to all open bugs in this domain
→ [[wikilinks]] to fixed bugs (archived section)

root-causes/[cause-name].md
→ Why the bug occurs (technical explanation)
→ Underlying architectural flaw
→ [[wikilink]] to the related `brain/patterns/` or `brain/decisions/` if a past architectural choice caused it
→ [[wikilinks]] to the bug files

proposed-fixes/[fix-name].md
→ Step-by-step code changes required
→ Code snippet (max 10-15 lines)
→ [[wikilinks]] to the bug and root-cause files

reproduction-steps/[repro-name].md
→ Environment prerequisites
→ Exact numbered sequence of actions to trigger
→ Expected vs. Actual behavior
→ [[wikilink]] to the related bug file

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PHASE 6 — WIKILINK HIERARCHY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

bug-brain/INDEX
└→ bugs/[domain]/[domain-node]
└→ bugs/[domain]/[bug-name]
├→ reproduction-steps/[repro-name]
├→ root-causes/[cause-name]
├→ proposed-fixes/[fix-name]
└→ **CROSS-LINK:** primary-brain/components/[component-name]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PHASE 7 — AGENTS.md (MASTER REWRITE)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Overwrite the existing `AGENTS.md` with the following Dual-Brain Operating Manual:

# DUAL-BRAIN OPERATING MANUAL

This project utilizes two interconnected Obsidian brains:

1. `brain/` - The Architectural Matrix (Features, Components, Decisions, Patterns)
2. `bug-brain/` - The Incident Tracker (Bugs, Root Causes, Fixes, Repros)

## Session Initialization

At the beginning of every session, read in exact order:

1. `brain/INDEX.md` & `brain/activeContext.md`
2. `bug-brain/INDEX.md` & `bug-brain/activeHunt.md`

## Context Switching

Determine your task and navigate accordingly:

* **Building a Feature:** Work primarily in `brain/`. Map new components, log architectural decisions, document patterns.
* **Hunting a Bug:** Work primarily in `bug-brain/`. Document symptoms, trace root causes, outline reproduction steps.
* **Refactoring:** Work across both. If a bug fix changes the architecture, update `brain/components/` and mark the bug as `fixed` in `bug-brain/`.

## Session End & Synchronization

Before closing every session:

1. **If building:** Update `brain/components/`, log decisions, and update `brain/logs/YYYY-MM-DD.md`.
2. **If debugging:**    - Update bug status (`open` -> `fixed`).
* Move fixed bugs to the archived section of their domain node.
* Create `bug-brain/logs/YYYY-MM-DD.md` detailing fixes applied.


3. **Cross-Pollination:**
* If a bug revealed a dangerous pattern, add it to `brain/gotchas/`.
* Ensure all bugs link to the architectural components they affect using global `[[component-name]]` wikilinks.


4. Update BOTH `brain/activeContext.md` and `bug-brain/activeHunt.md` with the current status and Last Updated date.

## General Rules

* Never copy entire source files into either brain; use snippets or references.
* Max 30-40 lines per file. Split if necessary.
* Maintain strict wikilink hierarchy. No file in either brain should be an orphan.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PHASE 8 — FINAL CHECK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

When finished, report:

Dual-Brain Status:

* Primary Brain detected: Yes/No
* Bug Brain initialized: Yes/No
* Cross-brain links established: How many bugs successfully linked to primary components?

File counts (`bug-brain/`):

* Open Bugs / Fixed Bugs
* Root causes / Proposed fixes / Reproductions
* Domain nodes

Link check:

* Any broken [[wikilinks]] between `bug-brain` and `brain`?
* Any unlinked files in `bug-brain`?
