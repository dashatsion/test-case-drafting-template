# Context Bootstrap Workflow

Use this file only for `/context-bootstrap` or when the QA asks to refresh reusable skill context from the repository.

Bootstrap is a setup/update workflow. It is not daily test generation.

## Goal

Analyze the repository once, or after meaningful product changes, to maintain small reusable context files that QA can use without forcing the agent to rescan the whole repository on every run.

`/context-bootstrap` is the process.

`product-context.md` and `feature-map.md` are the outputs.

## What to update

### `product-context.md`

Keep it short and stable. Include only:

- What the product area or feature scope is.
- Main features in the scope.
- Supported roles and permission vocabulary.
- Valid environments, if relevant.
- Stable repository entry points for models, policies, routes, UI, and specs.
- High-level QA philosophy or constraints that apply to the whole scope.

Do not add detailed feature behavior, field lists, or every validation here.

### `feature-map.md`

Use this for feature relationships and regression seams. Include:

- Object relationships.
- Cross-feature links.
- Shared models or data surfaces.
- Permission shape that affects multiple features.
- High-risk regression seams.
- Feature-specific discovery depth when it is durable enough to reuse.

Do not copy full implementation details from code. Point to where current truth lives.

## Repository analysis scope

Read only the files needed to maintain the reusable context:

- Scope-related models.
- Scope-related policies or permission rules.
- Scope-related routes/controllers.
- Scope-related UI entry points.
- Current PRDs/specs if available.
- Existing QA/test management conventions if stored in the repository.

Avoid scanning unrelated product areas unless the QA explicitly wants to clone this skill for another scope.

## Bootstrap output rules

- Do not generate test cases.
- Do not upload to a test management system.
- Do not create a giant coverage map.
- Keep context concise enough to be read often.
- Prefer stable statements over fragile snapshots.
- When unsure, write a short note like `Needs confirmation from current code` instead of guessing.

## Suggested prompt

```text
/context-bootstrap

Refresh reusable context for the <scope-name> test case drafting skill.
Update product-context.md and feature-map.md only.
Do not generate test cases.
Keep the files concise and reusable for the QA team.