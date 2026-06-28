# ServiceNow and Microsoft Copilot - msandbu.org
This is a summary of a presentation that I had a few weeks ago where I went into different integration options between Microsoft Copilot and Service Now, both using Copilot 365 and with Copilot Studio building custom agents.

Before we go into the different options it is important to understand the different GenAI models and the ecosystem since within ServiceNow we have the option to choose from different models. Now Assist which is a combination of different “skills” in ServiceNow such as case summary can be defined as a skill. For many of these skills we can configure which AI model we want to use (Azure OpenAI, Claude, Gemini or NowLLM which depending on which version is Llama or Mistral-Nemo.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/11/image.png?resize=617%2C343&ssl=1)

This does not apply for all skills most for many of them where we can configure which models can be used by each skill. In most cases GPT-5 is the best model, but this can change quickly with the release of Google Gemini 3 coming shortly.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/11/image-2.png?resize=546%2C520&ssl=1)

I also want to mention MCP, which I have previously blogged about Copilot Studio Agents with MCP using Logic Apps – msandbu.org

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/11/image-3.png?resize=734%2C390&ssl=1)

MCP provides an easier way to integrate 3.party system, and the interesting part is that ServiceNow is coming with their own MCP servers. Firstly Service Now can trigger different MCP servers Introducing AI Agent Fabric – Enable MCP and A2A f… – ServiceNow Community and also Bring the ServiceNow AI Platform to Any Employee Experience with the MCP Server Console.

While we are waiting for the official MCP server, here in this video I am using a community one from Claude which is a MCP client. Where I am using different MCP tools to update and create knowledge articles.

Where the results in Service Now would look like this. It is important to note that MCP allows different actions to become available using natural language, instead of being a UI navigator in Service Now.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/11/image-4.png?resize=1024%2C500&ssl=1)

For those that have Copilot 365, we also have the ability to use Graph Connectors, which allows us to fetch data from Service Now and index them directly into Microsoft 365. Right now there are 3 built-in connectors which include ServiceNow Incidents, Knowledge and Catalogue items. The cool thing about this is that users do not need to go into Service Now to get information they can just query Copilot 365 to get information (Which is also the downside, since it cannot do actions only give information).

As seen in this video below, which goes trough the Copilot 365 integration and shows knowledge sources (sorry in Norwegian but much of it is self-explanatory

Then the last part is with using a custom agent in Copilot Studio which can be integrated with ServiceNow using custom integrations using connectors. While Copilot Studio can also use MCP Servers we are still waiting for the official one from ServiceNow, hence I need to use the built-in ones from Microsoft. Of course these agents can be used to anything, but here the main goal is to just use it to interact with incidents.

We also have one final option which is the use of Now Virtual Agent within Copilot 365. This means that the logic behind the agent and orchestration and integrations are handled by Service Now and that the UI part is only visible within Copilot 365. This uses adaptive cards in Teams so that you can use it to order catalogue items for instance directly from Microsoft Teams.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/11/image-5.png?resize=755%2C553&ssl=1)

This means that is directly communicating with Service Now. But this requires that you have both Now Assist and Copilot 365 licenses.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/11/image-6.png?resize=884%2C555&ssl=1)

To try and summarize things and showcase the different options I tried to add all the features and capabilities into this table

### **Summary Comparison: MCP vs Copilot 365 vs Copilot Studio vs ServiceNow Virtual Agent**



* Capability / Feature: Independence
  * MCP (Model Context Protocol): Independent of product and licensing (Uses mostly RestAPI)
  * Copilot 365 (Graph Connector): Extends Microsoft 365 only
  * Copilot Studio: Independent of Copilot 365 (separate license)
  * ServiceNow Virtual Agent: Requires ServiceNow Now Assist + Copilot licenses
* Capability / Feature: Primary Purpose
  * MCP (Model Context Protocol): Simplifies integrations across systems
  * Copilot 365 (Graph Connector): Enriches Microsoft 365 with ServiceNow data
  * Copilot Studio: Build custom copilots & integrations
  * ServiceNow Virtual Agent: AI-powered ServiceNow agent for workflows & case handling
* Capability / Feature: Customization
  * MCP (Model Context Protocol): Limited customization
  * Copilot 365 (Graph Connector): Only supports lookup, not executing tasks
  * Copilot Studio: Can use connectors and custom integrations
  * ServiceNow Virtual Agent: Can trigger workflows, agents, and other data sources
* Capability / Feature: Integrations
  * MCP (Model Context Protocol): Supported by most major vendors
  * Copilot 365 (Graph Connector): ServiceNow data only (Knowledge, Tickets, Catalogue)
  * Copilot Studio: Some ready-made connectors, rest must be built via REST/MCP
  * ServiceNow Virtual Agent: Integrated into ServiceNow ecosystem
* Capability / Feature: Data Handling
  * MCP (Model Context Protocol): —
  * Copilot 365 (Graph Connector): Continuous indexing into Microsoft 365
  * Copilot Studio: —
  * ServiceNow Virtual Agent: Data and tasks controlled within ServiceNow
* Capability / Feature: Licensing Impact
  * MCP (Model Context Protocol): No license dependency
  * Copilot 365 (Graph Connector): Microsoft 365 Copilot required
  * Copilot Studio: Requires Copilot Studio license
  * ServiceNow Virtual Agent: Requires Now Assist + Virtual Agent + Copilot license
* Capability / Feature: Key Limitations
  * MCP (Model Context Protocol): Not as flexible for deep customization
  * Copilot 365 (Graph Connector): Lookup-only, no action execution
  * Copilot Studio: Some integrations missing – must be custom-built
  * ServiceNow Virtual Agent: ServiceNow-centric, not cross-platform like MCP
