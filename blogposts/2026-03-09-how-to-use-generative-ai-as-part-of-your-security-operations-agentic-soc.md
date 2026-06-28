# How to use Generative AI as part of your Security Operations? - Agentic SOC - msandbu.org
While there are many articles that explore how a SOC or people working within IT security should start using Generative AI or virtual agents as part of their role, few actually explain how do to this in practice. Therefore I wanted to write this article as a part of my upcoming talk at Microsoft Sentinel Day where I will explore this in a bit more detail and wanted this post to be a summary of sorts of the talk.

Firstly, this blog will focus on three parts.  
1: The “Foundation” which are the LLMs that make this possible, a bit about their development, which ones are the best currently and some of the differences between them.  
2: The “Workbench” how we can utilize new tools and capabilities like Visual Studio Code + Github Copilot + MCP + CLI + Skills and Agents to help us understand, guide or even solve security incidents  
3: The last part is purely on “Automation” how we can now create runbooks in Logic Apps combination with Agentic loops (making the playbooks more act like a virtual agent) to solve tasks on their own.

The foundation
--------------

The foundation in all of this and what makes it possible it because of the innovation that has happened within Generative AI the last years. Since the release of ChatGPT a little over 3 years ago we have seen large improvements in these language models. Just to name some of the major improvements.

*   **Insane Efficiency:** Costs are down **99.9%** for token inferencing
*   **Reliability Level-Up:** Thanks to RAG, hallucinations have dropped by **90%**.
*   **Massive Scale:** Models now handle **500x more data** and even up to **1.5 hours of video**. (Such as the early days with ChatGPT it only supported 3500 words, now with GPT 5.4 it supports close to 750.000 words.
*   **Run Anywhere:** With **10,000+ models** available, you can run AI on your phone, PC, or the cloud.
*   **Better Communication:** New standards like **MCP/A2A** are changing how agents talk to each other. We also have standards coming like MCP Apps or WebMCP.

The “Big Three ” (OpenAI, Google, Anthropic) are still leading the pack, but “underdogs” like Mistral, Qwen, and Deepseek are closing the gap and also focusing more on open-source based models. It should also be noted that even if these new LLMs can handle more information it is still not “that much” information, it is only equivalent to the same as 4 floppy disks… (750,000 words)

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/image-4.png?resize=434%2C410&ssl=1)

It is also important to note that there is no LLM that is best at everything! while the difference in some of the areas are small, they have different strengts. Some excel at running as virtual agents, some at code developing, some at handling security context, parsing log content.

### **The Best Tools for the Job** (7 March 2025)

*   **Coding & Accuracy:** GPT 5.4 Codex xhigh.
*   **Agents & Security:** Claude Opus 4.6.
*   **Reasoning & Multimodality:** Gemini 3.1 Pro Preview.
*   **Large datasets:** Grok 4.1 Fast (while not as accurate)
*   **Local Infrastructure:** Kimi K2.5 and Qwen 3.5

It should be noted that these change whenever new models are relased, and you can see the benchmarks to compare these language models across different areas here –> https://artificialanalysis.ai/

But another example to highlight just how good these LLMs have become, I want to highlight this statement from Anthropic and Mozilla where they tested out Opus 4.6 against the source code of Firefox to see if they detected any vulnerabilities. In 2 weeks, they found 22, and ~1/5th of all high severity CVEs in a year…

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/image-1.png?resize=1024%2C576&ssl=1)

The Workbench
-------------

My workbench for many of my tasks consist of Visual Studio Code + Github Copilot that gives me access to different LLMs (both cloud but can also run local models trough Ollama) Then integrations are often trough MCP (Model Context Protocol) where we now have many more MCP servers available from Microsoft (Sentinel Data Lake + Defender + Entra ID) but also we can create our custom MCP servers trough Logic Apps and also many many 3.party MCP servers as well.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/Bilde-07.03.2026-klokken-21.30.jpeg?resize=1024%2C542&ssl=1)

We can also access 3.party systems trough regular CLI or custom scripts that run API. As long as the VS Code can run it, it can access it. The other part is knowledge, which can be documentation, ITSM systems or even Microsoft 365 where your data resides. This is helpful so that your agent or session can find “How did we solve this incident before?” “What our routines and processes for these cases?”

The last part is configuration, how do we want the workbench to function. Using Skills, agents and custom instructions. This is using local configuration files that VS Code is reading to apply its own configuration at start.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/image.png?resize=1024%2C370&ssl=1)

To give you an idea about a structure you can use this Github Repo which contains examples of all of these –> https://github.com/msandbu/sentinelday.

Also to explain a bit what skills is, think about them as a cookbook with different recipes. You know you have a cookbook, you know the recipe for pie is there but you do not remember all the details in your head. Skills work exactly the same way, when you need to do something specific the agent or the session will try and find a specific skill to help them solve the task and then it loads the information into the context. It should be noted that the “accuracy” of using skill can be a bit lower then just specifying it directly or using agents.md files which you can read more about here –> https://vercel.com/blog/agents-md-outperforms-skills-in-our-agent-evals

You can also see these predefined skills from Microsoft as an example –> https://github.com/MicrosoftDocs/Agent-Skills or this on Entra ID https://graph.pm/getting-started/introduction/

Once we have this in place, we can use our “workbench”. Here we have an session, where I asked to to check the latest Sentinel incidents and determine which I should focus my efforts on. It fetched the latest incidents (using MCP) it determined that there were to major things happening “Impossible travel” and “brute force” it also mocked me for having a weak analytics rule, in which I agree… Then it noticed that my brute force attacks and checked one of the more malicious IP addresses and added it to an NSG rule.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/image-2.png?resize=1024%2C596&ssl=1)

Within this workbench I am also using the latest GPT-5.4 LLM trough Github Copilot, which unfortunately restricts a bit how many tokens that I can use. Since traffic is being sent trough the Github Proxy, I am limited to 272.000 tokens. I also want to highlight how fast things are moving! that by default in visual studio code it needs to ask me for permissions for each “action” that It need to take such as run CLI command to complete something, however last week Microsoft introduced an “autopilot” feature where you are automatiaclly approving all actions.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/image-5.png?resize=488%2C286&ssl=1)

Probably not a good idea from a security perspective, but still pretty interesting!

Another part is when it comes to adding your own knowledge, data or documentation there are several ways to add this. Many of the main ITSM systems such as Jira, Service Now and others have their own MCP servers which can in turn be used to search for knowledge there trough RAG (Retrieval Augmented Generation) if you use Microsoft 365 Copilot you should use WorkIQ MCP (https://github.com/microsoft/work-iq) servers. Another approach is to use Azure AI Search + Embedding models from Azure OpenAI. Azure AI Search can connect to many different data sources and using the embedding LLM to vectorize data and store it in a AI search vector index.

Azure AI Search also supports agentic retrieval, which allows the service to rephrase incoming questions or prompts to ensure a higher likelihood of finding relevant information.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/Bilde-08.03.2026-klokken-22.52.jpeg?resize=1024%2C673&ssl=1)

Now when setting up your “workbench” with these different tools such as MCP, RAG and CLI access there are some things that you should take note of!

Takeaways: Implementing and Scaling MCP
---------------------------------------

### 1\. Authentication and Governance

*   **OAuth as Standard:** Use OAuth for secure authentication when connecting to MCP servers. Most servers from Microsoft uses this, it allows you to authenticate on behalf of your user account.
*   **Centralized Control:** Manage access either individually or centrally via an **MCP Gateway** (e.g., using API Management or Context-Forge). This simplifies the infrastructure by acting as a single entry point for context. I have written more about MCP Gateways here –> https://msandbu.org/optimizing-developer-experience-with-ai-and-mcp/

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/image-6.png?resize=718%2C304&ssl=1)

### 2\. Scaling Limitations and Efficiency

*   **The 128-Tool Limit:** Avoid exceeding **128 tools** within a single MCP instance to maintain performance and this also ensures accuracy of the models.
*   **Token Optimization:** Historically, MCP is “token-hungry.” However, newer models (like GPT 5.4) have addressed this through **Tool Search**, significantly improving how the model identifies the right tool without exhausting the context window. But ensure that you having the “right tools” enabled makes it easier and quicker for the agent to find the right tools for the job.

### 3\. Developer Experience (DevEx)

*   **Cloud-Native Development:** Utilizing a **centralized repository with GitHub Codespaces** ensures a consistent, pre-configured environment for developers working on MCP integrations.
*   **Instruction Accuracy:** Moving from `Skills.md` to an **`Agent.md`** approach results in higher accuracy and better alignment for the AI agents –> https://vercel.com/blog/agents-md-outperforms-skills-in-our-agent-evals

### 4\. MCP for Data Lakes

*   **Time-Sensitive Queries:** When using MCP server for Data Lake, it is important to ensure `|TimeGenerated` is included in the prompt to filter data correctly, if not it can by default get ALL the data which can be quite cost generating if you have a lot of data.

Then we have building our own custom MCP Servers! Firstly there are a few things you need to have to expose a logic app playbook as an MCP server

1: HTTP Request (With a description) + JSON Schema that contains the input you want to have.  
2: Any type of action that can be used with the input (In this case I have a Kusto Query Logic App – Where my input is just the KQL)  
3: HTTP Response with my desired output.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/image-7.png?resize=1024%2C706&ssl=1)

Once I have created the playbooks I need to expose them trough the MCP server configuration pane in Logic Apps where I group the playbooks I want, give a description of the MCP servers

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/image-8.png?resize=798%2C320&ssl=1)

Lastly I copy the URL which I need to have to add it to my MCP configuration in VS Code, it will usually look like this

```
},
"nameofmyserverinconfig": {
"url": "https://logicapp.azurewebsites.net/api/mcpservers/name/mcp",
"type": "http“
},

```


Which can then be triggered from the Github Copilot or an agent by asking “Run this Kusto Query” While it does not sound super impressive, since that can easily by done directly in the portal, but this gives an agent the ability to check for different tasks directly.

Automation with Agentic Loops
-----------------------------

The last piece is the pure automation part. Having virtual agents the ability to handle incidents directly with predefined tools or even other MCP servers using Logic apps agentic loops.

Agentic Loops are only supported in standard workflows in Logic Apps and only supports Azure OpenAI (Not Foundry) meaning only OpenAI models. In this example screenshot shown below I define a security incident trigger where certain sets of information is being sent down to the Agent. The agent has a predefined set of instructions and is given some tools they it can use to “solve” the task based upon the instructions.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/image-9.png?resize=1024%2C463&ssl=1)

Then for each tool I define its own instructions on when it should be triggered and I define a parameter which contains a “conclusion” to the case, here again description is important since it gives the agent instructions on what kind of information should be contained here.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/image-10.png?resize=1024%2C982&ssl=1)

The last part here is for the agent to use this conclusion to add a comment to the incident.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/image-11.png?resize=1024%2C724&ssl=1)

The other tool I have, is where the agent comes to the conclusion that it is a false positive and closes the alert by itself, as seen in the screenshot below.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/image-12.png?resize=984%2C1024&ssl=1)

Now there are some other important new capabilities in Sentinel that use GenAI as well. Firstly is the Entity Analyzer (Where the data lake is a prerequisite) but this is available trough Logic App playbooks (as part of the content package for SOAR essentials) but Entity Analyzer is essentially a custom wrapped GenAI package to check different entities such as URL or User account. This is especially useful when you want to monitor impossible travel alerts and need to analyze a wide range of different logs, but now its a simple Logic App that does the heavy lifting and updates the incidents. You can read more about it here –> https://techcommunity.microsoft.com/blog/microsoft-security-blog/announcing-ai-entity-analyzer-in-microsoft-sentinel-mcp-server—public-preview/4476230

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/image-13.png?resize=1024%2C311&ssl=1)

And lastly, Microsoft has recently introduced a Playbook Generator feature, which is only available from the Defender portal under the automation pane, but unfortunately it requires Security Copilot.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/03/image-14.png?resize=534%2C356&ssl=1)

A summary of sorts..
--------------------

Hopefully this gave some context on how you can build a modern workbench using VS Code + Github Copilot with addons and also showcased how you can use Agentic Loops and Entity Analzyer to provide more GenAI Automation into your SOC plattorm in Microsoft.

It should be noted that my example workbench is not the replacement for a good case management system, since it requires some multitasking to find correct incidents and go back and forth between the portal and if you are “flooded” with incidents on a daily basis adding capabilities like this only makes the multitasking worse. Therefore it is important to start with the automation pieces to reduce the load and get better control before you start making large changes to the workbench. However using this new toolbench to write summarizes / reports / statistics is a great way to use them, and also to get a better understanding when you have something you cant explain that has happened.
