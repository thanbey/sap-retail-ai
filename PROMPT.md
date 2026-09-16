# Kickoff prompt for Claude Code

Open a terminal in this folder, run `claude`, and paste the prompt below.
After Day 1, use `/day 2`, `/day 3`, and so on (defined in .claude/commands/day.md).

---

I am building sap-retail-ai, a two-week prototype described in CLAUDE.md,
docs/solution-plan.md and docs/work-plan.md. Read all three now, then
docs/DECISIONS.md.

Today is Day 1. The deliverable is: repo skeleton runnable end to end, a CAP
mock of S/4HANA serving OData V4 for AIFMessage, Article, Site,
PhysicalInventoryDoc, CountResult, POSTransaction and FIDocument, and a
Python OData connector with a passing test against that mock.

Learning mode applies (docs/LEARNING.md): explain the Day 1 concepts first and
check I can restate them, then I write the OData connector myself with your
review; you scaffold the rest. Do it in this order and check in with me
between steps:

1. Python scaffold: pyproject.toml managed with uv (Python 3.11+), src-style
   package under service/, FastAPI app with /health, ruff + pytest configured,
   Makefile with the targets listed in CLAUDE.md (stub the ones for later days).
2. CAP mock in mock-s4/: cds init, schema.cds with the seven entities and
   sensible retail fields (AIFMessage needs interface, namespace, version,
   status, errorClass, messageText, payload as LargeString, createdAt),
   a service exposing them at /odata/v4/retail, and small csv seed data so
   `cds watch` returns rows.
3. service/connectors/s4.py: httpx-based OData V4 client (list with $filter,
   $top, $skip; get by key; patch) reading base URL and auth from settings.
   One pytest that starts against the running mock (or skips with a clear
   message if it is not up) and asserts it can read AIFMessage rows.
4. Update the Day 1 row in README.md, add any decisions to docs/DECISIONS.md,
   and give me a commit message `day1: ...`.

Constraints: no secrets in code, no global installs without telling me, stay
inside this repo, and ask before anything that costs money. If you hit a
blocker for more than a few minutes, log it in DECISIONS.md and propose a
workaround instead of grinding on it.
