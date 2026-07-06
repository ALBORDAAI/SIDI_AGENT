<div align="center">

<img src="./assets/sidi-avatar.png" alt="SIDI — AI Customer Support Agent" width="220">

# SIDI
### The AI Customer Support Agent, Native to Hassaniya

**Status:** 🟢 In Production &nbsp;·&nbsp; **Version:** 1.0 &nbsp;·&nbsp; **Built by** [Alborda AI](https://alborda.ai)

</div>

---

## 1. What is SIDI?

**SIDI** is Alborda AI's flagship B2B product: a fully automated, multichannel customer support agent built specifically for the Mauritanian market. Unlike generic international chatbots that translate Arabic or French into approximate responses, SIDI is powered by **Dimeyz**, Alborda's proprietary large language model natively trained on **Hassaniya Arabic** — the everyday spoken language of Mauritania.

SIDI is not a custom integration built once per client. It is a **configurable product**: every business onboards onto the same core engine, with tenant-specific knowledge bases, channels, and feature flags — no forked codebases, no one-off maintenance burden.

**Who it's for:** banks, telecom operators, and any consumer-facing business in Mauritania that needs to handle high support volume without forcing customers to write in French or wait on hold.

---

## 2. Why SIDI is different

| # | Differentiator | What it means in practice |
|---|---|---|
| 01 | **Native Hassaniya** | Responses are generated directly in Hassaniya by Dimeyz — not machine-translated from English or French. |
| 02 | **Code-switching** | Mauritanian customers naturally mix Hassaniya, French, and Modern Standard Arabic mid-sentence. SIDI follows the switch without losing context. |
| 03 | **Mobile money literacy** | Balance checks, transfer status, and agent locations are handled as first-class intents, not edge cases. |
| 04 | **Omnichannel by design** | WhatsApp, Facebook, and Instagram are unified behind one conversation history — a customer can start on WhatsApp and continue on Messenger without repeating themselves. |
| 05 | **Human handoff** | Conversations that need a person are escalated with full context, not a cold transfer. |
| 06 | **Live CSAT tracking** | Every conversation is scored for sentiment, giving support teams a real-time satisfaction signal instead of a quarterly survey. |
| 07 | **Data sovereignty** | Tenant data never trains third-party models. No retention agreements with external LLM providers for production traffic. |

---

## 3. How it works — architecture overview

```
                         ┌─────────────────────────────┐
                         │   Client channels             │
                         │   WhatsApp · Facebook · IG    │
                         └──────────────┬────────────────┘
                                        │
                              Channel Adapters
                        (normalize into InboundMessage)
                                        │
                                        ▼
                        ┌───────────────────────────────┐
                        │     Orchestration Layer         │
                        │  · Intent detection              │
                        │  · Routing (tenant, plan, flags)│
                        └───────┬───────────────┬─────────┘
                                │               │
                     Voice note?│               │Text
                                ▼               ▼
                     ┌────────────────┐   ┌─────────────┐
                     │ Dimeyz Speech   │   │  RAG layer   │
                     │ (ASR)           │   │ (tenant KB)  │
                     └────────┬────────┘   └──────┬──────┘
                              └─────────┬──────────┘
                                        ▼
                              ┌───────────────────┐
                              │   Dimeyz (LLM)      │
                              │ Hassaniya generation│
                              └─────────┬───────────┘
                                        │
                        Voice channel?  │  Text channel
                              ┌─────────┴─────────┐
                              ▼                   ▼
                    ┌──────────────────┐   ┌─────────────┐
                    │ Dimeyz Speech     │   │  Direct      │
                    │ (TTS)             │   │  reply       │
                    └────────┬──────────┘   └──────┬──────┘
                             └──────────┬───────────┘
                                        ▼
                        ┌───────────────────────────────┐
                        │   Decision & Logging            │
                        │  · Resolved automatically        │
                        │  · Transfer to human              │
                        │  · Ticket created                 │
                        │  · Sentiment + metrics logged      │
                        └───────────────────────────────┘
```

Every stage is decoupled: channel adapters know nothing about the LLM, the LLM knows nothing about the channel, and the RAG layer is scoped per tenant. This is what makes multi-tenancy a foundation rather than a retrofit.

---

## 4. Core components

| Component | Role |
|---|---|
| **Dimeyz** | Proprietary LLM natively trained on Hassaniya Arabic. Generates all text responses. |
| **Dimeyz Speech** | ASR/TTS module for voice notes — the dominant input format on WhatsApp in Mauritania. |
| **Channel Adapters** | Pluggable connectors that translate each platform's API into a single internal message format. |
| **Orchestration Layer** | Routes messages, applies tenant feature flags, decides between auto-resolution, human handoff, or ticket creation. |
| **RAG Layer** | Retrieves tenant-specific knowledge (FAQs, product info, policies) to ground responses in accurate, client-approved content. |
| **Supabase (multi-tenant)** | Stores tenants, conversations, messages, tickets, and CSAT scores. Self-hosted for full data sovereignty. |

---

## 5. Supported channels

`WHATSAPP` · `FACEBOOK MESSENGER` · `INSTAGRAM DM` · `VOICE NOTES`

---

## 6. Plans & feature flags

SIDI is offered in tiered formulas, each unlocking a different set of feature flags at the tenant level (voice, sentiment analysis, human handoff, ERP/ticketing integration). Feature flags are modeled at the data layer, not scattered through conditional logic — this keeps every tenant on the same core codebase regardless of plan.

---

## 7. Data & security principles

- **No third-party training on tenant data.** Conversations never leave Alborda's infrastructure to train external models.
- **Self-hosted core infrastructure** (Supabase, orchestration) for full control over data residency.
- **PII scrubbing and encryption at rest** applied to all stored conversation data.
- **Audio processing** transits external ASR providers only with logging disabled and no data retention for training.

---

## 8. Roadmap highlights

- Deeper ERP / ticketing system integrations (Zendesk, Freshdesk, or custom)
- Expanded mobile money intents (bill payments, merchant lookup)
- Compliance features for regulated sectors (banking-grade audit trails)
- Additional channels based on tenant demand

---

## 9. About Alborda AI

Founded in 2024 in Mauritania, Alborda AI is an international AI company democratizing artificial intelligence for underrepresented languages across the Middle East and North Africa (MENA). We develop language models and personalize them for a wide range of tasks, so millions can access advanced AI natively — in their own language, not a borrowed one.

**Products:** Dimeyz (LLM) · SIDI (B2B support agent) · MOUNA (executive assistant) · SOULEYMAN (AI tutor) · Dimeyz Chat (consumer chat)

---

## 10. Contact

📧 [contact@alborda.ai](mailto:contact@alborda.ai)
🌐 [alborda.ai](https://alborda.ai)

---

<div align="center">
<sub>© 2026 Alborda AI — Building AI that speaks your language.</sub>
</div>
