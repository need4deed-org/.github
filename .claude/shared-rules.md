# Shared project rules

These rules apply to **all three repos** (`be`, `fe`, `sdk`). This file is synced from the
org `.github` repo — do not edit it inside a downstream repo; change it at the source and let
the sync open a PR. Repo-specific rules live below the import in each repo's own `CLAUDE.md`.

## API changes go through the SDK contract first

The `sdk` is the single source of truth for the API contract. Any change to the API surface
(endpoints, request/response shapes, types, error codes) **MUST** follow this order:

1. Define or update the contract in the `sdk` repo first.
2. Publish the new SDK version to npm.
3. Only then update `be` and `fe` to consume the change.

**IMPORTANT:** `be` and `fe` MUST depend on the SDK as published on **npmjs.com** — never on the
local `sdk` checkout or a sibling folder. Do not use `file:../sdk`, `npm link`, workspace or
`link:` references, or any other local linking for the SDK dependency. Pin to a version that is
actually published. If the version you need isn't on npmjs.com yet, the work is **not ready** to
land in `be`/`fe` — finish and publish the SDK first.

Do not implement or "stub" an API change in `be` or `fe` ahead of the contract. If the contract is
missing, wrong, or incomplete, fix it in `sdk` and publish — never work around it locally.

Allways make sure all API related issues are based on the latest dependency "need4deed-sdk".

## Reuse before you create

Before adding any new util, helper, hook, component, or shared function, **first search** the
codebase (and the SDK) for something that already does the job. Prefer reusing or extending
existing code over writing a near-duplicate. If nothing fits and you must add a new one, state
briefly why the existing options didn't work.

## Be conservative with database schema changes

Before altering the database schema:

- Confirm the change is **absolutely necessary** and cannot reasonably be solved without touching
  the schema.
- Confirm it is **semantically correct** — names and structure must match existing modeling
  conventions and clearly express what the data represents.

Surface the proposed change and your reasoning _before_ writing a migration. Schema changes are
deliberate decisions, not incidental side effects of a feature.

## Clean up processes you launch

Any dev server or other long-running process started to check or verify a change (`yarn dev`,
`yarn dev:docker`, `yarn start`, etc.) **must be killed once you're done with it**. Do not leave
orphaned processes running — e.g. stray `next-server`/node instances piling up on ports 3000+.

## Code comments: almost none

Default to **no comments**. Name things so the code explains itself.

- Allowed: a rare one-line comment for a non-obvious _why_ (e.g. a security or data-protection
  gotcha), and tool directives (`eslint-disable`, `@ts-expect-error`).
- Not allowed: issue/PR references (`fe#123`, `be#456`), change history, review discussion,
  explanations of what the code does, multi-line rationale. That belongs in the commit message or
  PR description.
- Don't copy the comment style of surrounding code; remove such comments when you touch it.

## Domain names: one name per thing

Each name below means exactly one thing in the UI, issues, PRs, code and database. Never use it
for anything else, and use it in new issues and code. Where "Code today" differs, the rename is
tracked in the "Clear names" epic; until it lands, map the old code name to the new name here.

| Name | What it is | UI (en / de) | Code today |
| --- | --- | --- | --- |
| need4deed event | An event need4deed runs itself, managed in the Calendar, with sign-ups | Events / Veranstaltungen | `EventN4D`, table `event_n4d` |
| opportunity:event | An NGO opportunity of type event: one date, one-off help | Event opportunity / Einsatz bei Veranstaltung | type value `events` (`ProfileVolunteeringType.EVENTS`) |
| Activity | A kind of volunteering work, like a skill | Activities / Aktivitäten | `Activity`, table `activity` |
| Time log | Volunteering hours logged per match | Time log / Zeiterfassung | `ActivityLog`, table `activity_log`, `/activity-log` |
| Profile changes tracker | Who changed what on a volunteer or opportunity profile, and when | Profile changes / Profiländerungen | `VolunteerAuditLog` (be, sdk), `VolunteerActivityLog` (fe) |
| Agent | An NGO's accommodation centre (Einrichtung) | NGOs / Einrichtungen | `Agent`, table `agent` |

- Never call a profile change or a time log entry an "activity" or "activity log".
- Never call an opportunity of type event a "need4deed event", or the reverse.
- Write "AI agent" for AI tools; a bare "agent" is always the NGO.

## Cases for names

- all TypeScript names are in camelCase
- all SQL names are in snake_case
- all enum values, file names, etc. are in kebab-case
