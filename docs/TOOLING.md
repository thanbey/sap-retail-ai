# Tooling

CLIs used in this project, what each is for, and how it got here.

| CLI | Purpose | Install |
|---|---|---|
| cf | Cloud Foundry CLI: push the FastAPI/Streamlit apps to BTP CF, bind services | Homebrew (`cloudfoundry/tap/cf-cli`) |
| cds | SAP CAP CLI: run the S/4 mock in `mock-s4/` (`cds watch`) | `npm i -g @sap/cds-dk` (or via `make setup`) |
| btp | SAP BTP CLI: manage global account, subaccounts, entitlements, subscriptions (e.g. HANA Cloud) | Manual: darwin-arm64 tarball from https://tools.hana.ondemand.com/#cloud, binary in `/usr/local/bin/btp` |
| gh | GitHub CLI: create repos, auth, PRs | Homebrew |
| uv | Python env + lockfile manager for `service/` | Homebrew |

Login: `btp login --url https://cli.btp.cloud.sap` (browser SSO); `cf login -a <api endpoint>`; `gh auth login`.
