# Workshop FAQ

## How do I see all the branches?

Run `git fetch origin`, then `git branch -a`. Remote branches are listed under
`remotes/origin/`. Inspect the history with `git log --graph --oneline --all --decorate`.

## How do I work on a remote branch locally?

In a fresh clone, use `git switch --track origin/cytang/evening-hours`.
If you already have that local branch, use `git switch cytang/evening-hours`.
To experiment without changing the shared branch, create your own branch from it:
`git switch -c your-name/hours-practice origin/cytang/evening-hours`.

## How do I back out of a practice conflict?

Use `git merge --abort` during a merge or `git rebase --abort` during a rebase.
Run `git status` to see which operation is in progress before choosing a command.

## Why does the decaf pull request have a conflict?

The decaf and seasonal-menu branches added drinks at the same location.
The seasonal branch is already merged; keep both drinks when resolving the decaf branch.
