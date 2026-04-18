# Contributing to A2A-SIN-Zoom

## Scope first

Before changing code or docs, verify the change genuinely belongs to the **Zoom** surface.

Put the change here when it affects:
- Zoom meeting, chat, or session workflows
- Zoom evidence, recovery, auth, or recording/session handling
- Zoom contracts tied to meeting coordination and session automation

Do **not** put the change here when it belongs to:
- generic messaging ownership outside Zoom
- unrelated social, meeting, or chat platform behavior
- organization SSOT docs or architecture ownership

## Workflow

1. Branch from the latest `main`.
2. Make the smallest repo-scoped change possible.
3. Run validation command(s) relevant to the touched surface.
4. Include exact validation commands and evidence in the PR.

## Boundary checklist

- Does this change stay within Zoom ownership?
- Does another repo already own the adjacent platform behavior?
- Does this PR avoid redefining shared docs, runtime, or platform canon?

## License

By contributing, you agree that your contributions will be licensed under the Apache License 2.0.
