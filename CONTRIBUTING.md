# Boiko-School code rules

In short: code lives in the organization, reaches `master` only through a squash-merged PR, and git never holds secrets or children's data. Everything else is common sense.

## Repositories

- All code in the organization's repositories belongs to Boiko-School, regardless of who wrote it, when or how: an employee, a contractor, an AI agent, or code moved in from a personal account, Bitbucket or anywhere else. By putting code into the organization, the author hands it over to the organization. For employees and contractors this is also stated in their contracts.
- All working code lives in the [Boiko-School](https://github.com/Boiko-School) organization. Not in personal accounts, not on Bitbucket, not in a local folder without a remote.
- All repositories are private. Only things that are public anyway can be public: a GitHub Pages site and the like. Only an admin creates a public repository.
- The default branch is `master`.
- A new repository is created for a task the tech lead knows about. Experimenting is fine, but an experiment that becomes real moves into the organization, and an abandoned one gets archived.
- Names are in Latin letters, kebab-case, and say what the thing is: `music-school`, not `x-meal-4-final`.
- Abandoned projects are archived, not deleted.
- Every repository has a README: what it is, how to run it, where it runs (prod, dev) and who owns it.

## Branches and pull requests

- No direct pushes to `master`. Every change goes through a branch and a PR.
- Squash merge only. The PR title becomes the commit on `master`, so write it like a human, saying what and why: `Billing: transfer balance between contracts`. Not `S44`, not `32`, not `slop2`.
- Branch names: anything meaningful, e.g. `fix/portmone-webhook`, `meal-orders-ui`.
- Branches are deleted automatically after merge.
- A second-person review is required when the code touches money, children's data, authentication or access rights. Anything else you can merge yourself once CI is green.
- Keep PRs small. Big refactorings go in parts.
- Force-pushing your own branch is fine; force-pushing `master` is not.
- An admin may bypass protection in an emergency; GitHub logs it, and afterwards we explain what happened in the PR or in chat.

## Secrets

- No passwords, tokens, keys, certificates or `.env` files in the repository. Not in a private one, not "temporarily", not in a README, not in examples.
- Production secrets live in GCP Secret Manager. Locally, use a `.env` that is in `.gitignore`. The repository only holds a `.env.example` with empty values.
- A secret that got into git is compromised. Rotate it first, then clean the history. Deleting the commit does not save it.
- Default passwords like `admin/admin` are only acceptable with a forced change on first login.
- Checks: [gitleaks](https://github.com/gitleaks/gitleaks) in pre-commit and in CI.

## Personal data

- Personal data of children, parents and staff never goes into a repository: no dumps, no exports, no screenshots, no "test" data taken from production. Test data is made up.
- Production database dumps are not kept on laptops. If you need one for debugging, take an anonymized one and delete it afterwards.

## AI agents

- Claude, Copilot and other agents follow the same rules: a branch, a PR, a meaningful title, human review where review is required.
- Agents never get production secrets.
- `CLAUDE.md` and `AGENTS.md` in a repository are fine.

## Minimum for every repository

- A README.
- A `.gitignore` that includes `.env`.
- A `.env.example` if there are settings.
- CI: build, tests, gitleaks.

## What we don't require

Conventional commits, two approvals, CODEOWNERS, signed commits, issue templates, GitFlow with a `develop` branch, a test coverage percentage. We'll add any of these if we ever need them.
