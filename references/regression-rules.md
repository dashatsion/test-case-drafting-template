# Scope & Regression Rules

These rules keep generated cases durable and useful for regression across any product scope.

Use scope-specific rules from:

`references/scopes/<scope-name>/feature-map.md`

when the selected scope has special requirements, connected surfaces, permissions, or required preconditions.

## Scope

Default behavior is focused and token-efficient:

`one scope → one feature → one flow → one case → stop`

Broader coverage is generated only when the QA explicitly asks for:

- smoke coverage
- regression slice
- comprehensive coverage
- permission coverage
- cross-surface coverage

For coverage requests:

- Start with a short coverage slice.
- Do not generate a giant coverage map unless explicitly requested.
- Cover the logic relevant to the requested flow, not every possible product behavior.
- No `General` dumping-ground cases — each case targets a specific, named scenario.
- Depth comes from focused cases, not bloated mega-cases.

## Compose into logical flows, not atomic checks

Build each case as one realistic user journey.

Combine related actions when they naturally belong together:

- **Life-cycle flow:** create → observe/use → edit → delete/archive, when this is a realistic path.
- **Paired actions:** pause/resume, archive/unarchive, add/remove, expand/collapse, enable/disable, start/stop.
- **Related fields/options:** verify several fields or settings in the same flow when they belong to the same user action.
- **State transitions in context:** trigger a state change through the scenario that causes it.
- **Cross-screen or cross-surface journey:** act in one place → verify the effect elsewhere → return or confirm the original surface.

Do not split a required end-to-end path into atomic cases when the tester must run the whole path anyway.

## Boundaries

Do not over-merge.

Split cases when:

- flows are unrelated;
- different roles produce different behavior;
- a failure would not point to a clear cause;
- the case becomes too long to run and debug;
- a setup/precondition is meaningfully different;
- a destructive action should be isolated.

Role/permission differences should be separate cases, not branches inside one case.

## Make cases durable

A durable case survives small UI changes and still asserts the right behavior.

Prefer:

- user-visible outcomes;
- state changes;
- redirects;
- list/card/table updates;
- enabled/disabled behavior;
- permission outcomes;
- count/status changes;
- saved values shown after refresh or navigation.

Avoid:

- pixel positions;
- layout-only assertions;
- implementation details;
- DOM-specific wording;
- internal IDs;
- backend-only claims unless the UI exposes the outcome.

Tie each Expected result to behavior supported by the source of truth.

## Permissions

When a flow depends on role or access level:

- write separate permission-specific cases;
- use the role names from the selected scope context;
- derive exact permission behavior from the relevant policy, product rule, or observed UI;
- do not guess permission outcomes from memory;
- include no-access or gated states when they are valid coverage dimensions for the selected scope.

Examples of permission-sensitive dimensions:

- admin vs non-admin behavior;
- manager vs direct report behavior;
- owner vs viewer behavior;
- feature enabled vs disabled;
- add-on purchased vs not purchased;
- object owner vs watcher/assignee/member;
- group membership;
- read-only vs editable access.

If the selected scope has required permission rules, they should be documented in:

`references/scopes/<scope-name>/feature-map.md`

under:

`## Scope-specific test rules`

## Cross-surface regression

Use the selected scope's feature map:

`references/scopes/<scope-name>/feature-map.md`

Include cross-surface checks when the flow affects another place in the product.

Examples:

- a change on one page appears in a dashboard widget;
- an item created in one area appears in a profile section;
- a setting affects navigation or visibility elsewhere;
- a status change affects filters, counters, cards, or reports;
- a linked object updates consistently across pages;
- removing a relationship does not delete the underlying object unless that is the intended behavior.

Do not add cross-surface checks just to make a case bigger. Add them only when the selected scope context or observed product behavior shows that another surface is affected.

## Validation and sad paths

Include validation and sad paths when they are meaningful for the requested flow.

Good candidates:

- required fields;
- invalid format;
- duplicate names or conflicting values;
- permission denied;
- disabled submit button;
- empty state;
- loading/failure state;
- cancel/close without saving;
- save failure or retry behavior;
- archived/deleted/read-only state.

For unreachable states, write a clear precondition and mark UI-observable expectations with:

`⚠ to verify in UI`

## Smoke vs regression vs comprehensive

### Smoke

Use when QA asks for a minimal confidence check.

Smoke should cover:

- one primary happy path;
- the main visible outcome;
- only the most critical secondary surface if required.

### Regression slice

Use when QA asks for practical regression coverage.

Regression slice should cover:

- happy path;
- key permission-sensitive path;
- key validation/sad path;
- key state transition;
- key cross-surface seam if applicable.

### Comprehensive

Use only when QA explicitly asks for comprehensive coverage.

Comprehensive can include:

- all major types/modes;
- all relevant permission branches;
- important validations;
- state transitions;
- cross-surface seams;
- unreachable states with clear preconditions.

## Efficiency

- Do not reference "all of the above" or "previous cases"; name the exact case or flow.
- Do not print long coverage maps unless asked.
- Do not print suite trees, counts, or summaries unless asked.
- For daily work, generate one case and stop.
- For large uploads, process in batches of 3–5.
- Skip read-back validation unless QA asks, upload is uncertain, or Testomat returns ambiguous data.