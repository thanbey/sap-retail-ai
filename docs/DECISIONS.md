# Decisions log

## 2026-09-16 Project setup
- S/4HANA and AIF mocked with SAP CAP rather than the CAL appliance, to avoid
  hyperscaler cost. Connector is config-swappable if a real system appears.
- BTP trial + AI Core free-tier booster + 30-day Generative AI Hub trial.
  Start the GenAI Hub trial on Day 2 so the clock covers demos.
- Fallback LLM provider (Ollama) behind the same interface for trial gaps.
