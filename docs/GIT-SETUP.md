# Git setup

| Repo | GitHub | Remote |
|---|---|---|
| ~/Dev/projects/sap-retail-ai | thanbey/sap-retail-ai | HTTPS (gh) |
| ~/Dev/projects/blog | thanbey/thanbey.github.io | SSH |

- Blog repo must be named `thanbey.github.io` for a root Pages site. Deploys via Actions on push.
- Project repo created with `gh repo create sap-retail-ai --public --source=. --push`.
- `git push` cannot create a repo; "Repository not found" = repo missing, not a key issue.
- Remote switched to HTTPS: `git remote set-url origin https://github.com/thanbey/sap-retail-ai.git`.

## Conventions
- `main` only. Commit per deliverable, message `dayN: summary`. Push daily.
- Never commit `.env`; `.env.example` documents variables.
- Cowork commits locally; you push from Terminal.

## Daily
```
git status -sb
git add -A && git commit -m "dayN: summary"
git push
```
