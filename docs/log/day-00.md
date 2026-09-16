# Day 0: accounts, tooling, repos

Deliverable: BTP trial live, CLIs installed, both repos on GitHub, Day 0 post published.

- 10:30  BTP trial created. Region US East (VA) - AWS. Global account 2aa19bf4trial, subaccount trial, CF org 2aa19bf4trial, space dev. Cockpit: https://account.hanatrial.ondemand.com. (record in 1Password: SAP BTP Trial)
- 11:05  sap-retail-ai pushed to GitHub: https://github.com/thanbey/sap-retail-ai
- 11:05  Lesson: `git push` cannot create a remote repo; "Repository not found" over SSH meant the repo did not exist yet, not a key problem. `gh repo create <name> --public --source=. --push` creates it from the CLI. gh already installed (2.101.0); gh auth login set git protocol to HTTPS.
- 11:05  Remote switched from SSH to HTTPS (git remote set-url origin https://github.com/thanbey/sap-retail-ai.git); gh manages the credential. Blog repo still on SSH and works.
