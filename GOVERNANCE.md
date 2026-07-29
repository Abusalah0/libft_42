# Governance

## Project model

libft currently uses a Benevolent Dictator for Life (BDFL) governance model.

The project maintainer and BDFL is [@abusalah0](https://github.com/abusalah0).

The project maintainer has final responsibility for:

- the project direction,
- public API decisions,
- release decisions,
- accepting or rejecting contributions,
- and resolving disagreements.

## Proposing changes

Contributors can propose changes through GitHub issues and pull requests.

Open an issue before starting work on changes that:

- add or remove public functions,
- change existing behavior,
- introduce new dependencies or tooling,
- affect compatibility,
- or significantly change the project structure.

Small bug fixes, tests, and documentation improvements may be submitted directly as pull requests.

## Decision process

Technical decisions are based on:

- correctness,
- memory safety,
- compatibility with the existing API,
- usefulness to the project’s users,
- and consistency with the project’s scope.

Discussion is encouraged, but consensus is not required. The maintainer makes the final decision after considering the available evidence and contributor feedback.

A contribution may be declined even when it works correctly if it expands the project beyond its intended scope or introduces unnecessary maintenance cost.

## Reviews and merging

The maintainer reviews pull requests before merging them.

Contributors may be asked to:

- clarify the motivation,
- reduce the scope,
- add tests,
- update documentation,
- or revise the implementation.

Only the maintainer may merge changes into the default branch.

## Releases

The maintainer decides when a release is ready and assigns its version according to Semantic Versioning.

Release decisions consider:

- completed fixes and features,
- compatibility,
- test results,
- documentation status,
- and known unresolved issues.

Each release should have a corresponding Git tag and changelog entry.

## Conduct and security

All project participation must follow [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md).

Security vulnerabilities must be reported through the process described in [`SECURITY.md`](SECURITY.md), not through public issues.

## Future changes to governance

This governance model may change if the contributor community grows.

Possible future changes include:

- granting review or merge rights to regular contributors,
- defining maintainership areas,
- or adopting a small maintainer committee.

Any governance change will be documented in this file and discussed publicly before adoption.
