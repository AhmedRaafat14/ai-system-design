# 20. Security (mapped to OWASP Top 10 for LLM Applications, 2025)

*Part IV. Production Engineering · [Reading list](../README.md)*

| Risk | Core mitigation |
|---|---|
| LLM01 Prompt injection | Assume it succeeds; containment architecture, least privilege, human gates on consequential actions |
| LLM02 Sensitive information disclosure | Data minimization in context, output filtering, PII redaction in logs |
| LLM03 Supply chain | Pin and verify models, adapters, datasets, [MCP](../part-3-agentic-systems/13-mcp.md) servers, and libraries; scan third-party artifacts |
| LLM04 Data and model poisoning | Provenance and validation for training/[fine-tuning](../part-2-core-techniques/10-fine-tuning.md) data and [RAG](../part-2-core-techniques/08-rag-system-design.md) sources |
| LLM05 Improper output handling | Treat model output as untrusted input to downstream systems; sanitize before render/execute |
| LLM06 Excessive agency | Minimal tools, minimal permissions, confirmation for high-impact actions |
| LLM07 System prompt leakage | Assume the system prompt is public; never put secrets or auth logic in it |
| LLM08 Vector and [embedding](../part-2-core-techniques/09-embeddings-and-vectors.md) weaknesses | ACLs on vector stores, tenant isolation, index poisoning detection |
| LLM09 Misinformation | Grounding, citations, abstention, human review for high-stakes output |
| LLM10 Unbounded consumption | Budgets, quotas, per-run circuit breakers, anomaly alerts |

### Prompt injection: design for containment

"Separate instructions from data" is necessary but NOT sufficient; models
cannot reliably distinguish injected instructions inside data, and
classifier-based filters have been bypassed in shipped products (e.g., the
EchoLeak zero-click exfiltration in Microsoft 365 Copilot, CVE-2025-32711).
So:

- Apply Simon Willison's **lethal trifecta** rule: an agent that combines
  (1) access to private data, (2) exposure to untrusted content, and
  (3) the ability to communicate externally can be tricked into exfiltrating
  data. Break at least one leg by architecture: e.g., the agent that reads
  untrusted web/email content does not hold privileged tools or open egress.
- Everything influenced by untrusted input is itself untrusted, including
  the model's own output (chains into LLM05).
- Layer defenses: input classifiers, allowlisted egress, output validation,
  scoped credentials, human approval for consequential actions. Watch the
  research on capability-based designs (e.g., CaMeL) but do not bet the
  system on any single filter.
- Security controls live in deterministic, auditable code outside the
  model. A system prompt is not a security boundary.

Also standard hygiene: authenticate every request, authorize every
retrieval, encrypt in transit and at rest, redact secrets and PII in logs
and traces, audit privileged tool actions, define retention for prompts and
transcripts, keep credentials out of anything model-visible.

---

**Prev:** [19. Reliability Patterns](19-reliability-patterns.md) · [Reading list](../README.md) · **Next:** [21. Evaluation Strategy](21-evaluation-strategy.md)
