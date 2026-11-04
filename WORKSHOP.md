# Git practice guide

Work in your own clone and branch. Use `git status` whenever you are unsure.
If you do not have push access, fork the repository and use your fork as `origin`.

## 1. Explore history

Run `git log --oneline --graph --all` and `git log -- menu.html`.
Find the cold brew currency fix. Use `git show <commit>` to inspect it, then
`git blame menu.html` to see which commits last touched the menu lines.
Replace angle-bracket placeholders with real commit IDs; do not type the brackets.

## 2. Open a pull request

Follow [CONTRIBUTING.md](CONTRIBUTING.md). Add a snack on your own branch,
commit it, push it, and ask a partner to review your pull request.

## 3. Clean up a branch with an interactive rebase

On a new practice branch, make three small commits to the café story.
Run `git rebase -i HEAD~3` and squash two of them. Compare the history before
and after. If you already pushed this personal branch, coordinate with anyone
using it and update it with `git push --force-with-lease`.

## 4. Resolve a conflict

Create two local branches from the same commit. On each branch, change the
same opening-hours line in `index.html` to different values and commit it.
Merge one branch into the other, choose the final hours, remove conflict
markers, stage the file, and finish the merge. Use `git merge --abort` if you
want to return to the state before the merge and try again.

## 5. Cherry-pick one useful change

Create a local branch from the commit immediately before the currency fix
(use `git switch -c your-name/currency-practice <fix-commit>^`). Then run
`git cherry-pick <fix-commit>` and inspect the new commit with `git show`.
Return to your original branch when finished.

## 6. Undo a change without rewriting history

On a practice branch, change the café tagline and commit it. Run
`git revert <tagline-commit>` and inspect the new commit. Compare that with
what an interactive rebase does to history.

## 7. Stash work in progress

Edit a sentence without committing it. Run `git stash push -m "café copy draft"`,
check `git status`, and restore it with `git stash pop`.

## Facilitator notes

The café and events are fictional. All seed commits were created for this
workshop; the history is intentionally a sequence of small, readable changes.
Have pairs edit the same menu or opening-hours line for repeatable conflicts.
Participants should practice history rewriting on their own branches.
