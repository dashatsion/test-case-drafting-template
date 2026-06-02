# Test Case Format

Manual QA cases are web cases in the team's Testomat format. Two title styles are accepted; use whichever fits the case:

- **Action-style:** `View Updates page and navigate between pages`
- **ISBAT-style:** `ISBAT navigate between pages of the Updates list`

Use a clear, outcome-focused title either way. Match existing sibling cases in the target suite for consistency.

## Required shape

```markdown
<Title — action-style or ISBAT>

### Permission
Admin/Owner.
[Role only. Omit this whole section when there is no role-specific behavior.]

### Pre-conditions
1. User is logged in.
2. User has the required access/permissions for this flow.
3. [Only the setup the scenario actually needs — seed data, feature flags, enabled add-ons, existing records, counts that activate a state, or the screen that's open.]

### Steps
1. <Action using exact UI copy from the source of truth>
  ***Expected result***:
  <Visible, user-facing result.>
  <A second observable assertion for the same step, if relevant.>
2. Click [Create new]
  ***Expected result***:
  <Next visible state.>
```

The case must end after the final step's Expected result.

Do not append a `Notes` section.

## Final case body rules

The final Testomat case body must include only:

- Title
- `### Permission` when role-specific behavior matters
- `### Pre-conditions`
- `### Steps`

Do not include these sections in the final Testomat case body:

- `Notes`
- `Verification mode`
- `Assumptions`
- `Cleanup reminders`
- `Internal source references`
- Repo/file references
- Explanations about how the case was generated

If assumptions, cleanup reminders, or `⚠ to verify in UI` items exist, mention them briefly in the chat response only, not inside the Testomat case body.

Before upload to Testomat, remove any review notes from the case body.

## Formatting rules

- **Expected results** use `***Expected result***:` and may list several observable assertions for one step.
- Keep Expected results user-visible; avoid backend-only assertions unless the case is specifically about persistence/state and the UI exposes it.
- **Redirects and state changes are first-class expected results.** If an action navigates, assert the destination ("the … page opens" / URL changes to the detail page). If an element changes state, assert the change explicitly (button becomes disabled, status badge changes, a row appears/disappears, a toast shows).
- Expected results should come from observing the page before and after the action. See `verification-modes.md` and `page-analysis-rules.md`.
- When a step is drafted from code only and not yet observed, append `⚠ to verify in UI`.
- **Buttons:** bracket format — `Click [Create new]`, `Click [Save]`.
- **Links:** name them as links — `Click "View all responses" link`.
- **Screens/modals:** include the noun — `the "Create update" modal`, `the Home page`, `the Settings screen`.
- **Filters/fields:** quote exact labels — the `"Status"` filter, the `"Search"` field.
- Keep steps **5–9**, never above **10** without explicit approval.
- Use exact copy from the source of truth. If you don't have the exact label yet, check the live app or source files — do not paraphrase.

## Permission section

- Include `### Permission` only when behavior differs by role.
- When present, list the role(s) the relevant product rule, policy, or permission model actually grants.
- Example roles: Admin/Owner, Billing Admin, Manager, Author, General, Member, Viewer.
- If a flow behaves differently for two roles, write separate permission-specific cases with the correct role prefilled, rather than branching inside one case.

## Pre-conditions

- Write in plain QA language.
- Include only what the scenario needs to run.
- Common preconditions:
  - User is logged in.
  - User has the required access/permissions.
  - Required feature flag, add-on, plan, or suite is enabled.
  - Required seed data or existing records are available.
  - The relevant page/screen is open.
- Add feature-state setup only when a state depends on it, for example:
  - "More than 10 records exist, so pagination is active."
  - "A recurring meeting series exists."
  - "A user with Manager permissions exists."
  - "The account has access to the selected feature."
- Do not encode implementation details, tokens, table names, or internal IDs unless the case is specifically about that.

## Scope-specific rules

Do not put product-specific assumptions into this generic format file.

Scope-specific requirements must live in:

- `references/scopes/<scope-name>/product-context.md`
- `references/scopes/<scope-name>/feature-map.md`
- `references/examples.md` or scope-specific examples if they exist

Examples:

- Operations-specific precondition: `The Operations Suite has been purchased.`
- Billing-specific precondition: `The account has billing access.`
- Home-specific precondition: `The user has dashboard widgets available.`

These belong to the scope context or examples, not the generic format rules.

## What a good case looks like

See `examples.md` for worked examples. Some examples may be scope-specific.

The quality bar: a tester who has never seen the feature can run the case top to bottom and know exactly what "pass" means at each step, using only what's written.