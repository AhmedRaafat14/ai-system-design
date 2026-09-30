# 13. MCP (Model Context Protocol)

*Part III. Agentic Systems · [Reading list](../README.md)*

MCP is the open standard for connecting models to tools and data
(client-server), launched by Anthropic in late 2024, adopted across the
major AI vendors and developer tools, and now governed vendor-neutrally
under a Linux Foundation body. Treat it as the default integration layer
when you want tools reusable across models and clients, instead of bespoke
per-provider function wiring.

Production rules:

- **Third-party MCP servers are supply chain** ([OWASP](../part-4-production-engineering/20-security.md) LLM03). Pin versions,
  review the tool descriptions you import (tool-description injection is a
  real attack vector), and re-review on update.
- Scope credentials per server, allowlist which servers each agent may use,
  and prefer read-only servers wherever possible.
- Everything in §12 still applies: an MCP tool is still a tool. The
  protocol standardizes transport and discovery, not safety.
- The spec is evolving (auth hardening, long-running tasks, stateless
  transport); pin the protocol version you deploy against and track
  deprecations.

---

**Prev:** [12. Tools and the Agent-Computer Interface (ACI)](12-tools-and-aci.md) · [Reading list](../README.md) · **Next:** [14. Agent Memory](14-agent-memory.md)
