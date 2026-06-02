---
name: test-case-drafting-template
description: Draft reusable, Testomat-ready manual QA test cases for selected product scopes in Claude Code or a local agent. Use when a QA asks to generate, review, stage, or upload manual cases; asks for coverage for a single flow, regression slice, permission scenario, cross-feature seam, or live staging page; or runs /context-bootstrap to create or refresh reusable scope context from the repo. Default to one scope -> one feature -> one flow -> one case -> stop unless the QA explicitly requests a larger coverage set.
---

# Test Case Drafting Template

This skill helps QAs generate durable manual test cases using the team's Testomat format.

Default behavior is intentionally token-efficient: **one scope -> one feature -> one flow -> one case -> stop**.

Use broader coverage only when the QA explicitly asks for a regression set, smoke set, or comprehensive coverage map.

## Core rule

Draft only what the current source of truth supports. Never invent screens, copy, fields, statuses, permissions, redirects, or edge cases.

- Live UI is the source of truth for runnable Steps and Expected results.
- Code is a compass for logic, permissions, states, routes, and cross-surface coverage.
- Product specs explain intent.
- If behavior is not observed in UI, mark UI-observable expectations with `⚠ to verify in UI`.

## Scope selection

Every daily generation or coverage request must include:

`Scope: <scope-name>`

Examples:
- Scope: example-feature
- Scope: billing
- Scope: admin-settings

When scope is provided, read scope-specific context from:

- `references/scopes/<scope-name>/product-context.md`
- `references/scopes/<scope-name>/feature-map.md`

Do not read product context or feature map from another scope.

If scope-specific files do not exist, ask the QA to run `/context-bootstrap` first for that scope.

If scope is missing, ask:

`Which scope should I use? Available scopes are in references/scopes/.`

## Supported modes

### Daily generation mode — default

Use this when the QA asks for a test case, a specific flow, or a small regression slice.

1. Identify `Scope: <scope-name>`.
2. Read `references/scopes/<scope-name>/product-context.md` for stable scope context.
3. Read `references/test-case-format.md` before drafting.
4. Read `references/verification-modes.md` to choose Live UI, Code Skeleton, or Both.
5. Read `references/page-analysis-rules.md` when live UI or browser tooling is available.
6. Read `references/scopes/<scope-name>/feature-map.md` only when the requested flow touches related surfaces, permissions, states, or cross-feature behavior.
7. When reading `references/scopes/<scope-name>/feature-map.md`, always apply its `Scope-specific test rules` section if present.
8. Read `references/regression-rules.md` only when the QA asks for smoke, regression, comprehensive coverage, permissions, or cross-feature seams.
9. Generate or stage exactly one case unless the QA explicitly asks for multiple.
10. Stop.

### `/context-bootstrap` mode

Use this only when the QA asks to bootstrap, create, refresh, or update reusable context for a scope.

The QA must provide:

- `Scope: <scope-name>`
- Product area
- Feature scope
- Main pages/routes, if known
- Relevant roles, if known
- Staging URL, if available
- PRD/spec links, if available

1. Read `references/bootstrap-workflow.md`.
2. Create the scope folder if it does not exist:

   `references/scopes/<scope-name>/`

3. Analyze the repo only enough to update reusable context for the requested scope.
4. Create or update:

   - `references/scopes/<scope-name>/product-context.md`
   - `references/scopes/<scope-name>/feature-map.md`

5. Do not update context files for other scopes.
6. Do not generate test cases.
7. Keep context concise and suitable for all QA teammates.

### Upload mode

Use only when the QA explicitly asks to push/create/upload cases in Testomat.

1. Read `references/testomat.md`.
2. Confirm Testomat MCP/API access is configured.
3. Read staged cases from:

   `<active-skill-directory>/generated-test-cases/<scope-or-feature>/`

4. Upload only under Draft or to the exact target suite provided by the QA.
5. After success, respond only:

   `Done`

## Working principles

- Prefer local context files over scanning the whole repo.
- Do not scan the whole repo during daily generation.
- Inspect source files only when they are needed for the requested feature, policy, route, or UI copy fallback.
- Ask at most one clarifying question when truly blocked. Otherwise proceed with explicit assumptions.
- Never log in, enter credentials, change billing/payment/account settings, or destructively mutate production data.
- Do not claim live verification unless a browser-driving tool was actually used or the QA provided observations.

## Output defaults

For daily generation:

- Produce one Testomat-ready manual case.
- Use `references/test-case-format.md` exactly.
- Target 5–9 steps unless a cross-surface flow genuinely needs more.
- Save staged output to `<active-skill-directory>/generated-test-cases/<scope-or-feature>/<YYYY-MM-DD>-<short-slug>.md` when running in Claude Code.
- In chat, respond only with:
  - `Done`
- Do not add notes unless there is a blocker, `⚠ to verify in UI`, or cleanup action.

For coverage requests:

- First produce a short coverage slice, not a giant coverage map.
- Name only the flows relevant to the requested scope.
- Generate cases only after the QA asks or when the original request clearly asks for cases.

## Reference files

- `references/scopes/<scope-name>/product-context.md` — stable scope context, roles, environments, routes, and repo entry points.
- `references/scopes/<scope-name>/feature-map.md` — scope relationships, permission shape, connected surfaces, and regression seams.
- `references/verification-modes.md` — truth-source modes: live UI, code skeleton, or both.
- `references/page-analysis-rules.md` — how to inspect a page and convert observed deltas into Expected results.
- `references/regression-rules.md` — regression scope, case composition, permissions, seams, and token discipline.
- `references/test-case-format.md` — exact Testomat manual case format.
- `references/examples.md` — quality-bar examples.
- `references/testomat.md` — local staging, upload, and suite placement rules.
- `references/bootstrap-workflow.md` — scope context bootstrap/update workflow.