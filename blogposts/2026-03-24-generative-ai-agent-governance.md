# Generative AI Agent Governance - msandbu.org
While most are experimenting with Generative AI in many different flavors such as Claude Code, Codex, OpenClaw, Nemo Claw, Github Copilot, Cursor and the list goes on and on. In addition to this many companies also have other initiatives on cloud based agent frameworks from different companies like Service Now, Microsoft, Salesforce, AWS, Google and the list goes on and on here as well. Lastly let us not forget the open-source frameworks like Langgraph and Agent Framework etc.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/Skjermbilde-2026-03-21-kl.-13.02.28.png?resize=1024%2C489&ssl=1)

Now we can group agents into three different categories, firstly is

*   **Endpoint based agents** – Agents running in the context of the end-user machine that enables it to interact with the machine such as access to the file system and CLI. This is most common with Github Copilot, Codex or Claude Code.
*   **PaaS agents** – Agents running in different cloud providers as a service, this can be Copilot Studio or Tasked as an example. Where these agents have a predefined runtime and access is determined by the platform and what kind of integrations that you have configured such as through native integrations or tools like MCP.
*   **Framework Agents** – In lack of a better term, but these are agents that are using some form of framework and running as a centralized service on some runtime stack. This can be agents built in frameworks like Langgraph or Microsoft Agent Framework.

These agents also have different homes within a business. Where many regular users have adopted Copilot, might be using Now Assist from Service Now or even started to use Cowork. Where the more advanced use-cases are using custom built agents on some form of framework, while developers use one of the many IDEs and built-in agent frameworks.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/image-15.png?resize=1024%2C517&ssl=1)

These agents all have some building blocks in common.

*   **LLM Access** – PaaS agents in most cases have a predefined LLM, while framework and endpoint agents are more agnostic where you can determine which LLM you want to use. While some of them are interacting directly with an inferencing API through a Cloud platform, such as AWS, Azure or Google and others have it embedded as part of their agent platform.
*   **Identity –** Since many of these agents needs to interact with 3.party sources or APIs they need to have some form of identity which is used to authenticate to the service or it can be authentication on-behalf of the user.
*   **Skills & MCP** – This does not apply to all but many of these services are now starting to support MCP and Skills, which allows them to have a predefined set of integrations and expertise to solve different tasks and actions.
*   **Data** – In most cases these agents are interacting with the company data. This can be developer agents that interact with code, or as another example you might have a MCP server configured against Microsoft Fabric which is available through an agent such as Copilot Studio or through even developer agents.

Now a question that I usually get is, how can we govern these agents? Do we have a centralized way to monitor? Do we have a centralized way to secure them?

Well that’s the problem is that you have to do this individually for each service, since there is limited ways to handle this as a centralized service, so let me dig into it.

**Azure Foundry Agents:** Microsoft has now GAed the new Foundry AI Portal and gateway where we can publish custom agents running on the foundry runtime. The neat thing about foundry is that it supports guardrails and tracing that gives us insight into the usage and different tool calls that have been performed by the agent

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/Skjermbilde-2026-03-23-kl.-23.35.51.png?resize=1024%2C518&ssl=1)

Foundry can also integrate with Palo Alto AIRS for guardrails. Foundry also supports Defender for AI, which supports OpenAI models and models from partners listed here –> https://learn.microsoft.com/en-us/azure/foundry/foundry-models/concepts/models-from-partners that can be used to monitor for prompt injection attacks, configure purview to monitor agents data (but requires custom Purview license)

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/Skjermbilde-2026-03-23-kl.-23.45.23.png?resize=1024%2C382&ssl=1)

If you plan to configure direct access to different LLM inferencing APIs you should also look into an AI Gateway, while there are many options to choose from here as well, and Microsoft is trying to position APIM their managed API offering which now has the ability to handle LB to different LLMs and can expose MCP servers and Microsoft has even created their own AI Gateway Developer Portal.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/preview.png?resize=1024%2C636&ssl=1)

Which you can download and read more about from here –> https://github.com/Azure-Samples/ai-gateway-dev-portal

**Skills:** Skills is currently a minefield since a Skill can consist of so much different code, firstly it is a markdown file which contains what to do, but it can be bundled with scripts and other CLI commands that it should run. For instance this is a malicious skill https://github.com/openclaw/skills/blob/main/skills/hightower6eu/yahoo-finance-ijybk/SKILL.md which tells the agent to download another file and run it locally on the machine…. (Still available from OpenClaw Repo..) While Cisco has a free skill-security tool, you can also use online based services such as from Repello https://repello.ai/tools/skills

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/Skjermbilde-2026-03-23-kl.-22.12.11.png?resize=1024%2C614&ssl=1)

**Claude Code and Cowork:** Both comes with a predefined sandbox, while it is enabled by default for CoWork you need to explicitly enabled it for Claude Code by typing **/sandbox** (https://code.claude.com/docs/en/sandboxing) before starting it. In addition Claude Code supports OpenTelemetry as a way to export metrics https://code.claude.com/docs/en/monitoring-usage as an enterprise you can also configure custom rules for permissions which unfortunately does not support MCP server configuration –> https://code.claude.com/docs/en/server-managed-settings. Another issue is when you use Claude Code on the Web, which is a managed service from Anthropic they have additional security guardrails in place.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/Skjermbilde-2026-03-23-kl.-09.52.15.png?resize=1024%2C524&ssl=1)

*   **Isolated virtual machines**: Each cloud session runs in an isolated, Anthropic-managed VM in AWS.
*   **Network access controls**: Network access is limited by default and can be configured to be disabled or allow only specific domains
*   **Credential protection**: Authentication is handled through a secure proxy that uses a scoped credential inside the sandbox, which is then translated to your actual GitHub authentication token
*   **Branch restrictions**: Git push operations are restricted to the current working branch
*   **Audit logging**: All operations in cloud environments are logged for compliance and audit purposes
*   **Automatic cleanup**: Cloud environments are automatically terminated after session completion

However, you have no/limited insight into the usage of these machines and what they do. Lastly is remote control where users can connect to a local Claude Code instance on their machine from their phone using iOS/Android phone, where you have limited ability to control. The best option to avoid that a code instance would get access to sensitive information on the local device is to use Claude Code with .devcontainers and Docker configuration.

https://github.com/anthropics/claude-code/blob/main/.devcontainer/

This allows you to execute this on a local developer container on your own machine, as seen in the screenshot below. This allows you to run a full Claude Code instance in a local sandbox.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/Skjermbilde-2026-03-23-kl.-10.13.14.png?resize=1024%2C498&ssl=1)

Or you can use OpenShell from NVIDIA which does some of the same that runs the instance within a docker container https://github.com/NVIDIA/OpenShell but also Alibaba Cloud OpenSandbox has a larger ecosystem of built-in tools and capabilities when it comes to handle LLM traffic and ingress https://github.com/alibaba/OpenSandbox

If you want you get better insight into the usage if you configure Claude Code together with an LLM directly from Microsoft Foundry, AWS Bedrock, Google Vertex or LLM Gateway like LiteLLM. Setting it up with Foundry allows you to get better insight into the usage of the LLM but does not provide you with any capabilities to manage the agent. Read more about Foundry set up here –> https://code.claude.com/docs/en/microsoft-foundry

It should also be noted that Claude recently added support for Microsoft 365 using native connectors –> https://support.claude.com/en/articles/12542951-enable-and-use-the-microsoft-365-connector that allows Claude to query data in Microsoft 365 (Dont worry it needs admin approval to get access) but you should also ensure that this is properly monitored. If you are using Sentinel you can use the following KQL query to detect the usage of these connectors https://github.com/SlimKQL/Detections.AI/blob/main/KQL/m365-connector-for-claude-detection.kql

**Github Copilot:**

Github Copilot allows you to get access to a multitude of different LLMs such as Claude, OpenAI GPT, Gemini, Grok and others it also provides some more management capabilities. We can determine what kind of LLMs that should be available, and we can also configure which MCP servers that should be available (and also enforce it!) at least for certain frameworks/IDE

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/Skjermbilde-2026-03-23-kl.-22.13.40.png?resize=1024%2C820&ssl=1)

Where we can define an MCP registry where we can provide a predefined list of MCP servers that should be available for Github Copilot users. It is important to note that there is a difference between an MCP registry and a MCP Gateway. While a Gateway handles the authentication and traffic flow to MCP servers, a registry is just a catalogue. Also for Github Copilot and VS Code there are two supported options for MCP Registry at the moment, either self-hosted using the official MCP registry or Azure API Center.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/Skjermbilde-2026-03-23-kl.-22.22.04.png?resize=1024%2C820&ssl=1)

In addition to this, the coding agent running locally VSCode can also use the same approach with DevContainers. That allows you to run Github Copilot agents and CLI within an isolated docker container.

Also like Claude, Github Copilot within VSCode also supports OpenTelemetry for monitoring of usage. Same goes for Github Copilot CLI, documentation here –> https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference#opentelemetry-monitoring

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/Skjermbilde-2026-03-23-kl.-22.30.47.png?resize=1024%2C149&ssl=1)

However when it comes to coding agents in Github that are attached to a repository, we also have some other management capabilities such as defining firewall rules, MCP configuration. The logs of the usage of these agents are collected through Github audit logs, that can be collected trough Sentinel or other SIEM or log collectors.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/Skjermbilde-2026-03-23-kl.-22.38.52.png?resize=1024%2C454&ssl=1)

You also now have the option to define which MCP servers that can be used within the organization (with the recent update that was released in April –> GitHub Copilot in Visual Studio — March update – GitHub Changelog)

I am not going to go into details when it comes to Cursor, but let’s just say that they have their own capabilities when it comes to security settings and audit logs, as can be seen here –> https://cursor.com/docs/account/teams/analytics The issue is that regardless of which product you select (Agents, IDE or CLI tools) what kind of governance, auditing, security logs is different. Same also applies to which guardrails that each of them have in place in terms of protection against prompt injection, malicious skills and malicious MCP servers.

But what can we do with Agent 365? Agent 365 is Microsoft’s answer to provide a unified platform for managing AI agents built across Microsoft Copilot Studio, Azure Foundry, and third-party runtimes. However right now the third-party runtimes is limited to Semantic Kernel, OpenAI, Agent Framework, LangChain agents. For instance with Langchain you need to toolkit extension to provide observability https://www.npmjs.com/package/@microsoft/agents-a365-tooling-extensions-langchain

While it should be noted that Microsoft also introduced Microsoft Defender for Cloud Apps – Copilot Studio, that allows you to get threat monitoring and better prompt injection for Copilot Studio created agents. I am not going into details on how to set that up since there is a great blog about it here –> https://jeffreyappel.nl/how-to-secure-microsoft-copilot-studio-agents-with-real-time-protection/ That means that as of right now there some blind spots if you are using Agent 365 and use a variety of agents

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/Skjermbilde-2026-03-23-kl.-22.57.05.png?resize=1024%2C209&ssl=1)

Also this problem becomes bigger when teams and others are starting to use other tools and platform from other vendors. Including the regular suspects from Service Now, Salesforce, AWS, Google and the list of agent frameworks.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/Skjermbilde-2026-03-23-kl.-23.04.02.png?resize=1024%2C384&ssl=1)

Observability:
--------------

When it comes to observability, the ability to understand what an agent is doing, there are many different ways to handle this. For local insight you have VS Code and debug mode, but in most cases I have been using this tool –> https://github.com/tobilg/ai-observer

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/image-16.png?resize=1024%2C668&ssl=1)

But for an organization that wants to view this for the entire company and across frameworks/plattforms, the good part is that most of these agents/frameworks support OpenTelemetry, which is an open source observability framework for software. However it does require configuration on each system using this so that information is sent to centralized service.

*   Claude Code –> https://code.claude.com/docs/en/monitoring-usage
*   Azure Foundry Agents –> https://learn.microsoft.com/en-us/azure/foundry/observability/concepts/trace-agent-concept
*   Github Copilot –> https://code.visualstudio.com/docs/copilot/guides/monitoring-agents#\_enable-otel-monitoring
*   OpenAI Codex –> https://developers.openai.com/codex/config-advanced#observability-and-telemetry

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/image-18.png?resize=1024%2C583&ssl=1)

There are also frameworks like OpenLIT which provides a set of centralized frameworks and tools to integrate most LLMs and agent frameworks –> https://github.com/openlit/openlit

Some of the vendors also have their own compliance API, which is many cases is not enabled by default, and vendors like Anthropic just added this capability two days ago –> Access the Compliance API | Claude Help Center

A sort of summary or conclusion…
--------------------------------

One thing to note is that there is no single solution that can handle all different agents, frameworks, LLM providers and provide a centralized ways to manage governance across.

1: Understand the providers and capabilities what is it that the service provides – Management? Observability ? Audit logs? Guardrails?  
2: MCP and Skills should be should be managed individually, however with care. I recommend setting up a private marketplace using the .claude example so that employees can use centralized skills and plugins https://code.claude.com/docs/en/plugin-marketplaces and also having some form of custom-built security check of skills should be in place.  
3: Configure local agents to run in sandbox using .devcontainers or sandbox (as with Claude or OpenShell, OpenSandbox) with limitations in terms of network/file access.  
4: Ensure that MCP servers and or scripts through Skills to not use API keys, passwords or shared secrets. They should always connect using OAuth or Managed Identities wherever possible.  
5: Ensure that you have traceability in how agents are used. This way you can audit what agents did, which tools they used and LLMs.
