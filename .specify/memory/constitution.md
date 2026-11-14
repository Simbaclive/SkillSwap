<!--
Sync Impact Report
- Version change: unversioned template → 1.0.0 (initial project constitution).
- Modified principles: template placeholders → SkillSwap product value, TypeScript
  correctness, Next.js architecture, utility-first UI, and verified delivery.
- Added sections: Technology & Implementation Standards; Team Workflow & Quality Gates.
- Removed sections: none.
- Templates: ✅ .specify/templates/plan-template.md
  ✅ .specify/templates/spec-template.md
  ✅ .specify/templates/tasks-template.md
  ✅ .github/agents/speckit.tasks.agent.md
  ✅ .github/agents/speckit.plan.agent.md (reviewed; already compatible)
  ✅ .github/agents/speckit.specify.agent.md (reviewed; already compatible)
  ⚠ .specify/templates/commands/*.md (directory absent; no command templates to update)
  ✅ README.md and AGENTS.md (reviewed; no conflicting project rules found)
- Ratification date set to the date this initial constitution was established.
-->
# SkillSwap Constitution

## Core Principles

### I. Useful Skill Exchange
SkillSwap MUST center its features on helping people offer skills, request skills, and
propose mutually useful swaps. Each feature MUST make its intended user value and
relevant exchange flow clear in its specification and acceptance criteria. This keeps
product work aligned with the app's purpose rather than adding unrelated functionality.

### II. Strict TypeScript
Application code MUST use TypeScript with strict checking enabled and MUST NOT use
`any`, including through casts or implicit escape hatches. Values from external,
untrusted, or otherwise uncertain sources MUST be typed as `unknown` and narrowed or
validated before use. Shared types MUST express real domain contracts. This reduces
runtime errors and makes skill listings and swap flows safer to evolve.

### III. Next.js App Router
The application MUST use Next.js App Router and its file-based routing conventions
under `app/`; new routes MUST NOT use the Pages Router. Components MUST be Server
Components by default. A component MUST use the Client Component boundary only when
browser APIs, local interaction state, or event handlers require it, and that boundary
MUST remain as narrow as practical. This preserves framework conventions and avoids
unnecessary client-side code.

### IV. Utility-First Interface
UI styling MUST use Tailwind CSS utility classes by default. Custom CSS MUST be added
only when the design cannot be expressed clearly and maintainably with the available
utilities, and its need MUST be apparent from the code or review. Interfaces MUST
remain responsive, accessible, and consistent across the offer, request, and swap
journeys.

### V. Tested, Reviewable Changes
Changes that alter user-visible behavior or application logic MUST include automated
tests at the appropriate unit, integration, or end-to-end level. Tests MUST verify the
intended behavior and important failure or boundary cases; a change without an
appropriate automated test MUST explain why in its plan. Every change MUST pass the
repository's available lint, type-check, and test validations before merge, or clearly
record unavailable checks and their impact. This keeps core exchange workflows
reliable as features are added.

## Technology & Implementation Standards

- The required stack is Next.js App Router, TypeScript, and Tailwind CSS. Plans MUST
  identify how their design follows these requirements and MUST justify any proposed
  exception before implementation.
- Keep routing and route-specific layouts in `app/`. Shared React components belong
  in `components/`; reusable non-UI logic belongs in `lib/`. Follow Next.js reserved
  route filenames and conventions where applicable.
- Name React components and their files in PascalCase, functions, variables, and
  hooks in camelCase, and types/interfaces in PascalCase. Name feature directories
  and non-reserved route segments in lowercase kebab-case. Follow framework-mandated
  filenames where they differ.
- Use Tailwind utilities before adding styles to `app/globals.css` or other custom CSS.
  Keep CSS scoped to a concrete design need rather than duplicating utility styling.
- The project currently has no configured automated test runner. Each plan MUST
  select or identify the test tooling needed for its scope; do not treat the absence
  of a test script as a reason to omit required coverage.

## Team Workflow & Quality Gates

- Feature specifications MUST describe the user value and observable behavior;
  implementation choices and compliance with this constitution MUST be recorded in
  the implementation plan.
- Plans MUST include a Constitution Check for the stack, strict typing, routing and
  component boundaries, styling, naming, and tests. Any exception MUST state its
  reason, alternatives considered, and mitigation.
- Contributors MUST communicate ownership and overlapping edits before parallel work.
  Pull requests MUST summarize the change, link relevant feature documentation, and
  receive review from at least one teammate before merge.
- Reviewers MUST verify behavior, test coverage, type safety, accessibility, and
  compliance with the Constitution Check. Contributors MUST resolve review feedback
  or document an agreed follow-up before merging.
- Pull requests MUST report validation commands and outcomes. Secrets MUST NOT be
  added to source control; unrelated generated or local files MUST NOT be included.

## Governance

This constitution is the project's governing source for engineering practices and
takes precedence over conflicting feature-level guidance. Amendments MUST be made in
this file and propagated to dependent specification, planning, task, and development
guidance templates. The amendment MUST include a Sync Impact Report and an explanation
of material changes.

Constitution amendments require agreement from the project team and review of the
affected templates and implementation guidance. Feature plans and pull requests MUST
check compliance; any approved exception MUST be explicit, scoped, and documented.

Versioning follows semantic versioning: MAJOR for incompatible removals or
redefinitions of principles, MINOR for new principles or materially expanded
requirements, and PATCH for clarifications and non-semantic refinements. Compliance
MUST be reviewed during planning and pull-request review, with gaps recorded as
follow-up work rather than silently waived.

**Version**: 1.0.0 | **Ratified**: 2026-11-14 | **Last Amended**: 2026-11-14
