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

## 2026-09-16 Approach check against SAP Community prior art
- Exception triage agents on BTP with LangGraph plus Generative AI Hub are an
  established pattern (SAP Architecture Center golden path, Dorairaj series).
  Keep the stack. Differentiate on: AIF and retail specificity, typed
  remediation gated by policy and approval, audit trail, PIR and POS-to-FI.
- Cloud ALM Solving Tips only recommends SAP Notes; Sentinel acts. State this
  explicitly in the solution plan and Day 10 post.
- Single agent for Sentinel in the prototype; router plus sub-agents is a
  documented production delta, not a two-week goal.
- Use parameterised queries everywhere (prior art used f-string SQL).
