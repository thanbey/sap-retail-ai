# Learning plan

The goal is that on Day 10 I can whiteboard, explain and defend every part of
this system without notes. Claude Code is a tutor and pair, not a contractor.

## How each day runs

1. Concept first (30 to 45 min). Before any code, Claude explains the day's
   concepts with a small diagram or example. I restate them in my own words in
   docs/log/day-NN.md. If I cannot, we are not done with the concept.
2. I drive. I type the core code for the day's key module. Claude reviews,
   suggests, and writes only scaffolding, tests and boilerplate. Anything
   Claude writes, I read and can explain before it is committed.
3. Break it. Once it works, Claude asks me to predict what happens if we change
   a threshold, a prompt, a schema, a config value. I make the change and check.
4. Interview drill (15 min). Claude asks 3 to 5 questions a hiring manager
   would ask about today's work. I answer out loud, then write the best answer
   into docs/log/day-NN.md under "Drill".
5. Teach it back. The blog post is the test: if I cannot write the day's post
   without looking at the code, the day is not finished.

## Concepts by day

| Day | Concepts I must be able to explain |
|---|---|
| 1 | BTP account hierarchy (global account, subaccount, CF org/space); what CAP is and why it can stand in for S/4; OData V4 basics ($filter, $top, keys); what SAP AIF is and where errors live |
| 2 | AI Core vs Generative AI Hub vs AI Launchpad; deployments, resource groups, service keys; what an embedding is; why a vector store; HANA vector engine vs alternatives |
| 3 | Synthetic data design; AIF interface/namespace/message model; retail interfaces (POS inbound, article master, pricing, goods movements); chunking and RAG retrieval quality |
| 4 | Classification vs LLM: when each; TF-IDF, gradient boosting; precision, recall, macro-F1, confusion matrix; confidence thresholds; serving a model on AI Core |
| 5 | Agent loop (plan, act, verify); typed tools and why the LLM never calls SAP directly; policy gating; audit trail design; LangGraph state |
| 6 | Human-in-the-loop UX; feedback as training data; cf push, manifests, service bindings; API auth (API key now, XSUAA later) |
| 7 | Physical inventory process in S/4 Retail (MI docs, count, difference posting); anomaly detection (Isolation Forest, z-scores); planted-anomaly evaluation |
| 8 | Dashboard design for variance; LLM narratives with structured output; Datasphere and SAC as the production path |
| 9 | POS to FI flow (POS DTA/CAR, tenders, GL mapping); deterministic then fuzzy matching; break taxonomy (timing, mapping, duplicate, FX); correcting entries |
| 10 | Production deltas (real S/4 connector, XSUAA, Datasphere, Joule); Cloud ALM Integration and Exception Monitoring as ingestion; how to present metrics honestly |

## Standing interview questions (answer by Day 10)

- Why an agent instead of a rules engine for AIF errors?
- How do you stop the LLM from posting a bad FI document?
- What does Cloud ALM give you that AIF monitoring alone does not?
- How would you prove the classifier is good enough to auto-remediate?
- What changes when this moves from a CAP mock to a real S/4 system?
- Where does Generative AI Hub sit relative to AI Core, and why use it over
  calling OpenAI directly?
- What is the data model for the PIR dashboard, and where does it live in
  production?
- How do you reconcile POS sales to FI, and what are the usual breaks?

## Reading, 30 min a day, in this order

- SAP AI Core and Generative AI Hub docs: concepts pages only, then the Python
  SDK README.
- CAP "Getting started" and the OData V4 section.
- SAP AIF overview (help.sap.com), and the Cloud ALM Integration and Exception
  Monitoring page.
- LangGraph concepts: state, nodes, edges, tools, human-in-the-loop.
- S/4HANA Retail physical inventory and POS data transfer overview pages.

## Prior art on SAP Community (read before the matching day)

| Day | Post | Take from it |
|---|---|---|
| 1 | Monitoring and error handling for interfaces in AIF (members, 2023) | AIF vocabulary: interfaces, namespaces, error categories, restart vs cancel |
| 2 | How to Integrate SAP AI Core with LangChain Using Generative AI Hub SDK (SAP) | `generative-ai-hub-sdk`, `gen_ai_hub.proxy.langchain` ChatOpenAI with `proxy_model_name` |
| 3 | Cloud ALM Alert Overview, Integration & Exception Monitoring example (SAP) | Alert and exception payload shapes to mirror in the mock |
| 3 | Cloud ALM AI-assisted Solving Tips (SAP, 2025) | Cloud ALM's built-in AI recommends SAP Notes only; it does not act. That gap is Sentinel's reason to exist |
| 5 | SAP Agentic AI in Practice, Parts 1 and 3 (Dorairaj, 2026) | LangGraph state schema, router plus sub-agents, reactive vs scheduled monitoring. Note: triage only, no remediation, no approval, f-string SQL |
| 6 | Hands-on: AI Agent with human-in-the-loop control (CanAbdulla, 2025) | Review node before mutative tools; the approval pattern we use |
| 10 | Build AI Agents on SAP BTP, SAP Architecture Center golden path | Pro-code (LangGraph via SAP Cloud SDK for AI) vs Joule Studio; A2A and MCP; cite in the final post |
| 10 | SAP AI Agent Hub (SAP, 2026) | Governance layer for agents; mention in production deltas |
