# 16. Human-in-the-Loop

*Part III. Agentic Systems · [Reading list](../README.md)*

Two triggers should always hand control to a human (OpenAI's agent guide):

1. **Failure thresholds exceeded**: repeated retries, repeated
   misunderstanding of intent, budget exhaustion.
2. **High-risk actions**: irreversible, sensitive, or high-value operations
   (refunds, payments, cancellations, external communications) until
   confidence is earned.

Implementation notes:

- Model "contact a human" as a tool call that pauses the workflow and
  resumes on response (async approvals via Slack/email work well when state
  is checkpointed).
- Escalations must carry clean context: what was tried, what failed, what
  is pending. No raw transcript dumps.
- Review queues + sampled human review for medium-risk output; 100% review
  early in a launch, then ratchet down as [evals](../part-4-production-engineering/21-evaluation-strategy.md) earn trust.
- Capture feedback (thumbs, edits, escalation reasons) and feed it into the
  eval set and retrieval fixes. This flywheel is the actual moat.

---

**Prev:** [15. Multi-Agent Systems (rarely justified)](15-multi-agent-systems.md) · [Reading list](../README.md) · **Next:** [17. Reference Architecture](../part-4-production-engineering/17-reference-architecture.md)
