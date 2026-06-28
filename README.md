# Awesome Agentic AI Security [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of resources for **securing agentic AI** — systems where models **choose actions** (tools, APIs, code, data, and money), not just generate text.

**Thesis:** prompts guide behavior; **specs, policies, and runtimes** must enforce what agents are allowed to do. This list favors **deterministic boundaries**, **eval**, and **evidence** over prompt-only guardrails.

Maintained by [Mayur Sinha](https://themayursinha.com) · [MCP Visor](https://github.com/themayursinha/mcp-visor) · *Prompts guide. Specs enforce.*

---

## Contents

- [Control planes & runtime enforcement](#control-planes--runtime-enforcement)
- [MCP firewalls, proxies & policy](#mcp-firewalls-proxies--policy)
- [Sandboxes & isolation](#sandboxes--isolation)
- [Gateways & output guardrails](#gateways--output-guardrails)
- [Static analysis & agent supply chain](#static-analysis--agent-supply-chain)
- [Observability, audit & SOC](#observability-audit--soc)
- [Evaluation, red team & benchmarks](#evaluation-red-team--benchmarks)
- [Skills, hooks & coding agents](#skills-hooks--coding-agents)
- [Papers](#papers)
- [Notable writeups & advisories](#notable-writeups--advisories)
- [Standards, frameworks & checklists](#standards-frameworks--checklists)
- [Learning](#learning)
- [Related awesome lists](#related-awesome-lists)
- [Contributing](#contributing)
- [License](#license)

---

## Control planes & runtime enforcement

Tools on the **action path** (tool calls, egress, secrets) — not only filtering model text.

- [Adrian](https://github.com/secureagentics/Adrian) — Runtime security monitoring and control for AI agents; catches malicious tool use and policy violations.
- [Doberman-Core](https://github.com/fu351/Doberman-Core) — Agent security framework: guardrails, prompt-injection handling, and policy around tool execution.
- [Invariant Labs](https://invariantlabs.ai/) — Runtime guardrails and tracing for agent workflows (commercial; reference architecture for tool-call policies).
- [MCP Visor](https://github.com/themayursinha/mcp-visor) — Declarative YAML policy on an MCP proxy: parse, redact, chain rules, approval gates, hash-chained audit.
- [PipeLock](https://github.com/luckyPipewrench/pipelock) — Open-source agent firewall for MCP and agent egress; scans and constrains outbound/tool traffic.
- [Tracecat](https://github.com/TracecatHQ/tracecat) — Open-source security automation platform for teams **and** AI agents (orchestration + guardrails in SOC workflows).

---

## MCP firewalls, proxies & policy

**Model Context Protocol** and tool-RPC boundaries. For MCP-only depth, see [awesome-mcp-security](https://github.com/Puliczek/awesome-mcp-security).

- [awesome-mcp-security](https://github.com/Puliczek/awesome-mcp-security) — The dedicated MCP security awesome list (papers, tools, incidents).
- [JanuScope](https://github.com/giancarloerra/JanuScope) — Local-first MCP policy proxy: tool block, SQL-mutation gate, PII redaction.
- [mcp-reticle](https://github.com/soth-ai/mcp-reticle) — Intercept, visualize, and profile MCP JSON-RPC traffic.
- [Model Context Protocol — specification](https://modelcontextprotocol.io/) — Official spec: transports, tools, trust boundaries.
- [MCP — security best practices (draft)](https://modelcontextprotocol.io/specification/draft/basic/security_best_practices) — Official security guidance for implementers.
- [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers) — Reference MCP servers; study each as **untrusted code with network access**.
- [MCP Security Checklist](https://github.com/slowmist/MCP-Security-Checklist) — Community checklist for hardening MCP deployments.

---

## Sandboxes & isolation

Where agent **code and tools** run — contain blast radius before policy even applies.

- [Computer-Use Agent (CUA)](https://github.com/trycua/cua) — Open infrastructure for computer-use agents: sandboxes, SDKs, isolation patterns.
- [OpenSandbox](https://github.com/opensandbox-group/OpenSandbox) — Secure, fast, extensible sandbox runtime built for AI agents.
- [Context Mode](https://github.com/mksglu/context-mode) — Context-window optimization via sandboxed tool output (reduces leakage surface in coding agents).

---

## Gateways & output guardrails

Sit between apps and models; useful for **rate limits, logging, and guardrails** — complement (not replace) runtime tool enforcement.

- [Guardrails](https://github.com/guardrails-ai/guardrails) — Open-source guardrails for LLM inputs/outputs (validators, structure, policy hooks).
- [LiteLLM](https://github.com/BerriAI/litellm) — AI gateway / proxy to 100+ APIs; supports callbacks, logging, and policy hooks in the request path.
- [LLM Guard](https://github.com/protectai/llm-guard) — Security toolkit for LLM interactions (sanitization, detection, scanners).
- [NeMo Guardrails](https://github.com/NVIDIA-NeMo/Guardrails) — Programmable rails for dialog and tool flows in NVIDIA NeMo stacks.
- [Portkey AI Gateway](https://github.com/Portkey-AI/gateway) — AI gateway with integrated guardrails and routing to many providers.
- [LangKit](https://github.com/whylabs/langkit) — Open toolkit for monitoring and testing LLM inputs/outputs (quality + security signals).

---

## Static analysis & agent supply chain

Find misconfigurations **before** runtime — MCP configs, skills, dangerous tools.

- [agent-audit](https://github.com/HeadyZhang/agent-audit) — Static scanner for LLM agents: prompt injection surfaces, MCP config risks.
- [Agentic Radar](https://github.com/splx-ai/agentic-radar) — Security scanner for agentic workflows (graph of tools, data flows, risks).
- [AgentSeal](https://github.com/getagentseal/agentseal) — Scan the machine for dangerous agent skills, configs, and exposure.
- [AI Security Rules](https://github.com/SecureCodeWarrior/ai-security-rules) — Security rule packs for AI-assisted coding tools.
- [Armur VibeScan](https://github.com/Armur-Ai/vibescan) — SAST-style scanner aimed at AI-generated (“vibe-coded”) applications.

---

## Observability, audit & SOC

Evidence for **what the agent did** — required for incident response and compliance.

- [Future AGI](https://github.com/future-agi/future-agi) — Open platform for eval, observability, and improvement loops on LLM/agent apps.
- [OpenLIT](https://github.com/openlit/openlit) — OpenTelemetry-native LLM observability (traces, costs, security-relevant telemetry).
- [Tracecat](https://github.com/TracecatHQ/tracecat) — *(also listed above)* Case management and automation when agents participate in security ops.

---

## Evaluation, red team & benchmarks

Prove agents **fail safely** under prompt injection, tool abuse, and data exfiltration.

- [AgentDojo](https://github.com/ethz-spylab/agentdojo) — Dynamic environment for attacks and defenses on tool-using agents.
- [AI-Infra-Guard](https://github.com/Tencent/AI-Infra-Guard) — Full-stack AI red-teaming platform for the AI ecosystem (models, agents, infra).
- [Argus](https://github.com/gy15901580825/Argus) — Black-box open-source red-team testing for AI agents.
- [DeepEval](https://github.com/confident-ai/deepeval) — LLM eval framework; supports agent and RAG test cases.
- [Garak](https://github.com/NVIDIA/garak) — LLM vulnerability scanning and probing.
- [Giskard](https://github.com/Giskard-AI/giskard) — Open-source evaluation and testing for LLM agents (bias, robustness, security tests).
- [LLAMATOR](https://github.com/LLAMATOR-Core/llamator) — Red-teaming framework for chatbots and GenAI systems.
- [MCP LLM Security Evaluator](https://github.com/themayursinha/mcp-llm-security-evaluator) — Eval harness for MCP / LLM security scenarios.
- [promptfoo](https://github.com/promptfoo/promptfoo) — Test prompts, agents, and RAG; red teaming and regression suites.
- [Purple Llama](https://github.com/meta-llama/PurpleLlama) — Meta’s Llama stack tools including **CyberSec Eval** and related safety benchmarks.
- [PyRIT](https://github.com/Azure/PyRIT) — Microsoft’s Python Risk Identification Toolkit for generative AI red teaming.
- [Whistleblower](https://github.com/Repello-AI/whistleblower) — Offensive security tooling for testing system prompts and agent boundaries.
- [awesome-skills-security](https://github.com/Eyadkelleh/awesome-skills-security) — Curated security testing patterns for agent skills and tool surfaces.

---

## Skills, hooks & coding agents

Where **most production agents** live today (IDE agents, Claude Code, OpenClaw, etc.).

- [AGENTS.md patterns](https://github.com/Austin1serb/agents-md) — Context-engineering patterns for coding agents; safer conventions for tool and repo access.
- [Anthropic Cybersecurity Skills](https://github.com/mukul975/Anthropic-Cybersecurity-Skills) — Large structured skill library for security tasks in agent harnesses (map to your threat model).
- [Claude Hooks (Lasso)](https://github.com/lasso-security/claude-hooks) — Security integrations for Claude Code, including prompt-injection oriented hooks.
- [ClawShield](https://github.com/SleuthCo/clawshield-public) — Security proxy for AI agents; scans messages for injection before they reach the model/tools.
- [Dropbox LLM Security](https://github.com/dropbox/llm-security) — Research code and results from Dropbox’s LLM security work (relevant patterns for enterprise agents).
- [openai-agents-python](https://github.com/openai/openai-agents-python) — OpenAI’s multi-agent SDK — read the docs with least-privilege tools and handoff risks in mind.
- [LangGraph](https://github.com/langchain-ai/langgraph) — Agent orchestration graphs; security = state boundaries + tool scopes per node.

---

## Papers

Peer-reviewed and preprint work on **agents, tools, MCP, and control**.

- [MCP: Landscape, Security Threats, and Future Research Directions (2025)](https://arxiv.org/abs/2503.23278) — Survey of MCP threat landscape.
- [MCP Safety Audit: LLMs with MCP Allow Major Security Exploits (2025)](https://arxiv.org/abs/2504.03767) — Empirical safety audit of MCP integrations.
- [Beyond the Protocol: Attack Vectors in the MCP Ecosystem (2025)](https://arxiv.org/abs/2506.02040) — Attack vectors beyond the base spec.
- [Enterprise-Grade Security for MCP (2025)](https://arxiv.org/pdf/2504.08623) — Frameworks and mitigations for enterprise MCP.
- [MCP Guardian: Security-First Layer for MCP-Based AI Systems (2025)](https://arxiv.org/abs/2504.12757) — Gateway/guardian architecture for MCP.
- [Systematic Analysis of MCP Security (2025)](https://arxiv.org/pdf/2508.12538) — Systematic analysis of MCP security properties.
- [Simplified and Secure MCP Gateways for Enterprise AI (2025)](https://arxiv.org/abs/2504.19997) — Enterprise MCP gateway design.

*For more MCP papers and videos, see [awesome-mcp-security](https://github.com/Puliczek/awesome-mcp-security).*

---

## Notable writeups & advisories

High-signal **incidents and architecture** posts (agent + MCP). Not exhaustive — see Puliczek’s list for the full timeline.

- [Simon Willison — MCP has prompt injection security problems (2025)](https://simonwillison.net/2025/Apr/9/mcp-prompt-injection/) — Why tool context is an attack surface.
- [Trail of Bits — How MCP servers can steal your conversation history (2025)](https://blog.trailofbits.com/2025/04/23/how-mcp-servers-can-steal-your-conversation-history/) — Data exfiltration via malicious servers.
- [Trail of Bits — Jumping the line: MCP servers attack before first use (2025)](https://blog.trailofbits.com/2025/04/21/jumping-the-line-how-mcp-servers-can-attack-you-before-you-ever-use-them/) — Install-time / supply-chain risks.
- [CyberArk — Poison everywhere: no MCP server output is safe (2025)](https://www.cyberark.com/resources/threat-research-blog/poison-everything-no-output-from-your-mcp-server-is-safe/) — Tool and resource poisoning.
- [Invariant — GitHub MCP exploited: private repo access (2025)](https://invariantlabs.ai/blog/mcp-github-vulnerability) — Realistic tool-scope failure case.
- [Wiz — MCP Security Research Briefing (2025)](https://www.wiz.io/blog/mcp-security-research-briefing) — Enterprise-oriented threat summary.
- [Google DeepMind — AI Control roadmap](https://deepmind.google/discover/blog/ai-control/) — Research agenda for evaluating and controlling capable AI systems.
- [Anthropic — Building effective agents](https://www.anthropic.com/research/building-effective-agents) — Agent patterns; pair with least-privilege tool design.

---

## Standards, frameworks & checklists

- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) — Risk framing for AI systems in production.
- [OWASP AI Security and Privacy Guide](https://owasp.org/www-project-ai-security-and-privacy-guide/) — Community guide for AI security and privacy.
- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) — Baseline threats including excessive agency and supply chain.
- [OWASP Top 10 for LLM Applications (GitHub)](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications) — Project repo and change history.
- [MCP Security Checklist (SlowMist)](https://github.com/slowmist/MCP-Security-Checklist) — Practical MCP deployment checklist.

---

## Learning

- [AI Agents: The Definitive Guide](https://github.com/Nicolepcx/ai-agents-the-definitive-guide) — Broad agent reference; read security chapters with tool-permission mindset.
- [Learning LLMs and GenAI for DevSecOps](https://github.com/jedi4ever/learning-llms-and-genai-for-dev-sec-ops) — Lessons for builders who ship agents into production environments.
- [awesome-security-vul-llm](https://github.com/xu-xiang/awesome-security-vul-llm) — Curated vulnerability / POC resources (use only in authorized environments).

---

## Related awesome lists

- [awesome-mcp-security](https://github.com/Puliczek/awesome-mcp-security) — MCP-specific security (papers, tools, incidents).
- [awesome-llm-security](https://github.com/corca-ai/awesome-llm-security) — Broader LLM security; many items apply to agents.
- [awesome-skills-security](https://github.com/Eyadkelleh/awesome-skills-security) — Security testing for agent skills.

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). **Quality over quantity** — every link should earn its place.

If you maintain a tool that enforces policy on **tool calls** (not just prompts), open a PR under [Control planes](#control-planes--runtime-enforcement) or [MCP firewalls](#mcp-firewalls-proxies--policy).

**Star this repo** to help others find curated agent-security resources.

---

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, contributors have waived all copyright to this list. Individual linked projects keep their own licenses.