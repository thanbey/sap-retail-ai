# Git setup

| Repo | GitHub | Remote |
|---|---|---|
| ~/Dev/projects/sap-retail-ai | thanbey/sap-retail-ai | HTTPS (gh) |
| ~/Dev/projects/blog | thanbey/thanbey.github.io | SSH |

Blog repo must be named `thanbey.github.io` for a root Pages site; it deploys via Actions on push.

## Commands we ran

```
git init                                   # start a repo in the folder
git add -A && git commit -m "day0: ..."    # stage everything, snapshot it
git branch -M main                         # rename default branch to main
git remote add origin git@github.com:thanbey/thanbey.github.io.git   # link local repo to GitHub (SSH)
git push -u origin main                    # first push; -u makes later pushes just `git push`
git remote -v                              # show the remote URL
gh auth login                              # log the GitHub CLI in (browser); sets HTTPS + credential helper
gh repo create sap-retail-ai --public --source=. --push   # create the GitHub repo from this folder and push
git remote set-url origin https://github.com/thanbey/sap-retail-ai.git   # switch remote from SSH to HTTPS
git status -sb                             # changed files, plus ahead/behind origin
git log --oneline                          # commit history, one line each
```

Notes
- `git push` cannot create a repo. "Repository not found" meant it did not exist yet.
- `gh repo create` said "Unable to add remote origin" because origin already existed; harmless.

## Conventions
- `main` only. Commit per deliverable, message `dayN: summary`. Push daily.
- Never commit `.env`; `.env.example` documents variables.
- Cowork commits locally; you push from Terminal.
