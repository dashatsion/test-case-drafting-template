# Test Case Drafting Template

A reusable AI skill template for drafting practical QA test cases from product context.

This template helps QA engineers generate consistent, product-aware manual test cases using specs, docs, PRs, code context, browser observations, and test management context.

The template is product-agnostic. Replace the example scope with your own product area, feature, or workflow.

## What this skill does

Use this template to:

- draft manual test cases from product or feature context;
- structure test cases in a consistent format;
- reuse product scope context across QA tasks;
- avoid generic or duplicated test coverage;
- support spec-based, code/PR-based, browser-verified, or hybrid test case generation;
- keep reusable QA rules, examples, and context in one place.

## Recommended repository structure

```text
test-case-drafting-template/
├── README.md
├── SKILL.md
├── examples-prompts.md
├── generated-test-cases/
└── references/
    ├── scopes/
    │   └── example-feature/
    │       ├── product-context.md
    │       └── feature-map.md
    ├── bootstrap-workflow.md
    ├── examples.md
    ├── page-analysis-rules.md
    ├── regression-rules.md
    ├── test-case-format.md
    ├── testomat.md
    └── verification-modes.md
```

## Key files

### `SKILL.md`

Main skill instructions.

This file defines when the skill should be used, how it should behave, which references to load, and how to handle daily generation, context bootstrap, and upload workflows.

### `examples-prompts.md`

Reusable prompt examples for common workflows, such as:

- generating one local test case;
- creating a skeleton without browser access;
- creating a short coverage slice;
- generating from a spec;
- generating from code or PR context;
- generating from browser observations;
- creating or updating reusable scope context;
- uploading reviewed cases to a test management system.

### `generated-test-cases/`

Optional workspace for generated draft test cases.

Use this folder for local review before uploading anything to a test management system.

### `references/bootstrap-workflow.md`

Guidance for creating or refreshing reusable scope context.

Use this when bootstrapping a new product area or feature scope.

### `references/examples.md`

Examples of high-quality test cases and reusable patterns.

Keep examples generic if this repository is public or shared outside your organization.

### `references/page-analysis-rules.md`

Rules for analyzing live UI behavior and turning observed changes into test steps and expected results.

### `references/regression-rules.md`

Shared regression thinking and case composition rules.

Use this for smoke, regression, comprehensive, permission, and cross-surface coverage requests.

### `references/test-case-format.md`

The standard manual test case format used by this skill.

### `references/testomat.md`

Optional guidance for Testomat placement and upload workflows.

If your team does not use Testomat, adapt this file to your own test management system or remove it.

### `references/verification-modes.md`

Explains how to choose between:

- spec-based mode;
- code/PR-based mode;
- browser-verified mode;
- hybrid mode.

## Product scope context

Product or feature context lives under:

```text
references/scopes/
```

Each scope should start with two files:

```text
product-context.md
feature-map.md
```

Example:

```text
references/scopes/example-feature/
├── product-context.md
└── feature-map.md
```

## `product-context.md`

Use this file for stable shared context about a product area or feature scope.

Include:

- what the scope is;
- main purpose;
- shared terminology;
- supported roles or permission vocabulary;
- shared navigation patterns;
- connected surfaces;
- common states;
- common regression risks;
- assumptions and open questions.

Do not include sensitive company data, customer data, private URLs, real credentials, internal project IDs, or secrets.

## `feature-map.md`

Use this file as a lightweight map of features and flows inside the scope.

Include:

- features or sub-features;
- main flows;
- connected surfaces;
- permission-sensitive behavior;
- cross-surface checks;
- validation and sad paths;
- regression seams;
- open questions.

Keep this file short. It should be a map, not a detailed test plan.

## When to add feature-specific files

Do not create feature-specific files too early.

Start with:

```text
references/scopes/<scope-name>/product-context.md
references/scopes/<scope-name>/feature-map.md
```

Create a dedicated feature file only when the feature has enough unique reusable context, such as:

- unique user flows;
- unique permissions;
- unique connected surfaces;
- unique edge cases;
- complex regression risks;
- enough test coverage to justify separate context.

Example:

```text
references/scopes/example-feature/
├── product-context.md
├── feature-map.md
└── sub-feature.md
```

If a feature becomes large, use a folder:

```text
references/scopes/example-feature/
├── product-context.md
├── feature-map.md
└── sub-feature/
    ├── product-context.md
    └── feature-map.md
```

## Verification modes

### Spec-based mode

Use when the input comes from:

- requirements;
- acceptance criteria;
- product specs;
- docs;
- diagrams;
- tables;
- design notes.

Good for:

- draft test cases;
- coverage gaps;
- assumptions;
- open questions;
- risk analysis.

### Code/PR-based mode

Use when the input comes from:

- PR descriptions;
- changed files;
- routes;
- components;
- API contracts;
- implementation notes.

Good for:

- implementation-aware test ideas;
- QA review;
- regression risks;
- draft test cases;
- AC vs implementation gaps.

### Browser-verified mode

Use when QA has verified the flow in a real browser or app session.

Good for:

- exact UI copy;
- exact button and field names;
- modal behavior;
- toast messages;
- required and optional fields;
- visible side effects;
- cross-surface checks.

### Hybrid mode

Use when multiple sources are available:

- specs;
- code/PR context;
- browser observations;
- existing tests;
- known bugs.

This usually gives the strongest output.

## Core rules

- Do not invent product behavior.
- Use only confirmed context from specs, code, browser observations, docs, or QA notes.
- Mark assumptions and open questions clearly.
- Keep test cases practical and runnable.
- Prefer user-visible expected results.
- Avoid backend-only assertions unless the UI exposes the result.
- Avoid generic UI checks unless the user asks for them.
- Avoid duplicate coverage.
- Keep shared context in `product-context.md`.
- Keep feature lists and flow maps in `feature-map.md`.
- Add feature-specific files only when there is real context to maintain.

## Example prompt

```text
Use the test-case-drafting-template skill.

Mode: spec-based
Scope: <scope-name>
Feature: <feature-name>
Flow: <specific-flow>
Role: <user-role>

Context:
<paste requirement, notes, acceptance criteria, docs, or browser observations>

Task:
Draft one practical manual test case.

Rules:
- Do not invent behavior.
- Mark assumptions clearly.
- Keep the case runnable.
- Use the configured test case format.
- Include open questions if the context is incomplete.
- Do not upload to a test management system.
```

## Create or update reusable context

Use this workflow when setting up a new scope or refreshing an existing one.

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

## Adding a new scope

1. Create a folder under:

```text
references/scopes/
```

2. Use lowercase kebab-case.

Examples:

```text
billing/
people/
mobile/
admin-settings/
example-feature/
```

3. Add two starter files:

```text
product-context.md
feature-map.md
```

4. Keep the first version lightweight.

## Naming conventions

Use lowercase kebab-case for folders and files.

Good:

```text
example-feature
product-context.md
feature-map.md
admin-settings.md
```

Avoid:

```text
ExampleFeature
Product Context.md
featureMap.md
```

## Working with Git

### Clone the repository

Use this when you do not have the repository locally yet:

```bash
git clone <repo-url>
cd test-case-drafting-template
```

Example:

```bash
git clone https://github.com/<your-username-or-org>/test-case-drafting-template.git
cd test-case-drafting-template
```

### Pull the latest changes

Before making changes, always pull the latest version:

```bash
git checkout main
git pull origin main
```

### Create a branch

Use a branch for your changes:

```bash
git checkout -b update-test-case-drafting-template
```

For scope-specific changes, use a descriptive branch name:

```bash
git checkout -b add-example-feature-context
```

### Check what changed

```bash
git status
```

To inspect file differences:

```bash
git diff
```

### Commit changes

```bash
git add .
git commit -m "Update test case drafting template"
```

### Push changes

```bash
git push origin <branch-name>
```

Example:

```bash
git push origin update-test-case-drafting-template
```

### Open a pull request

After pushing your branch:

1. Open the repository in GitHub.
2. Click **Compare & pull request**.
3. Add a short description of what changed.
4. Request review from the relevant maintainer or QA owner.

### If you work directly on `main`

For small personal updates, you can commit directly to `main`:

```bash
git checkout main
git pull origin main
git add .
git commit -m "Update test case drafting template"
git push origin main
```

## Security and privacy

Do not commit:

- real API tokens;
- credentials;
- passwords;
- private URLs;
- customer data;
- internal project IDs;
- private staging links;
- sensitive screenshots;
- company-specific information that should not be public.

Use placeholders in public examples:

```text
<testomat-project-slug>
<testomat-suite-url>
<testomat-api-token>
<scope-name>
<feature-name>
<url-or-n/a>
```

Before publishing or sharing publicly, run a quick search:

```bash
grep -Rni "password\\|secret\\|api_key\\|token" . --exclude-dir=.git
grep -Rni "http://\\|https://" . --exclude-dir=.git
```

Review anything returned by the search and replace real values with placeholders.

## Maintenance rules

- Keep files small and useful.
- Do not add empty feature folders for future work.
- Do not duplicate shared context across many files.
- Remove outdated assumptions when behavior becomes confirmed.
- Keep examples generic if the repository is public.
- Keep organization-specific context in a private/internal fork or repo.

## Guiding principle

This skill should not replace QA thinking.

It should help package QA thinking into reusable context, so test case drafting becomes faster, more consistent, and more product-aware.
