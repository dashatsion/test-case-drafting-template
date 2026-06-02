# Testomat Placement & Upload

Default behavior is **draft-only**: produce reviewed cases for a human to approve. Only create or upload to Testomat when the QA explicitly asks, for example:

- "create and upload"
- "push these to Testomat"
- "upload these cases"

"Testomat-ready" means the case is formatted for Testomat. It does **not** mean upload automatically.

## Project

Use only the configured Testomat project for your team.

Example:

- Project: `<testomat-project-slug>`
- URL: `https://app.testomat.io/projects/<testomat-project-slug>/`

Before any upload, verify that the active project matches the configured target project.

If the active project is different, stop and tell the QA:

> Active Testomat project does not match the configured target project. Please switch to the correct Testomat project or provide the correct target suite URL.

Never upload generated QA cases into an unknown or unintended Testomat project.

## Where generated cases should be uploaded

Generated cases should be uploaded only to the target suite confirmed by the QA or by the configured workflow.

Default preference:

- Reuse an existing relevant suite whenever possible.
- Prefer a feature-specific suite if one exists.
- If the QA provides a target suite URL, use that exact suite.
- If no clear suite exists, ask the QA for the target suite instead of creating a new structure.

Do not assume that a specific parent folder such as `Draft`, `Generated test cases`, or `<Feature>` always exists.

If your team uses a dedicated draft area, configure that convention in your own private/internal version of this file.

## Suite hygiene

- Tests must live in a **`file`** suite, never a `folder` suite.
- Reuse an existing relevant suite whenever possible.
- Prefer a feature-specific suite if one already exists.
- If the QA provides a suite URL, use that exact suite.
- If multiple matching suites exist, ask the QA which one to use.
- If no suitable suite exists, ask before creating a new structure.
- Do not auto-create near-duplicate suites with slightly different names.
- Do not upload outside the confirmed target area unless explicitly requested.

## Upload discipline

- Upload only reviewed or approved cases, unless the QA explicitly said to create and upload in one step.
- Process large uploads in batches of **3-5**.
- Read back created tests or report Testomat IDs only when:
  - the QA asks for confirmation;
  - validation is required;
  - the upload result is uncertain;
  - Testomat returns ambiguous data.
- After a successful upload, respond only with:

`Done`

## Setup check before any Testomat read/write

Confirm Testomat access is configured before doing any read or write workflow.

Look for one of these:

- available Testomat MCP tools;
- an MCP config entry for Testomat;
- a configured Testomat API token available through the user's local environment or tool setup.

Do not ask the user to paste private tokens into chat.

Do not attempt writes without confirmed access.

If setup is missing, tell the QA that Testomat access is required before uploading or reading suites, and ask them to configure the required MCP/API access.

Use placeholders only in documentation examples. Never commit real API tokens, project tokens, credentials, private URLs, or customer data to the skill repository.

## Local staging -> edit -> push workflow

QAs should review and edit cases as files before anything reaches Testomat.

Recommended workflow:

1. Generate the case locally.
2. Save it as a Markdown file.
3. Let the QA review and edit it in their editor.
4. Upload only after the QA explicitly asks.

## Where to save generated cases

Write generated cases inside the active skill directory:

```text
generated-test-cases/<scope-or-feature>/
```

Use one file per run:

```text
generated-test-cases/<scope-or-feature>/<YYYY-MM-DD>-<short-slug>.md
```

Do not use the repository root as the default output location unless the user explicitly asks.

## File contents

Generated cases must follow the exact format from:

```text
references/test-case-format.md
```

If a file contains multiple cases, separate each case with a line containing only:

```text
---
```

This allows the upload workflow to split the file into individual Testomat tests.

Keep `[to verify in UI]` or similar review markers if some UI states were not observed live. Warn before upload if a case still contains verification markers, but do not block unless the QA asks you to.

## Edit rules

The QA may open generated files in their editor and change them freely.

Do not re-touch generated files unless explicitly asked.

If the QA edits a generated case, treat the edited file as the source of truth for upload.

## Push rules

Only push when the QA explicitly asks.

Examples:

- "push to Testomat"
- "upload these cases"
- "create these tests in Testomat"

Before uploading:

1. Confirm Testomat access.
2. Confirm the active project matches the configured target project.
3. Determine the correct target suite:
   - If the QA provided a suite URL, use it.
   - Else search for a relevant existing suite if tools are available.
   - Reuse an existing feature-specific suite whenever possible.
   - If the destination is unclear, ask the QA before uploading.
4. Read the staged file or files.
5. Split multiple cases on `---` if needed.
6. Warn if a case still contains `[to verify in UI]` or another verification marker.
7. Upload in batches of 3-5 when the list is large.
8. Report only:

`Done`

If the tool reports a different active project:

- do not try alternative projects blindly;
- stop and ask the QA to switch/select the correct Testomat project or provide the exact suite URL.

## Safe placeholder examples

Use placeholders like these in public or shareable documentation:

```text
<testomat-project-slug>
<testomat-suite-url>
<testomat-api-token>
<scope-name>
<feature-name>
```

Do not include real values from your company, customer accounts, private projects, staging environments, or internal tools.