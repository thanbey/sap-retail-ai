# ADR 0001: Get SAP AI Core from the Generative AI Hub trial, not the BTP trial

Date: 2026-09-16
Status: Accepted

## Context

The BTP trial account (`2aa19bf4trial`, US East (VA) AWS) does not offer SAP AI
Core. Its Booster catalog lists only Business Entity Recognition and Data
Attribute Recommendation under Artificial Intelligence. The "free tier" AI Core
booster in SAP tutorials applies to a pay-as-you-go account with a credit card
on file, not to the trial.

Days 2 through 10 need an AI Core tenant for LLM calls, embeddings, and model
serving through Generative AI Hub.

## Options

1. Generative AI Hub 30-day trial. No card. Ships its own AI Core tenant and
   service key. Expires after 30 days.
2. Convert to a BTP free-tier (pay-as-you-go) account. Card required; free
   plans cost nothing; AI Core "free" plan does not expire. Risk of accidental
   paid-plan use. About an hour of setup.
3. Skip AI Core; use Ollama or an OpenAI-compatible API behind the same
   interface. Loses the SAP-native story the job requires.

## Decision

Option 1 for the two-week build. Start the Generative AI Hub trial on Day 1
(moved from Day 2) so the 30 days cover Day 10 plus about 18 days of demos.
Keep option 3 wired as the fallback provider. Revisit option 2 after Day 10 if
the demo needs to stay live.

## Consequences

- `AICORE_*` values in `.env` come from the GenAI Hub trial service key.
- HANA Cloud still comes from the BTP trial via the "Set Up SAP HANA Cloud
  Administration Tools" booster.
- Blog Day 0 post gains a paragraph: trial does not include AI Core.
- Interview talking point: know the difference between trial, free tier and
  enterprise entitlements for AI Core.
