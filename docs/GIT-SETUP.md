# Git and GitHub setup

What was done, why, and the commands used. Two repos, one GitHub user (thanbey).

## Repos

| Repo | Local | GitHub | Purpose |
|---|---|---|---|
| sap-retail-ai | ~/Dev/projects/sap-retail-ai | github.com/thanbey/sap-retail-ai | The product: code, docs, logs |
| blog | ~/Dev/projects/blog | github.com/thanbey/thanbey.github.io | Build log site, served at thanbey.github.io |

The blog repo is named `thanbey.github.io` because GitHub serves a user's root
Pages site only from a repo with that exact name.

## What we did

**Initialised locally first.** `git init`, first commits, before any remote
existed. Commit messages name the work-plan day: `day0: ...`, `day1: ...`.

**Created the blog repo on the web, pushed over SSH.** New repo on github.com,
empty (no README, .gitignore or license, since the project already had them),
then `git remote add origin git@github.com:thanbey/thanbey.github.io.git`,
`git branch -M main`, `git push -u origin main`. Pages source set to
"GitHub Actions" in repo Settings; `.github/workflows/deploy.yml` builds and
deploys on every push to `main`.

**Created the project repo from the CLI.** `git push` cannot create a remote
repo; "Repository not found" over SSH meant the repo did not exist yet. Used
the GitHub CLI instead:

```
gh auth login                                    # once; browser login
gh repo create sap-retail-ai --public --source=. --push
```

`gh` reported "Unable to add remote origin" because `origin` was already set;
harmless. A plain `git push -u origin main` then worked.

**Switched the project remote to HTTPS.** `gh auth login` set the git
protocol to HTTPS and registered itself as the credential helper, so:

```
git remote set-url origin https://github.com/thanbey/sap-retail-ai.git
```

The blog stays on SSH; both work. HTTPS plus `gh` avoids SSH key management
on a new machine.

## Conventions

- Branch: `main` only for now. Feature branches when something is risky.
- Commit at least once per deliverable; message prefix is the day, e.g.
  `day3: synthetic AIF error generator`.
- `.gitignore` excludes `.env`, `.venv/`, `node_modules/`, `data/out/`,
  caches and `*.db`. Never commit secrets; `.env.example` documents variables.
- Push at the end of every day. Claude (Cowork) can commit locally but cannot
  push; the credential is in the Mac keychain.

## Daily commands

```
git status -sb                  # what changed, and ahead/behind
git add -A && git commit -m "dayN: <summary>"
git push
git log --oneline --since='1 day ago' --stat   # for the blog post
```

## If something goes wrong

- "Repository not found": the repo does not exist or the remote URL is wrong.
  `git remote -v` to check; `gh repo view` to confirm it exists.
- "could not read Username for https://github.com": credential helper not
  available in this shell; run the push from Terminal on the Mac.
- Stale `.git/*.lock` after an interrupted command: delete the lock file, then
  `git fsck` to confirm the repo is healthy.
- Pushed a secret by mistake: rotate it first, then rewrite history.
