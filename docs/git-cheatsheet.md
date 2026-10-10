# Git cheat sheet: commands used in Project 02

Every command below was used in this project. Grouped by the job it does.

## Start of every task

| Command | What it does |
|---|---|
| `git switch main` | Go to the main branch |
| `git pull` | Bring in everything merged on GitHub since you last looked |
| `git switch -c feature/short-name` | Create a new branch from here and switch to it |

Always branch from an up-to-date `main`.

## Saving work

| Command | What it does |
|---|---|
| `git status` | What changed, what is staged, which branch you are on |
| `git diff` | The exact lines changed (`+` added, `-` removed) |
| `git add <file>` | Stage one file for the next commit |
| `git add -A` | Stage everything, including new and deleted files |
| `git commit -m "type(scope): summary"` | Save a snapshot with a Conventional Commits message |
| `git commit -am "..."` | Stage already-tracked files and commit in one step |
| `git commit --amend -m "..."` | Replace the last commit (only if not pushed yet) |
| `git commit -a --amend --no-edit` | Fold a fix into the last commit, keep its message |

## Sharing work

| Command | What it does |
|---|---|
| `git push -u origin <branch>` | First push of a branch; `-u` remembers the link |
| `git push` | Later pushes of the same branch |
| `git fetch origin` | Download the latest from GitHub without changing your files |
| `git fetch --prune` | Also forget branches deleted on GitHub |

## Looking at history

| Command | What it does |
|---|---|
| `git log --oneline -5` | Last 5 commits, one line each |
| `git log --oneline --graph` | History drawn as a graph: branches and merges |
| `git log --oneline --decorate -3` | Shows branch and tag labels next to commits |
| `git log -1 --format=%B` | Full message of the latest commit |
| `git show HEAD --stat` | Latest commit and the files it touched |

## Merge conflicts

| Command | What it does |
|---|---|
| `git merge origin/main` | Bring the latest main into your branch; conflicts appear here |
| *(edit the file)* | Keep the right version, delete `<<<<<<<`, `=======`, `>>>>>>>` |
| `git add <file>` | Mark the conflict as resolved |
| `git commit -m "..."` | Finish the merge |
| `git merge --abort` | Give up and go back to before the merge |

## Undoing things

| Situation | Command |
|---|---|
| Commit is **pushed and shared** | `git revert --no-edit <hash>` (adds an undo commit) |
| Commit is **local only** | `git reset --hard origin/main` (throws local commits away) |
| Unsaved edits in one file | `git restore <file>` |
| File staged by mistake | `git restore --staged <file>` |
| A rebase went wrong | `git rebase --abort` |

## Rewriting your own unpushed commits

| Command | What it does |
|---|---|
| `git rebase -i HEAD~3` | Edit the last 3 commits; first line `pick`, the rest `squash` to combine them |
| `git config --global core.editor "code --wait"` | Use VS Code instead of Vim for commit and rebase messages |

Never rebase or amend commits other people already have.

## Moving work around

| Command | What it does |
|---|---|
| `git stash` | Put uncommitted changes on a shelf; working tree becomes clean |
| `git stash list` | See what is on the shelf |
| `git stash pop` | Take the latest changes back off the shelf |
| `git cherry-pick <hash>` | Copy one commit onto the current branch |

## Cleaning up branches

| Command | What it does |
|---|---|
| `git branch -a` | All branches, local and remote |
| `git branch -d <branch>` | Delete a merged branch (refuses if unmerged) |
| `git branch -D <branch>` | Force-delete, for branches you mean to throw away |

## Releases

| Command | What it does |
|---|---|
| `git tag -a v1.0.0 -m "..."` | Annotated tag: who, when, message |
| `git show v1.0.0 --stat` | Inspect the tag and the commit it points to |
| `git push origin v1.0.0` | Tags are not pushed by `git push`; send them on purpose |

## Pre-commit

| Command | What it does |
|---|---|
| `python3 -m pip install --user pre-commit` | Install the tool |
| `pre-commit install` | Put the hook in `.git/hooks/` (once per clone) |
| `pre-commit autoupdate` | Bump hook versions in `.pre-commit-config.yaml` |
| `pre-commit run --all-files` | Run every hook on every file now |

If a hook says **"files were modified by this hook"**, it already fixed the file: `git add` it again and re-commit. If **detect-secrets** fails, remove the secret; never bypass it.

## Credentials (HTTPS)

| Command | What it does |
|---|---|
| `printf "protocol=https\nhost=github.com\n\n" \| git credential reject` | Remove the saved GitHub login from the Keychain |
| `git ls-remote origin` | Check that authentication works |

GitHub does not accept account passwords for Git. Use a personal access token and keep it only in the credential store.
