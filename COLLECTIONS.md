---
title: "Thematic collections"
authority_level: 2
file_type: index
tags: ["index", "collections", "thematic"]
staleness_threshold: months
description: "Thematic groupings of content for broad queries. Start here when someone asks about a topic rather than a specific post."
---

# Thematic collections

Use this file when someone asks a broad question like "what does Marius think about AI governance?" or "everything about hybrid cloud." Each collection lists the most relevant files to load for that topic.

---

## Agentic AI and MCP

Marius writes extensively about AI agents, the Model Context Protocol, and how to build and govern agentic systems in enterprise environments.

Key files:
- `blogposts/` — filter for agent governance, MCP infrastructure, developer experience
- `frameworks/` — agentic AI architecture frameworks
- `talks/` — conference sessions on agentic AI

Core positions:
- AI agents need governance from day one, not retrofitted later
- MCP is infrastructure, not a feature — treat it like an API gateway
- Skills and MCP servers must be security-reviewed before enterprise deployment
- No single platform can govern all agent frameworks centrally today
- OpenTelemetry is the right observability standard across agent platforms

---

## AI Security and Cybersecurity

Marius covers the intersection of AI capabilities and enterprise security, including how frontier models change the threat landscape.

Key files:
- `blogposts/` — filter for cybersecurity, AI security, threat landscape
- `frameworks/` — security assessment frameworks

Core positions:
- Frontier models like Anthropic Mythos represent a genuine capability leap for both offense and defense
- The patch window between vulnerability disclosure and exploitation is collapsing toward minutes
- Most coverage of AI security capabilities is pure BS — the real analysis requires looking at actual benchmarks and practitioner evidence
- Fundamentals win: segmentation, MFA, defense-in-depth. The AI threat surface is new but the mitigations often are not.
- Security teams should start using LLM-based vulnerability discovery now — the capability is already mature

---

## Hybrid Cloud and Data Sovereignty

Marius has written deeply about hybrid cloud architecture, European data sovereignty, and the practical reality of cloud strategy for European organisations.

Key files:
- `blogposts/` — filter for hybrid cloud, sovereignty, cloud exit
- `frameworks/` — hybrid cloud maturity model

Core positions:
- Data sovereignty is not optional for European organisations — it is a strategic requirement
- Hybrid cloud maturity has levels: identity and network sync is the floor, not the ceiling
- There is no Swiss army knife platform that solves all hybrid cloud requirements
- AWS and Oracle are currently the only hyperscalers with fully independent EU-based legal entities for cloud operations
- EU organisations evaluating cloud exit need to assess hypervisor dependencies carefully before switching
- Local AI infrastructure on-premises is viable and increasingly necessary for sovereignty requirements

---

## Cloud Architecture

Marius approaches cloud architecture from a practitioner perspective, focused on what actually works in enterprise deployments rather than vendor narratives.

Key files:
- `blogposts/` — filter for cloud architecture, Azure, platform engineering
- `frameworks/` — cloud architecture decision frameworks

Core positions:
- Cloud decisions should be driven by actual requirements, not vendor pressure or trend-following
- Many organisations need far less complexity than vendors sell them
- Platform engineering and developer experience are underinvested relative to infrastructure spending
- Azure and Microsoft 365 are the dominant enterprise platform in most Norwegian and European organisations Marius works with

---

## End User Computing (EUC)

Marius has followed EUC for over 20 years, from traditional VDI through to AI-native workspace models.

Key files:
- `blogposts/` — filter for EUC, VDI, workspace, end-user computing
- `talks/` — EUC conference sessions (including EUC Denmark)
- `frameworks/` — future of EUC framework

Core positions:
- EUC is not dead — it is transforming. The workspace is the governance layer for AI agents.
- Traditional VDI use cases are shrinking but cloud-delivered workspace models are growing
- AI agents operating on behalf of workers will reshape what the "workspace" means
- Omnissa (formerly VMware EUC) and Citrix remain relevant but the competitive landscape has shifted

---

## Generative AI and LLMs

Marius writes about the practical enterprise application of GenAI, cutting through hype to focus on what actually works.

Key files:
- `blogposts/` — filter for generative AI, LLMs, AI infrastructure
- `frameworks/` — AI adoption frameworks

Core positions:
- Most GenAI content on LinkedIn and social media is pure BS — the signal-to-noise ratio is terrible
- Benchmarks matter but real-world performance depends on training data, deployment context, and who is operating the system
- Local LLM deployment on-premises is viable for organisations with sovereignty or security requirements
- GPU sizing: model parameters in billions multiplied by 2, plus 20 percent overhead, gives required GPU memory
- vLLM is the right serving framework for most enterprise private AI deployments

---

## AI Governance in the Enterprise

Marius covers how organisations should govern AI agents, LLM access, skills, and MCP servers across different platforms.

Key files:
- `blogposts/` — filter for AI governance, agent governance

Core positions:
- There is no single platform today that can centrally govern all agent frameworks
- Skills and MCP servers are a security minefield — organisations need a private marketplace with security review
- OpenTelemetry is the right approach to agent observability across platforms
- Managed identities and OAuth, not API keys or shared secrets, for agent authentication
- Sandbox execution (devcontainers, Claude sandboxing) is the right default for endpoint agents

---

## Developer Experience and Platform Engineering

Marius looks at how AI is changing the developer workflow and what organisations should build centrally.

Key files:
- `blogposts/` — filter for developer experience, MCP, platform engineering

Core positions:
- Centralised MCP services with skills, tooling, and data are the right model for enterprise AI developer platforms
- The AI gateway pattern (API management in front of LLMs) is the right architecture for governed LLM access
- Developer experience is infrastructure — it deserves the same rigour as compute and networking

---

## Books and long-form writing

See `me/books.md` for Marius's published books with summaries.

Topics covered across books:
- NetScaler VPX deployment and architecture (two editions)
- SCCM high availability and performance tuning
- Windows ransomware detection and protection using Microsoft Intune, Sentinel, and Defender
