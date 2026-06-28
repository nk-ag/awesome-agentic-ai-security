# Awesome Agentic AI Security [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of resources for **securing agentic AI** — systems where models **choose actions** (tools, APIs, code, data, and money), not just generate text.

**Thesis:** prompts guide behavior; **specs, policies, and runtimes** must enforce what agents are allowed to do. This list favors **deterministic boundaries**, **eval**, and **evidence** over prompt-only guardrails.

Maintained by [Mayur Sinha](https://themayursinha.com) · [MCP Visor](https://github.com/themayursinha/mcp-visor) · *Prompts guide. Specs enforce.*

---

## Contents

- [Control planes & runtime enforcement](#control-planes--runtime-enforcement)
- [MCP & tool protocols](#mcp--tool-protocols)
- [Evaluation, red team & benchmarks](#evaluation-red-team--benchmarks)
- [Papers & roadmaps](#papers--roadmaps)
- [Standards & guides](#standards--guides)
- [Related awesome lists](#related-awesome-lists)
- [Contributing](#contributing)
- [License](#license)

---

## Control planes & runtime enforcement

Tools that sit **on the action path** (tool calls, egress, secrets) rather than only filtering model output.

- [MCP Visor](https://github.com/themayursinha/mcp-visor) — Declarative YAML policy enforced by a Go MCP proxy: parse, redact, chain rules, approval gates, hash-chained audit.
- [mcp-reticle](https://github.com/soth-ai/mcp-reticle) — Intercept, visualize, and profile MCP JSON-RPC traffic for debugging and inspection.
- [Invariant Labs](https://invariantlabs.ai/) — Runtime guardrails and tracing for agent workflows (commercial; useful reference architecture).

*Add gateways, sidecars, and policy engines that enforce **before** side effects occur.*

---

## MCP & tool protocols

Security around **Model Context Protocol** and similar tool surfaces.

- [awesome-mcp-security](https://github.com/Puliczek/awesome-mcp-security) — Focused MCP security list (complementary; deeper MCP-specific coverage).
- [Model Context Protocol — specification](https://modelcontextprotocol.io/) — Official MCP docs; understand auth, transports, and server trust boundaries.
- [Anthropic — MCP security best practices](https://docs.anthropic.com/en/docs/agents-and-tools/mcp) — Vendor guidance on deploying MCP safely (verify current URL in docs).

*Protocol security is necessary but not sufficient: treat every MCP server as **untrusted code with network access**.*

---

## Evaluation, red team & benchmarks

Measure whether agents **leak, exfiltrate, or abuse tools** under attack.

- [MCP LLM Security Evaluator](https://github.com/themayursinha/mcp-llm-security-evaluator) — Evaluation harness oriented around MCP / LLM security scenarios.
- [Garak](https://github.com/NVIDIA/garak) — LLM vulnerability scanning / probing framework.
- [PyRIT](https://github.com/Azure/PyRIT) — Microsoft Python Risk Identification Toolkit for generative AI red teaming.
- [AgentDojo](https://github.com/ethz-spylab/agentdojo) — Benchmark for prompt injection and tool misuse in agent environments.
- [awesome-skills-security](https://github.com/Eyadkelleh/awesome-skills-security) — Security testing patterns for agent skills and tool surfaces.

---

## Papers & roadmaps

Research and industry framing for **misalignment, oversight, and control at the tool boundary**.

- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) — Baseline threat model including excessive agency and supply chain issues.
- [Google DeepMind — AI Control roadmap](https://deepmind.google/discover/blog/ai-control/) — Research agenda for evaluating and controlling capable AI systems (high-level; pair with runtime enforcement in production).
- [Anthropic — Building effective agents](https://www.anthropic.com/research/building-effective-agents) — Agent design patterns; read with a security lens (tool access, least privilege).

*Prefer papers that discuss **actions and environments**, not only jailbreak strings.*

---

## Standards & guides

- [OWASP AI Security and Privacy Guide](https://owasp.org/www-project-ai-security-and-privacy-guide/) — Community guide for AI system security and privacy.
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) — Risk framing useful for agent deployments in regulated contexts.

---

## Related awesome lists

- [awesome-mcp-security](https://github.com/Puliczek/awesome-mcp-security) — MCP-specific security resources.
- [awesome-llm-security](https://github.com/corca-ai/awesome-llm-security) — Broader LLM security (prompt injection, data leakage); many items apply to agents.

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). PRs welcome. Quality over quantity.

**Star this repo** if you want more curated agent-security resources in one place — it helps others find the list and signals what the community cares about.

---

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, contributors have waived all copyright to this list. Individual linked projects keep their own licenses.