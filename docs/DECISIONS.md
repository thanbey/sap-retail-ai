# Decisions log

## 2026-09-16 Project setup
- S/4HANA and AIF mocked with SAP CAP rather than the CAL appliance, to avoid
  hyperscaler cost. Connector is config-swappable if a real system appears.
- BTP trial + AI Core free-tier booster + 30-day Generative AI Hub trial.
  Start the GenAI Hub trial on Day 2 so the clock covers demos.
- Fallback LLM provider (Ollama) behind the same interface for trial gaps.

## 2026-09-16 BTP trial region
- US East (VA) - AWS chosen because SAP AI Core and HANA Cloud are both offered
  there on trial; EU regions were the alternative and lack the AI Core booster
  on some trial landscapes.

## 2026-09-16 GitHub via gh CLI, HTTPS remote
- Create repos with `gh repo create --public --source=. --push`, not the web
  form. Remote is HTTPS with gh as credential helper; SSH remained an option
  but HTTPS avoids key management on a new machine.
