# Copilot instructions

These notes are for agents new to this repository. Trust this file and only search further if details here are missing or wrong.

## Repository summary
- This repository is a curated collection of reusable GitHub Actions that are commonly used across our projects.
- Its purpose is to centralise these actions so they can be **controlled for security** (vetted, pinned, audited) and **standardised** (consistent inputs, outputs, and behaviour) across all consuming workflows.
- Consumers reference these actions instead of pulling third-party actions directly, giving us a single point of review and upgrade.
- Actions live under `.github/actions/`, grouped by domain (e.g. `artifact/`, `aws/`, `docker/`, `pull-request/`, `release/`, `version/`).
- Documentation for each action lives alongside it in a `README.md` file.

## Security and standardisation rules
- **Always pin third-party actions to a full-length commit SHA, not a tag or branch.** Tags and branches are mutable and a security risk; commit hashes are immutable.
  - Correct: `uses: owner/repo@<40-char-commit-sha>`
  - Incorrect: `uses: owner/repo@v1`, `uses: owner/repo@main`
- This rule applies to any `uses:` reference inside `action.yml` files, composite action steps, and workflows under `.github/workflows/`.
- First-party references within this repository (one action calling another in this repo) may use a relative path (`./.github/actions/...`) instead of a SHA.
- When adding or updating an action, prefer minimal, well-scoped permissions and explicit inputs/outputs over implicit behaviour.

## Stack and runtime versions
- Actions are expected to run in GitHub Actions runners.
- Each action's runtime, inputs, and outputs are defined in its own `action.yml` and README.
- Do not assume a single language/runtime for the repo; check each action folder first.

## Setup and bootstrap (not executed here)
- No global project setup is required for the repo itself.
- If an action includes a script or tooling dependency, follow the action-specific README.

## Run and entry points (not executed here)
- The entry point for an action is defined in its `action.yml` (e.g., `runs.using`, `runs.steps`).
- Local runs are not standardized; use the per-action README for usage examples.

## Testing (not executed here)
- No shared test harness is defined at the repo root.
- If an action has tests, they should be documented within that action's folder.

## Project layout and key files
- `.github/actions/`: action implementations, grouped by category.
- `.github/workflows/`: CI workflows for this repo.
- `.github/CODEOWNERS`: review ownership for changes.
- `README.md`: index of available actions and links to their docs.

## Known gaps
- If an action directory lacks a `README.md` or `action.yml`, treat it as incomplete and ask before editing.
- If you encounter a `uses:` reference pinned to a tag or branch instead of a commit SHA, flag it as a security issue and propose pinning to a SHA.
