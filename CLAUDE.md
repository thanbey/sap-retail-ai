# sap-retail-ai

Prototype of an AI service layer on SAP BTP for Strategic Retail use cases:
Sentinel AI (AIF interface error monitoring and remediation), a Physical
Inventory Reconciliation (PIR) insights dashboard, and S/4 Retail POS-to-FI
financial reconciliation. Built as a two-week portfolio project; see
`docs/solution-plan.md` (architecture) and `docs/work-plan.md` (day-by-day).

## Ground rules
- Read `docs/work-plan.md` and `docs/DECISIONS.md` before starting a day's work.
  Work the current day's deliverable only; do not pull in later days.
- Python 3.11+, `uv` for environments and locking, `src`-style layout under
  `service/`. Ruff for lint/format. pytest for tests. Type hints everywhere.
- Node 20 LTS for the CAP mock in `mock-s4/` (`@sap/cds`).
- Secrets live in `.env` (gitignored). Never write keys into code, notebooks,
  or docs. `.env.example` lists every variable with a placeholder.
- S/4HANA and AIF are MOCKED with CAP. Never claim the prototype talks to a
  real S/4 system. Connectors must be swappable by config (base URL + auth).
- All synthetic data comes from generators in `data/`. Never hand-edit
  generated CSV/JSON; fix the generator and regenerate.
- The LLM never calls SAP directly. Agents choose from typed tools in
  `service/agents/tools.py`, gated by `service/agents/policy.py`.
  Anything that would change stock or FI data requires human approval.
- Every agent step, prompt, model version and action is written to the audit
  store (`service/audit/`). If a feature skips audit, it is not done.
- Append a dated entry to `docs/DECISIONS.md` whenever you choose between
  alternatives (library, model, fallback). Keep entries to 3 to 5 lines.
- Keep the build log as described in `docs/BUILD-LOG.md`: `/log` notes to
  `docs/log/day-NN.md` during the day, curate into DECISIONS.md and the README
  status table at the end of it.
- Commit at least once per deliverable with a message that names the
  work-plan day, e.g. `day3: synthetic AIF error generator`.

## Layout
```
service/    FastAPI app: connectors/ llm/ rag/ agents/ ml/ audit/
mock-s4/    CAP project exposing S/4-shaped OData V4 (AIFMessage, Article, Site,
            PhysicalInventoryDoc, CountResult, POSTransaction, FIDocument)
data/       synthetic generators: aif_errors.py, pir.py, pos_fi.py
notebooks/  model training and evaluation
ui/         Streamlit pages: sentinel.py, pir.py, recon.py
deploy/     manifest.yml for BTP Cloud Foundry, AI Core serving templates
docs/       solution-plan.md, work-plan.md, DECISIONS.md, kb/ (runbooks for RAG)
```

## Stack decisions already made
- LLM access through SAP Generative AI Hub (`generative-ai-hub-sdk`) with a
  fallback provider (Ollama / any OpenAI-compatible endpoint) behind the same
  interface in `service/llm/client.py`.
- Vector store: SAP HANA Cloud vector engine via `hdbcli`; DuckDB acceptable
  for local dev only, behind the same interface in `service/rag/store.py`.
- Classical ML: scikit-learn / LightGBM. Agent loop: LangGraph.
- UI: Streamlit only. SAP Build / SAC are stretch goals, not requirements.

## Commands
- `make setup`   create venv, install deps, install CAP deps
- `make mock`    run the CAP mock on :4004
- `make api`     run FastAPI on :8000
- `make ui`      run Streamlit
- `make data`    regenerate all synthetic datasets
- `make smoke`   LLM call + embedding + vector search end to end
- `make test`    pytest
- `make demo`    regenerate data, start mock + api + ui, seed demo cases

## What not to do
- Do not install SAP tooling globally without noting it in DECISIONS.md.
- Do not spend more than 90 minutes on a single blocker; log it, work around
  it, move on. AI Core quota, HANA trial pauses and CAP quirks are expected.
- Do not expand scope beyond the current day's deliverable.
