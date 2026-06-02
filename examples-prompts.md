# Example Prompts

Reusable prompt examples for the `test-case-drafting-template` skill.

These prompts are intentionally generic. Replace placeholders with your own scope, feature, role, URL, and test management details.

---

## Generate one local test case

Use for daily work when you need one ready-to-review manual test case for a specific flow. This does not upload anything to a test management system.

```text
Use the test-case-drafting-template skill.

Generate ONE test-management-ready manual test case.

Scope: <scope-name>
Feature: <feature-name>
Flow: <specific-flow>
Role: <user-role>
Page or app URL: <url-or-n/a>

Source of truth: <spec | browser page | PR | codebase | notes | hybrid>

Use browser-verified mode if browser tools are available.
If browser tools are not available, do not claim live verification.
Do not upload to a test management system.
Save the file to generated-test-cases/<scope-name>/.
Stop after one case.
```

---

## Generate a skeleton without browser access

Use when you do not have access to a live browser, staging environment, or app session. The output should be treated as a draft.

```text
Use the test-case-drafting-template skill.

Generate ONE provisional manual test case skeleton.

Scope: <scope-name>
Feature: <feature-name>
Flow: <specific-flow>
Role: <user-role>
Known behavior / notes:
<paste notes, acceptance criteria, or confirmed behavior>

Browser tools are not available.
Do not claim live verification.
Mark all UI-observable expected results with: [to verify in UI].
Do not upload to a test management system.
Stop after one case.
```

---

## Create a short coverage slice

Use when you want to understand the test coverage before writing full test cases.

```text
Use the test-case-drafting-template skill.

Create a short coverage slice only.

Scope: <scope-name>
Feature: <feature-name>
Flow or area: <flow-or-area>
Context:
<paste notes, requirements, PR summary, or browser observations>

Do not generate test cases yet.
List only:
- key flows;
- permissions or roles;
- validations;
- connected surfaces;
- regression risks;
- open questions.

Keep it concise.
```

---

## Create test cases from a spec

Use when you have requirements, acceptance criteria, a PRD, a design note, a table, or another written source of truth.

```text
Use the test-case-drafting-template skill.

Mode: spec-based

Scope: <scope-name>
Feature: <feature-name>
Flow: <specific-flow>
Role: <user-role>

Spec / requirements:
<paste the spec, acceptance criteria, notes, or table>

Generate practical manual test cases.

Rules:
- Use only the provided context.
- Do not invent product behavior.
- Mark assumptions clearly.
- Add open questions when expected behavior is unclear.
- Keep cases runnable.
- Use the configured test case format.
- Do not upload to a test management system.
```

---

## Create test cases from code or PR context

Use when the source of truth is a PR, changed files, routes, components, API contracts, or implementation notes.

```text
Use the test-case-drafting-template skill.

Mode: code/PR-based

Scope: <scope-name>
Feature: <feature-name>
Flow: <specific-flow>

PR / code context:
<paste PR description, changed files summary, implementation notes, or relevant snippets>

Generate a QA-focused test case draft.

Include:
- implementation-based risks;
- happy path;
- sad path;
- edge cases;
- regression areas;
- open questions.

Rules:
- Use code as implementation evidence, not as product intent.
- Do not invent expected behavior.
- Mark unclear behavior as an open question.
- Do not claim browser verification.
- Do not upload to a test management system.
```

---

## Create test cases from browser observations

Use when QA has already walked through the flow in a real browser or app session and can provide observed UI behavior.

```text
Use the test-case-drafting-template skill.

Mode: browser-verified

Scope: <scope-name>
Feature: <feature-name>
Flow: <specific-flow>
Role: <user-role>

Observed browser/app notes:
- Entry point:
- Screen/page title:
- Buttons:
- Field labels:
- Required fields:
- Optional fields:
- Default states:
- Toasts or confirmations:
- Resulting page/state:
- Connected surfaces:
- Notes:

Generate ONE final manual test case using only the observed behavior.

Rules:
- Use exact UI wording from the observed notes.
- Do not invent buttons, fields, screens, or expected results.
- If something is missing from the notes, add it as an open question.
- Do not upload to a test management system.
```

---

## Create or update reusable context for this feature scope

Use when bootstrapping or refreshing reusable context for a product or feature scope. This should not generate test cases.

```text
Use the test-case-drafting-template skill.

/context-bootstrap

Create or update reusable context for this feature scope.

Scope: <scope-name>

Product area:
<product-area-name>

Feature scope:
<what this scope includes>

Main pages/routes:
<pages, routes, screens, or entry points>

Known related surfaces:
<other surfaces where this feature appears or has side effects>

Relevant roles:
<roles or permissions that may change behavior>

Source links or notes:
<spec links, PRD links, ticket links, design links, or N/A>

Browser/app URL:
<url or N/A>

Analyze only the files, notes, and pages needed for this scope.

Create or update:
- references/scopes/<scope-name>/product-context.md
- references/scopes/<scope-name>/feature-map.md

Do not update context files for other scopes.
Do not generate test cases.
Do not upload to a test management system.
Keep the context concise and reusable.

After completion, respond only with: Done.
```

---

## Upload a reviewed generated case to a test management system

Use only after a generated case has been reviewed and approved.

```text
Use the test-case-drafting-template skill.

Upload this reviewed generated case file to the configured test management system:

File:
generated-test-cases/<scope-name>/<file-name>.md

Target project:
<project-name-or-project-url>

Target suite:
<suite-name-or-suite-url>

Rules:
- Upload only if the target project and suite are clear.
- If the target suite is unclear, ask before uploading.
- Do not create duplicate suites.
- Check for a related existing suite or similar test if the workflow supports it.
- After success, respond only: Done.
```

---

## Prompt field guide

Use these placeholders consistently:

- `Scope`: short machine-friendly folder name, for example `billing`, `home`, `account-settings`, or `example-feature`.
- `Product area`: human-readable product area name.
- `Feature`: specific feature or sub-feature.
- `Flow`: exact user workflow to cover.
- `Role`: user role or permission level relevant to the case.
- `Main pages/routes`: pages, screens, or routes where the assistant should start analysis.
- `Known related surfaces`: other product areas where the feature may appear or have side effects.
- `Source links or notes`: specs, tickets, designs, PRs, or notes.
- `Browser/app URL`: URL or app screen used for live verification.
- `Target project`: project in the configured test management system.
- `Target suite`: suite/folder where reviewed cases should be uploaded.