# 14. Agent Memory

*Part III. Agentic Systems · [Reading list](../README.md)*

- **Working memory is the context window.** Manage it with the techniques
  in §7 (compaction, tool result clearing, sub-agents).
- **Persistent memory** is external: structured notes/files the agent
  writes and re-reads, or retrieval over past interactions. Store
  decisions, stable preferences, constraints, and failed approaches, not
  raw transcripts; over-storage becomes permanent context pollution.
- **Memory is an attack and privacy surface.** Poisoned memories persist
  across sessions (a stored injected instruction fires forever), so
  validate and constrain what gets written; give users visibility and
  deletion controls; apply the same ACL discipline as retrieval (§8).
- Expire or summarize aggressively. Memory systems degrade into noise
  without a curation policy.

---

**Prev:** [13. MCP (Model Context Protocol)](13-mcp.md) · [Reading list](../README.md) · **Next:** [15. Multi-Agent Systems (rarely justified)](15-multi-agent-systems.md)
