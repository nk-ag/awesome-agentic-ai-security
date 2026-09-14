# Awesome Agentic AI Security [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of resources for **securing agentic AI** — systems where models **choose actions** (tools, APIs, code, data, and money), not just generate text.

**Thesis:** prompts guide behavior; **specs, policies, and runtimes** must enforce what agents are allowed to do. This list favors **deterministic boundaries**, **eval**, and **evidence** over prompt-only guardrails.

Maintained by [Mayur Sinha](https://themayursinha.com) · [MCP Visor](https://github.com/themayursinha/mcp-visor) · *Prompts guide. Specs enforce.*

---

## Contents

- [Control planes & runtime enforcement](#control-planes--runtime-enforcement)
- [Agent identity & authorization](#agent-identity--authorization)
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
- [Failproof](https://github.com/FailproofAI/failproofai) — Learn from agent traces to find failure modes and fix them with policies (MIT, open-core).
- [Invariant Labs](https://invariantlabs.ai/) — Runtime guardrails and tracing for agent workflows (commercial; reference architecture for tool-call policies).
- [MCP Visor](https://github.com/themayursinha/mcp-visor) — Declarative YAML policy on an MCP proxy: parse, redact, chain rules, approval gates, hash-chained audit.
- [PipeLock](https://github.com/luckyPipewrench/pipelock) — Open-source agent firewall for MCP and agent egress; scans and constrains outbound/tool traffic.
- [Tracecat](https://github.com/TracecatHQ/tracecat) — Open-source security automation platform for teams **and** AI agents (orchestration + guardrails in SOC workflows).

---

## Agent identity & authorization

Agents are **non-human principals acting on your behalf** — identity is the control plane that makes least-privilege enforceable.

- [Descope — Diving Into the MCP Authorization Specification](https://descope.com/blog/post/mcp-auth-spec) — Implementation-level walkthrough of MCP's OAuth 2.1 flows (DCR, PKCE, resource indicators).
- [Microsoft Entra Agent ID](https://learn.microsoft.com/en-us/entra/agent-id/what-is-microsoft-entra-agent-id) — Identity lifecycle for agents in Entra: stable agent IDs, no passwords, Zero Trust controls for non-human actors.
- [MCP — Authorization specification](https://modelcontextprotocol.io/specification/draft/basic/authorization) — Official auth design: MCP server as OAuth resource server, separate authorization server, token audience binding.
- [OpenID Connect for Agents (OIDC-A) 1.0 (2025)](https://arxiv.org/abs/2509.25974) — Proposed OIDC extension carrying agent-specific claims (type, model, provider) for accountable agent identity.

---

## MCP firewalls, proxies & policy

**Model Context Protocol** and tool-RPC boundaries. For MCP-only depth, see [awesome-mcp-security](https://github.com/Puliczek/awesome-mcp-security).

- [awesome-mcp-security](https://github.com/Puliczek/awesome-mcp-security) — The dedicated MCP security awesome list (papers, tools, incidents).
- [Cisco AI Defense mcp-scanner](https://github.com/cisco-ai-defense/mcp-scanner) — Connects to MCP servers and pattern-scans tool descriptions, schemas, and responses for threats.
- [Invariant mcp-scan](https://github.com/invariantlabs-ai/mcp-scan) — Scans installed MCP servers for tool poisoning, rug-pull mutations, and shadowing; also proxies traffic with guardrails.
- [JanuScope](https://github.com/giancarloerra/JanuScope) — Local-first MCP policy proxy: tool block, SQL-mutation gate, PII redaction.
- [mcp-reticle](https://github.com/soth-ai/mcp-reticle) — Intercept, visualize, and profile MCP JSON-RPC traffic.
- [mcp-shield](https://github.com/riseandignite/mcp-shield) — Detects hidden instructions, exfiltration channels, and cross-origin escalations in installed MCP servers.
- [Model Context Protocol — specification](https://modelcontextprotocol.io/) — Official spec: transports, tools, trust boundaries.
- [MCP — security best practices (draft)](https://modelcontextprotocol.io/specification/draft/basic/security_best_practices) — Official security guidance for implementers.
- [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers) — Reference MCP servers; study each as **untrusted code with network access**.
- [MCP Security Checklist](https://github.com/slowmist/MCP-Security-Checklist) — Community checklist for hardening MCP deployments.

---

## Sandboxes & isolation

Where agent **code and tools** run — contain blast radius before policy even applies.

- [Computer-Use Agent (CUA)](https://github.com/trycua/cua) — Open infrastructure for computer-use agents: sandboxes, SDKs, isolation patterns.
- [Context Mode](https://github.com/mksglu/context-mode) — Context-window optimization via sandboxed tool output (reduces leakage surface in coding agents).
- [E2B](https://github.com/e2b-dev/E2B) — Firecracker microVM sandboxes purpose-built for agent code execution; self-hostable OSS with managed option.
- [Firecracker](https://github.com/firecracker-microvm/firecracker) — AWS's microVM manager (~50K LoC Rust VMM); the isolation primitive under most agent code-execution stacks.
- [gVisor](https://github.com/google/gvisor) — User-space application kernel intercepting syscalls; strong auditability and reduced host-kernel surface for agent workloads.
- [microsandbox](https://github.com/zerocore-ai/microsandbox) — Self-hosted libkrun microVM runtime for untrusted agent code; dedicated kernel per sandbox on your own infra.
- [OpenSandbox](https://github.com/opensandbox-group/OpenSandbox) — Secure, fast, extensible sandbox runtime built for AI agents.
- [Wassette](https://github.com/microsoft/wassette) — Microsoft's WebAssembly-based tool runtime: capability-scoped components instead of unrestricted process tools.

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
- [Security Context](https://securitycontext.dev/) — Provides AI agents with historical security context (commit fixes + CVEs) for any public GitHub repo via MCP and API.

---

## Observability, audit & SOC

Evidence for **what the agent did** — required for incident response and compliance.

- [Future AGI](https://github.com/future-agi/future-agi) — Open platform for eval, observability, and improvement loops on LLM/agent apps.
- [OpenLIT](https://github.com/openlit/openlit) — OpenTelemetry-native LLM observability (traces, costs, security-relevant telemetry).
- [Tracecat](https://github.com/TracecatHQ/tracecat) — *(also listed above)* Case management and automation when agents participate in security ops.
- [Uber ADR](https://github.com/uber/ADR) — Production agentic detection & response: sensor (Cursor/Claude/Codex traces), two-tier detector, ADR-Bench; prevention/Explorer not fully OSS.

---

## Evaluation, red team & benchmarks

Prove agents **fail safely** under prompt injection, tool abuse, and data exfiltration.

- [ADR-Bench (Uber ADR)](https://github.com/uber/ADR/tree/main/Detection) — Enterprise MCP agent security bench: 300+ tasks, 133 MCP servers, 17 techniques; pair with AgentDojo.
- [AgentDojo](https://github.com/ethz-spylab/agentdojo) — Dynamic environment for attacks and defenses on tool-using agents.
- [Agent Security Bench (ASB) (ICLR 2025)](https://arxiv.org/abs/2410.02644) — 10 scenarios / 400 tools formalizing direct & indirect prompt injection, memory poisoning, and tool-oracle attacks.
- [Agent-SafetyBench](https://github.com/thu-coai/Agent-SafetyBench) — 2,000 test cases across 349 environments and 8 risk categories for interactive agent safety.
- [AI-Infra-Guard](https://github.com/Tencent/AI-Infra-Guard) — Full-stack AI red-teaming platform for the AI ecosystem (models, agents, infra).
- [Argus](https://github.com/gy15901580825/Argus) — Black-box open-source red-team testing for AI agents.
- [Darkmoon](https://github.com/ASCIT31/Dark-Moon) — Autonomous AI pentest platform; notable agent-architecture pattern: tokenization gateway keeps real IPs and credentials out of model context, tools run through a controlled MCP layer.
- [DeepEval](https://github.com/confident-ai/deepeval) — LLM eval framework; supports agent and RAG test cases.
- [Garak](https://github.com/NVIDIA/garak) — LLM vulnerability scanning and probing.
- [Giskard](https://github.com/Giskard-AI/giskard) — Open-source evaluation and testing for LLM agents (bias, robustness, security tests).
- [InjecAgent](https://github.com/uiuc-kang-lab/InjecAgent) — 1,054 test cases measuring tool-integrated agent vulnerability to indirect prompt injection (direct harm + data stealing).
- [LLAMATOR](https://github.com/LLAMATOR-Core/llamator) — Red-teaming framework for chatbots and GenAI systems.
- [MCP LLM Security Evaluator](https://github.com/themayursinha/mcp-llm-security-evaluator) — Eval harness for MCP / LLM security scenarios.
- [promptfoo](https://github.com/promptfoo/promptfoo) — Test prompts, agents, and RAG; red teaming and regression suites.
- [Purple Llama](https://github.com/meta-llama/PurpleLlama) — Meta’s Llama stack tools including **CyberSec Eval** and related safety benchmarks.
- [PyRIT](https://github.com/Azure/PyRIT) — Microsoft’s Python Risk Identification Toolkit for generative AI red teaming.
- [R-Judge](https://github.com/Lordog/R-Judge) — Benchmark scoring whether LLMs can *judge* safety risks in multi-turn agent interaction records (10 risk types).
- [ToolEmu](https://github.com/ryoungj/toolemu) — Emulates tool execution with an LM-based kernel to identify risky agent behaviors at scale.
- [ToolSword](https://github.com/Junjie-Ye/ToolSword) — Safety benchmark covering input, execution, and output stages of tool learning (deceptive tools, data exposure).
- [Whistleblower](https://github.com/Repello-AI/whistleblower) — Offensive security tooling for testing system prompts and agent boundaries.
- [awesome-skills-security](https://github.com/Eyadkelleh/awesome-skills-security) — Curated security testing patterns for agent skills and tool surfaces.

---

## Skills, hooks & coding agents

Where **most production agents** live today (IDE agents, Claude Code, OpenClaw, etc.).

- [AGENTS.md patterns](https://github.com/Austin1serb/agents-md) — Context-engineering patterns for coding agents; safer conventions for tool and repo access.
- [Anthropic Cybersecurity Skills](https://github.com/mukul975/Anthropic-Cybersecurity-Skills) — Large structured skill library for security tasks in agent harnesses (map to your threat model).
- [Claude Code — Security documentation](https://code.claude.com/docs/en/security) — Vendor guidance on permissioning, sandboxing, and prompt-injection hardening for coding agents.
- [Claude Hooks (Lasso)](https://github.com/lasso-security/claude-hooks) — Security integrations for Claude Code, including prompt-injection oriented hooks.
- [ClawShield](https://github.com/SleuthCo/clawshield-public) — Security proxy for AI agents; scans messages for injection before they reach the model/tools.
- [Dropbox LLM Security](https://github.com/dropbox/llm-security) — Research code and results from Dropbox’s LLM security work (relevant patterns for enterprise agents).
- [openai-agents-python](https://github.com/openai/openai-agents-python) — OpenAI’s multi-agent SDK — read the docs with least-privilege tools and handoff risks in mind.
- [LangGraph](https://github.com/langchain-ai/langgraph) — Agent orchestration graphs; security = state boundaries + tool scopes per node.

---

## Papers

Peer-reviewed and preprint work on **agents, tools, MCP, and control**.

- [ADR: An Agentic Detection System for Enterprise Agentic AI Security (2026)](https://arxiv.org/abs/2605.17380) — Uber production ADR + ADR-Bench; MLSys 2026 industry track.
- [MCP: Landscape, Security Threats, and Future Research Directions (2025)](https://arxiv.org/abs/2503.23278) — Survey of MCP threat landscape.
- [MCP Safety Audit: LLMs with MCP Allow Major Security Exploits (2025)](https://arxiv.org/abs/2504.03767) — Empirical safety audit of MCP integrations.
- [Beyond the Protocol: Attack Vectors in the MCP Ecosystem (2025)](https://arxiv.org/abs/2506.02040) — Attack vectors beyond the base spec.
- [Enterprise-Grade Security for MCP (2025)](https://arxiv.org/pdf/2504.08623) — Frameworks and mitigations for enterprise MCP.
- [MCP Guardian: Security-First Layer for MCP-Based AI Systems (2025)](https://arxiv.org/abs/2504.12757) — Gateway/guardian architecture for MCP.
- [Systematic Analysis of MCP Security (2025)](https://arxiv.org/pdf/2508.12538) — Systematic analysis of MCP security properties.
- [Simplified and Secure MCP Gateways for Enterprise AI (2025)](https://arxiv.org/abs/2504.19997) — Enterprise MCP gateway design.
- [Design Patterns for Securing LLM Agents against Prompt Injections (2025)](https://arxiv.org/abs/2506.08837) — The canonical patterns paper: action-selector, plan-then-execute, dual-LLM, Codex-style separation.
- [MCP-Guard: A Multi-Stage Defense-in-Depth Framework (2025)](https://arxiv.org/abs/2508.10991) — Layered detection pipeline for tool-description poisoning and exfiltration.
- [MPMA: Preference Manipulation Attack Against MCP (2025)](https://arxiv.org/abs/2505.11154) — Subtly biasing how agents rank and select tools in multi-server registries.
- [MCP at First Glance: Studying the Security of MCP Servers (2025)](https://arxiv.org/abs/2506.13538) — Empirical study of 1,899 real MCP servers; 5.5% showed tool-poisoning patterns.
- [Agent Security Bench (ASB) (ICLR 2025)](https://arxiv.org/abs/2410.02644) — Formalizing attacks & defenses in LLM-based agents across 10 scenarios.
- [InjecAgent (ACL Findings 2024)](https://aclanthology.org/2024.findings-acl.624/) — Benchmark establishing indirect prompt injection risk for tool-integrated agents.
- [R-Judge (EMNLP Findings 2024)](https://arxiv.org/abs/2401.10019) — Safety-risk awareness judging over agent interaction traces.
- [ToolSword (2024)](https://arxiv.org/abs/2402.10753) — Safety issues of LLMs in tool learning across three stages.
- [Agent-SafetyBench (2024)](https://arxiv.org/abs/2412.14470) — Large-scale interactive safety evaluation for LLM agents.

*For more MCP papers and videos, see [awesome-mcp-security](https://github.com/Puliczek/awesome-mcp-security).*

---

## Notable writeups & advisories

High-signal **incidents and architecture** posts (agent + MCP). Not exhaustive — see Puliczek’s list for the full timeline.

- [Aim Security — EchoLeak: zero-click M365 Copilot exfiltration (CVE-2025-32711)](https://www.aim.security/blog/echoleak-zero-click-copilot-vulnerability) — First zero-click exploit of a production AI agent: RAG context inheritance turned one email into silent data theft.
- [Anthropic — Building effective agents](https://www.anthropic.com/research/building-effective-agents) — Agent patterns; pair with least-privilege tool design.
- [CyberArk — Poison everywhere: no MCP server output is safe (2025)](https://www.cyberark.com/resources/threat-research-blog/poison-everything-no-output-from-your-mcp-server-is-safe/) — Tool and resource poisoning.
- [Embrace The Red — Copilot: from prompt injection to exfiltration via ASCII smuggling (2024)](https://embracethered.com/blog/posts/2024/m365-copilot-prompt-injection-tool-invocation-and-data-exfil-using-ascii-smuggling/) — The foundational enterprise-copilot exfiltration technique.
- [Google DeepMind — Securing the future of AI agents (AI Control Roadmap)](https://deepmind.google/blog/securing-the-future-of-ai-agents/) — Defense-in-depth framework treating capable agents as potentially misaligned: detection levels, response tiers, live monitoring.
- [Invariant — GitHub MCP exploited: private repo access (2025)](https://invariantlabs.ai/blog/mcp-github-vulnerability) — Realistic tool-scope failure case ("toxic agent flow" across public/private repos).
- [Invariant — MCP tool poisoning attacks (2025)](https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks) — Hidden instructions in tool descriptions that persist across projects.
- [Invariant — WhatsApp MCP exploited (2025)](https://invariantlabs.ai/blog/whatsapp-mcp-exploited) — Message-history injection through a third-party MCP integration.
- [JFrog — Critical RCE in mcp-remote (CVE-2025-6514)](https://jfrog.com/blog/2025-6514-critical-mcp-remote-rce-vulnerability/) — OS command injection in the OAuth flow of the bridge most stdio-only clients use to reach remote servers.
- [Legit Security — Remote prompt injection in GitLab Duo (2025)](https://www.legitsecurity.com/blog/remote-prompt-injection-in-gitlab-duo) — Source-code theft and HTML injection via hidden prompts in merge requests.
- [Microsoft — Protecting against indirect prompt injection attacks in MCP (2025)](https://developer.microsoft.com/blog/protecting-against-indirect-injection-attacks-mcp) — Vendor guidance on trust boundaries when tool output is untrusted input.
- [Oligo — Critical RCE in MCP Inspector (CVE-2025-49596)](https://www.oligo.security/blog/critical-rce-vulnerability-in-anthropic-mcp-inspector-cve-2025-49596) — Browser-to-localhost attack chain against developer tooling (0.0.0-day + missing proxy auth).
- [Pomerium — When AI has root: lessons from the Supabase MCP data leak (2025)](https://www.pomerium.com/blog/when-ai-has-root-lessons-from-the-supabase-mcp-data-leak) — The lethal-trifecta incident: privileged agent + untrusted tickets + public channel.
- [Simon Willison — The lethal trifecta (2025)](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/) — Private data + untrusted content + external communication: why this combination fails.
- [Simon Willison — MCP has prompt injection security problems (2025)](https://simonwillison.net/2025/Apr/9/mcp-prompt-injection/) — Why tool context is an attack surface.
- [Snyk — ToxicSkills: malicious skills in agent registries (2026)](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/) — First large audit of the skill ecosystem; ~37% of scanned skills had security flaws.
- [Trail of Bits — How MCP servers can steal your conversation history (2025)](https://blog.trailofbits.com/2025/04/23/how-mcp-servers-can-steal-your-conversation-history/) — Data exfiltration via malicious servers.
- [Trail of Bits — Jumping the line: MCP servers attack before first use (2025)](https://blog.trailofbits.com/2025/04/21/jumping-the-line-how-mcp-servers-can-attack-you-before-you-ever-use-them/) — Install-time / supply-chain risks.
- [vulnerableMCP.info](https://vulnerablemcp.info/) — Community-maintained tracker of MCP-specific CVEs and disclosed vulnerabilities.
- [Wiz — MCP Security Research Briefing (2025)](https://www.wiz.io/blog/mcp-security-research-briefing) — Enterprise-oriented threat summary.

---

## Standards, frameworks & checklists

- [CoSAI — Coalition for Secure AI](https://www.coalitionforsecureai.org/) — Industry coalition; secure-by-design principles for agentic AI systems.
- [CSA — Agentic AI Red Teaming Guide](https://cloudsecurityalliance.org/artifacts/agentic-ai-red-teaming-guide) — Structured methodology for red-teaming autonomous agents (not just chatbots).
- [CSA — MAESTRO threat modeling framework](https://cloudsecurityalliance.org/blog/2025/02/06/agentic-ai-threat-modeling-framework-maestro) — Seven-layer threat model spanning agent systems: foundation models → agent orchestration → tools.
- [MCP Security Checklist (SlowMist)](https://github.com/slowmist/MCP-Security-Checklist) — Practical MCP deployment checklist.
- [MITRE ATLAS](https://atlas.mitre.org/) — Adversarial Threat Landscape for AI Systems: attacker TTPs incl. LLM prompt injection and agent context poisoning.
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) — Risk framing for AI systems in production.
- [OWASP Agentic Security Initiative](https://genai.owasp.org/initiatives/agentic-security-initiative/) — Umbrella project for securing autonomous agents and multi-step AI workflows.
- [OWASP Agentic Skills Top 10](https://github.com/OWASP/www-project-agentic-skills-top-10) — Risks & mitigations for agent skill ecosystems (SKILL.md, hooks, registries).
- [OWASP AIVSS](https://aivss.owasp.org/) — Vulnerability scoring system adapted to agentic AI weaknesses.
- [OWASP AI Security and Privacy Guide](https://owasp.org/www-project-ai-security-and-privacy-guide/) — Community guide for AI security and privacy.
- [OWASP MCP Top 10](https://owasp.org/www-project-mcp-top-10/) — MCP-specific risk taxonomy mapped to real CVEs.
- [OWASP Top 10 for Agentic Applications 2026](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/) — Peer-reviewed top risks for agents that plan, act, and transact (goal hijack, identity abuse, tool misuse…).
- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) — Baseline threats including excessive agency and supply chain.
- [OWASP Top 10 for LLM Applications (GitHub)](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications) — Project repo and change history.

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
- [Awesome-AI-Security](https://github.com/TalEliyahu/Awesome-AI-Security) — Curated AI security resources, research, and tools; dedicated agent tooling & MCP security section. (Site: [awesomeaisecurity.com](https://www.awesomeaisecurity.com/))

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). **Quality over quantity** — every link should earn its place.

If you maintain a tool that enforces policy on **tool calls** (not just prompts), open a PR under [Control planes](#control-planes--runtime-enforcement) or [MCP firewalls](#mcp-firewalls-proxies--policy).

**Star this repo** to help others find curated agent-security resources.

---

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, contributors have waived all copyright to this list. Individual linked projects keep their own licenses.