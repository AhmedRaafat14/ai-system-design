# 12. Tools and the Agent-Computer Interface (ACI)

*Part III. Agentic Systems · [Reading list](../README.md)*

Tool design deserves the same care as prompt design. Anthropic's guidance
from building tools for Claude:

- **Few, focused, non-overlapping tools** beat exhaustive API mirrors.
  Build a handful of thoughtful tools for high-impact workflows that match
  your [evals](../part-4-production-engineering/21-evaluation-strategy.md), then expand. Every exposed tool definition costs tokens and
  attention.
- **Consolidate multi-step operations** into single tools where the steps
  always go together (schedule_event that also checks availability, not
  three chained primitives).
- **Return token-efficient, high-signal responses.** A search_contacts tool
  beats list_all_contacts; do not make the agent brute-force through
  irrelevant output. Support concise vs detailed response formats.
- **Make errors instructive.** A good error tells the model how to correct
  the call, then gets compacted into context (not a raw stack trace).
- **Poka-yoke the arguments.** Design parameters so misuse is hard (require
  absolute paths, enums instead of free strings, explicit idempotency_key).
- Iterate on tool descriptions using real transcripts; test tools with the
  agent in the loop, not just unit tests.

### Tool contract

```json
{
  "name": "create_support_ticket",
  "description": "Create a customer-support ticket after user confirmation.",
  "input_schema": {
    "type": "object",
    "required": ["customer_id", "summary", "priority", "idempotency_key"],
    "properties": {
      "customer_id": { "type": "string" },
      "summary": { "type": "string", "maxLength": 1000 },
      "priority": { "enum": ["low", "normal", "high"] },
      "idempotency_key": { "type": "string" }
    }
  }
}
```

### Tool rules

- Minimum required permissions per tool; separate read tools from write
  tools; rate each tool's risk (low/medium/high) and gate high-risk tools
  behind confirmation.
- Validate all model-produced parameters server-side against the schema AND
  against business rules; validation next to the side effect is more
  reliable than agent-level checks.
- Per-tool timeout, retry, and cost limits; log inputs, outputs, duration,
  status, error category.
- Never expose credentials, raw database access, or unrestricted shell.
  Sandbox code execution with an egress allowlist.
- Use [structured outputs](../part-2-core-techniques/06-structured-outputs.md) / constrained decoding for every tool call; still
  validate, because schema conformance is not semantic correctness.

---

**Prev:** [11. The Architecture Ladder: Workflows vs Agents](11-workflows-vs-agents.md) · [Reading list](../README.md) · **Next:** [13. MCP (Model Context Protocol)](13-mcp.md)
