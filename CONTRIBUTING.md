# Contributing to BrewCart

## Golden rules
1. Nobody pushes to `main`. Every change goes through a pull request.
2. A pull request needs a **green `syntax` check** before it can merge. Required approvals: **0** while this is a one-person repo, raised to **1** when a second reviewer joins.
3. Never commit passwords, tokens or keys. The pre-commit hook will block them.
4. Keep pull requests small: one change, one reason.
5. Delete your branch after it is merged.

## One-time setup after cloning
```bash
python3 -m pip install --user pre-commit
pre-commit install
```
The hook runs on every commit. It fixes whitespace and end-of-file issues, validates YAML,
and blocks private keys, tokens and passwords. Run `pre-commit run --all-files` to check everything.

## Branch names
Format: `type/short-description` (lowercase, words joined with hyphens)

| Type | Use it for | Example |
|---|---|---|
| `feature/` | something new | `feature/add-cold-brew` |
| `fix/` | a bug fix | `fix/menu-price-typo` |
| `docs/` | documentation only | `docs/contributing` |
| `chore/` | tooling, config, housekeeping | `chore/pre-commit-hooks` |
| `hotfix/` | urgent fix for production | `hotfix/revert-bad-port` |

## Commit messages: Conventional Commits
Format: `type(scope): short summary in present tense`

| Type | Meaning |
|---|---|
| `feat` | a new feature |
| `fix` | a bug fix |
| `docs` | documentation only |
| `chore` | maintenance, no app change |
| `refactor` | code change that adds no feature and fixes no bug |
| `test` | adding or fixing tests |
| `ci` | pipeline or workflow changes |
| `revert` | undoing an earlier commit |

Examples:
- `feat(api): add Cold Brew to the menu`
- `fix(frontend): show 502 page when the API is down`
- `docs: add contributing guide`

## Pull request flow
1. `git switch main && git pull`
2. `git switch -c type/short-description`
3. Commit using Conventional Commits, then `git push -u origin <branch>`
4. Open a pull request and fill in the template
5. Wait for the green check (and the required approvals), then merge
6. `git switch main && git pull && git branch -d <branch>`

## Releases
We use Semantic Versioning tags: `vMAJOR.MINOR.PATCH` (for example `v1.0.0`).
- MAJOR: breaking change
- MINOR: new feature, nothing broken
- PATCH: bug fix only
