# First-Party AI & Shadow AI — SIEM Use Cases

100 SIEM detection use cases covering the two halves of enterprise AI risk:

- **First-Party AI (50)** — detections for the AI you approved and deployed: Microsoft 365 Copilot, ChatGPT Enterprise, Gemini Enterprise, Azure OpenAI, AWS Bedrock, internal RAG applications and agent platforms. Identity and access, data exposure and oversharing, prompt abuse and injection, agentic and tool abuse, model platform abuse, plugins and connectors, governance and guardrail drift, insider misuse and exfiltration.
- **Shadow AI (50)** — detections for the AI you did not approve: unsanctioned GenAI SaaS, personal-account use of approved vendors, AI browser extensions and AI-native browsers, source code and secret leakage, direct API calls bypassing the gateway, local and self-hosted models, shadow OAuth grants and AI notetakers, unregistered agents and low-code AI flows, BYOD and endpoint exposure, and the procurement trail.

Every use case carries the three fields a detection engineer needs to build it:

| Field | What it gives you |
| --- | --- |
| **Use case name** | the detection, stated as an outcome |
| **Log source** | the telemetry it depends on — 85 distinct sources across identity, endpoint, proxy/CASB, cloud, SaaS, CI-CD and AI-platform logs |
| **Sample log** | a representative event in the shape that source actually emits, so you can map fields before you have the data |

Plus **detection logic** (the rule in prose, with the aggregation or correlation it needs) and an indicative **framework mapping** to OWASP Top 10 for LLM Applications (2025) and MITRE ATLAS.

## Contents

- `index.html` — the published, filterable use case library (GitHub Pages)
- `usecases.json` — the structured dataset behind it

Live site: https://laklubin.github.io/First-Party-AI-and-Shadow-AI-SIEM-Use-Case/

## Data model

```json
{
  "id": "SHAI-021",
  "name": "Local LLM runtime installed or executed on an endpoint",
  "category": "Shadow AI",
  "group": "Local & Self-Hosted Models",
  "severity": "Medium",
  "description": "Ollama, LM Studio, llama.cpp, or a similar runtime runs on a corporate device...",
  "log_sources": ["EDR process, file & network events", "Endpoint software inventory"],
  "detection": "Alert on process creation for known local-inference binaries, and on listeners...",
  "mappings": ["OWASP LLM02"],
  "sample_log": "{\"Timestamp\":\"2026-10-23T20:11:47Z\",\"DeviceName\":\"LT-RD-083\",...}"
}
```

## Using this

Each entry is a **use case, not a finished rule**. Treat the log sources as a coverage checklist first: where you do not have the telemetry, the entry is a gap to close before it is a rule to write. Thresholds in the detection logic are illustrative and must be tuned to your own baseline — particularly the volumetric ones (token spend, upload bytes, interaction counts), which vary by an order of magnitude between organisations.

**Sample logs are synthetic.** Field names follow each vendor's published schema (Entra ID and Microsoft 365 unified audit JSON, AWS CloudTrail, Zscaler NSS, Netskope, Defender for Endpoint advanced hunting, Kubernetes audit, GitHub audit, LLM gateway JSON, and so on) so they map cleanly onto real data, but every value is fabricated — no real tenant, user, key, host or customer appears anywhere in this library.

Framework mappings are indicative, added to help align this content with an existing threat model. Neither OWASP's LLM Top 10 nor MITRE ATLAS publishes a native log-source taxonomy the way MITRE ATT&CK for Enterprise does, so the log source mapping here is original work, not a vendor-certified mapping.

## Related

Companion library: [AI Security Use Cases — MITRE ATLAS & OWASP LLM Top 10](https://laklubin.github.io/AI-Security-Use-Case-SIEM/) (188 techniques across the adversarial ML and LLM application attack surface).

Sources and references: [OWASP GenAI Security Project](https://genai.owasp.org), [MITRE ATLAS](https://atlas.mitre.org)

Maintained by LK for AI assurance and detection engineering reference.
