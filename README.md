# Commit Café

A fictional neighborhood café website for the Hack@Brown Git workshop.
The files and commit history are practice material: explore, change things,
and learn how to recover when a Git command surprises you.

## Run locally

Open `index.html` directly in a browser, or serve this folder with Python 3:

```sh
python3 -m http.server 8000
```

Then visit <http://localhost:8000>. There are no dependencies or build tools.

## Start practicing

- [Workshop exercises](WORKSHOP.md): inspect history, rebase, resolve conflicts,
  cherry-pick, revert, and stash.
- [Contribution guide](CONTRIBUTING.md): make a branch and open a pull request.

## Project files

| File | Purpose |
| --- | --- |
| `index.html` | Welcome, location, and opening hours |
| `menu.html` | Drinks, pastries, and prices |
| `about.html` | The café story |
| `events.html` | Fictional community events |
| `styles.css` | Shared styles and responsive layout |

## Check your changes

Open all four pages, follow the navigation links, try a narrow browser window,
and use Tab to check keyboard navigation. Use `git diff --check` before committing.

The café is fictional, and this commit history was created as workshop material.
