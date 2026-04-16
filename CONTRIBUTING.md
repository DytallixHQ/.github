# Contributing to DytallixHQ Repositories

This repository provides the default contribution guidance for public
DytallixHQ projects.

## Before You Open A PR

- Read the target repository README and any repo-specific contributing notes.
- Open an issue first for behavior changes, new features, or large refactors.
- Keep changes small and scoped to one problem.
- Do not claim production readiness that the current public deployment does not
  actually have.

## Reporting Problems

- Bugs, docs gaps, and reproducible behavior mismatches: open a public issue.
- Security vulnerabilities: follow [SECURITY.md](SECURITY.md).
- General usage questions: follow [SUPPORT.md](SUPPORT.md).

## Pull Request Expectations

- Explain what changed and why.
- Include the smallest validation that demonstrates the change is correct.
- Update docs when public behavior, commands, or supported surfaces change.
- Avoid unrelated cleanup in the same PR.

## Repository Truthfulness

Several DytallixHQ repositories document hosted runtime surfaces. If a repo is
docs-only, say so plainly. If a feature is incomplete, say so plainly. Public
repos should reduce ambiguity, not introduce it.