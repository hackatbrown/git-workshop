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

## Explore the prepared branch graph

Fetch all the workshop branches and show their history:

```sh
git fetch origin
git log --graph --oneline --all --decorate
```

Use `--all` to include the unmerged practice branches. In the original batch, two sample PRs were
merged using merge commits and four were left open for exercises.

| Branch | PR | Exercise |
| --- | --- | --- |
| `cytang/seasonal-menu` | [#1](https://github.com/hackatbrown/git-workshop/pull/1) | Inspect a merged three-commit feature |
| `cytang/community-events` | [#2](https://github.com/hackatbrown/git-workshop/pull/2) | Compare independent branches merged into main |
| `cytang/decaf-menu` | [#3](https://github.com/hackatbrown/git-workshop/pull/3) | Resolve the intentional menu conflict, keeping both new drinks |
| `cytang/evening-hours` | [#4](https://github.com/hackatbrown/git-workshop/pull/4) | Review changes and squash two commits on a personal branch |
| `cytang/autumn-palette` | [#5](https://github.com/hackatbrown/git-workshop/pull/5) | Rebase an older branch and review print styles |
| `cytang/workshop-faq` | [#6](https://github.com/hackatbrown/git-workshop/pull/6) | Practice a documentation review |

Create a personal branch from a remote practice branch before experimenting:

```sh
git switch -c your-name/decaf-practice origin/cytang/decaf-menu
git rebase origin/main
```

For the decaf conflict, edit `menu.html` to keep both seasonal and decaf items,
remove the conflict markers, run `git add menu.html`, then `git rebase --continue`.
`git rebase --abort` returns you to the state before the rebase.

## Compare merge strategies and stacked work

A second batch adds completed examples of squash merges, rebase merges, and
nested merges. Source branches are retained, including the pre-rebase takeaway
branch. Fetch before exploring:

```sh
git fetch origin
git log --graph --oneline --all --decorate
```

| PR | History example | What to inspect |
| --- | --- | --- |
| [#7](https://github.com/hackatbrown/git-workshop/pull/7) | Squash merge | Three bakery edits become one commit on main |
| [#8](https://github.com/hackatbrown/git-workshop/pull/8) | Squash merge | Three welcome revisions become one commit on main |
| [#9](https://github.com/hackatbrown/git-workshop/pull/9) | Branch rebase, then rebase merge | Compare the preserved before-rebase branch, rewritten branch, and main |
| [#10](https://github.com/hackatbrown/git-workshop/pull/10) | Rebase merge | Original visitor-guide commits have new copies on main |
| [#11](https://github.com/hackatbrown/git-workshop/pull/11) | Stack parent, merged | The group-visit commits are shared by main and the child branch |
| [#12](https://github.com/hackatbrown/git-workshop/pull/12) | Stack child, open | Originally based on the parent branch; now targets main with two checklist commits |
| [#13](https://github.com/hackatbrown/git-workshop/pull/13) | Nested merge | The feature branch merged main before its own PR merge |

### Compare a rebase with range-diff

This command compares the takeaway patches before and after rebasing. An equals
sign means the patch stayed the same even though its commit ID changed.

```sh
git range-diff 1c7f368..origin/cytang/rebase-takeaway-before f26d392..origin/cytang/rebase-takeaway
```

### Distinguish a squash from a merge

Inspect `git log --oneline origin/cytang/squash-snacks` and compare the source
commits with the single commit linked from PR #7. The original source commits
are not ancestors of main even though their final changes are present there.
A rebase merge similarly leaves original commit IDs off main, but preserves a
separate replacement commit for each patch rather than collapsing them.

### Follow a merge inside a merge

Find the merge for PR #13 in the graph. Follow its feature-side parent until you
reach `Merge main into volunteer board to pick up café updates`. That inner
commit has two parents too. Compare `git log --first-parent main` with the full
graph to see how first-parent history hides the feature branch's internal work.

### Inspect the remaining stack child

PR #12 is open. Its parent PR #11 is already merged. Compare the original stack
with `git log --graph --oneline origin/cytang/group-visits origin/cytang/group-checklist`
and inspect its current diff with `git diff origin/main...origin/cytang/group-checklist`.
