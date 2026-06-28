# Optimizing Developer Experience with AI and MCP - msandbu.org
Recently I got tasked with looking into how one can build the an AI-infused developer experience. What would it look like? How to have centralized services with MCP, Skills, Tooling, Data and workloads that could be centralized and easily distributed across different enviroments. I also wanted to provide access to agents that developers could use in different services, but also ensure that they only use approved services.

**So does it include?**  
**– MCP Gateway (To provide a centralized set of MCP Servers and tools that I want to have available)  
**– Standardized** System Prompts (Using SKILLs.md)  
– **Predefined set of LLMs to use** (based upon benchmarks (Quality, Accuracy)  
**– RAG Services to make** documentation/information easily available  
**– Common set of Tools** (IDE, Agent frameworks)  
**– Access to run local LLMs** on Developers machines.  
**– Standarized Agents** running on Github

Skills
------

Firstly we have Skills, which are a folders of instructions, scripts, and resources that Copilot (Supported in the latest Visual Studio Code Insider –> https://code.visualstudio.com/insiders) loads dynamically to improve performance on specialized tasks. The great thing about skills instead of having a large set of instructions, is that Copilot can load these on-demand when needed, instead of cluttering the system prompt. This mean that instead of cluttering your system prompt with 5000+ tokens, Copilot only read the metadata from the YAML context to load the skills. You can view a bunch of examples here from Anthropic –> https://github.com/anthropics/skills/tree/main/skills

Skills can also define which tools they can use such as MCP servers to complete a task, but ill get back to that once we look at the structure. Firstly if we want to use this in Copilot with VSCode I need to set this flag first **“Use Agent Skills”**

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image.png?resize=1024%2C433&ssl=1)

So here in my repository I have two defined skills “market-researcher” and “security-engineer”

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-1.png?resize=572%2C266&ssl=1)

Here is an extract of security-engineer SKILL.MD

```
---
name: security-engineer
description: Expert infrastructure security engineer specializing in DevSecOps, cloud security, and compliance frameworks. Masters security automation, vulnerability management, and zero-trust architecture with emphasis on shift-left security practices.
tools: Read, Write, Edit, Bash, Glob, Grep
---

You are a senior security engineer with deep expertise in infrastructure security, DevSecOps practices, and cloud security architecture. Your focus spans vulnerability management, compliance automation, incident response, and building security into every phase of the development lifecycle with emphasis on automation and continuous improvement.

When invoked:
1. Ask the User if they have contact their IT security person? 

```


When I ask the agent to do some vulnerability management I can see that Copilot loads the Skills.MD file and asks me the following as according to the instructions

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-2.png?resize=572%2C424&ssl=1)

Pretty simple, and eventually you will have a long list of these skills that are being produced. I recommend that you have a centralized repository where these are stored so that everyone can build/improve/use these skills.

But this should be in addition to any personal instructions that you might have. Where you can define tone of voice, language if it should be simplistic or not. Some overall guidelines that should be used regardless of which skills that are being used.

Copilot Configuration
---------------------

Much of this is done trough Github – But this allows us to define policies for how Github Copilot should be used including language models and such. Where I firstly define which LLMs that are allowed to be used.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-3.png?resize=1024%2C486&ssl=1)

For Coding I tend to use Opus 4.5 – For Deep Reasoning Gemini 3 PRO and the same if I want to use for visual content such as images. Gemini also has best accuracy when it comes to large context. You cannot define which model you should use within Skills, so you need to switch it in Copilot.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-4.png?resize=510%2C754&ssl=1)

I also enable most capabilites for Code Review, Commit Messages. If there is specific content that I do not want Github Copilot to have access to I have to define it in Github Settings (But I should be noted that GitHub Copilot CLI, Copilot coding agent, and Agent mode in Copilot Chat in IDEs, do not support content exclusion)

I also often define custom modes in Copilot such as defining agents that I want to work in the background, where I have instructions and defined models in place, while Skills we cannot define models we can however do with specific modes. If you have a specific and personal workflow I tend to have these as well.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-5.png?resize=518%2C176&ssl=1)

Within these markdown files, you get a custom mode in the chat window as seen here.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-6.png?resize=518%2C572&ssl=1)

This is the content in the markdown file that I use to describe the agent.

```
description: This mode is used for requirement definition tasks.

tools: ['changes', 'codebase', 'editFiles', 'fetch', 'findTestFiles', 'githubRepo', 'new', 'openSimpleBrowser', 'runCommands', 'search', 'searchResults', 'terminalLastCommand', 'terminalSelection', 'usages', 'vscodeAPI', 'mssql_connect', 'mssql_disconnect', 'mssql_list_servers', 'mssql_show_schema']

---

# Requirement Definition Mode
In this mode, requirement definition tasks are performed. Specifically, the project requirements are clarified, and necessary functions and specifications are defined. Based on instructions or interviews with the user, document the requirements according to the format below. If any specifications are ambiguous or unclear, Copilot should ask the user questions to clarify them.

## File Storage Location
Save the requirement definition file in the following location:
- Save as `requirement.md` under the directory `docs/[subsystem_name]/[business_name]/`
```


This means that I can use /delegate command to allow the agent to process and do the defined tasks in my content.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-7.png?resize=578%2C270&ssl=1)

LocalLLMs
---------

If you want to work with Local LLMs using VS Code then I recommend either using Cline as extension (Which supports Ollama or LMStudio) or Continue extension that also supports autocomplete using local LLMs. Note that here I recommend that you use Qwen-3 Coder model which comes wiht 30B parameters, but only 3.3B active parameters, which means that you should have atleast 7 GB of vRAM either on GPU or NPU that can handle the load.

Here is the configuration of Cline

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-8.png?resize=578%2C808&ssl=1)

In order to provide a set of predefined MCP servers you should deploy an MCP Gateway, that allows you to have a centralized configurasjon of MCP servers where you can define which tools and resources that should be available.

While there are already a lot of different provides out there, such as Obot, IBM Context-Forge, Cloudflare MCP Portal and vMCP. However many of them are lacking basic functionality such as the ability to create virtual MCP servers and defining which tools that should be available for each set of users or group. I think that the new version of IBM Context forge which is open-source is currently the one with the most features

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-10.png?resize=1020%2C458&ssl=1)

This also allows us to centrally add MCP servers with predefined authentication to different services, the problem is that many tools can be accessed trough a specific service principal instead of each user having their own user account. This Gateway also allows us to have predefined tools available, instead of each developer needing to specify which MCP tools they need to have access too. Since there is a limit of 128 tools (and server like Azure) has 40 tools built-in the limit can be reached quite quickly. Therefore having virtual MCP Gateways allows this to scale. However to be honest, it is important to note that these gateways are not mature yet.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-11.png?resize=571%2C233&ssl=1)

I also created my own custom MCP servers for components where we didnt have any native features available using Logic Apps with MCP support as I have written about here –> Copilot Studio Agents with MCP using Logic Apps – msandbu.org

However there are some MCP servers that use STDIO which can only run locally (unless you use a proxy) such as Azure DevOps, but it allows me to query work items, knowledge articles.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-17.png?resize=631%2C544&ssl=1)

And for VS Code there is already a MCP registry that allows you to easily set up these servers (but only local) and not trough a gateway.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-18.png?resize=1024%2C707&ssl=1)

Speckit
-------

Skills, local agents, and Speckits each shine in different parts of the workflow. **Skills** are like handy tools you can grab on demand for specific actions – “do X with this input” – and they don’t really care about the bigger picture. Local agents are more like focused teammates: you point them at a well-defined area (frontend, data cleanup, docs, etc.), and they use those skills to get a particular kind of job done. **Speckits** sit one level higher and they help you go from “here’s what we want” to concrete specs, break that into tasks, and keep track of how your thinking and requirements change over time, almost like version control for your reasoning, not just your code.

Speckit from Github can be enabled using this via CLI

```
uvx --from git+https://github.com/github/spec-kit.git specify init projectname
```


Once you run the command you specify which code agent, which will create a folder structure and define some agent configuration

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-12.png?resize=759%2C426&ssl=1)

As seen in the folder structure here.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-13.png?resize=873%2C723&ssl=1)

Then I define /specify and define what the desired outcome I want to get

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-14.png?resize=309%2C269&ssl=1)

Then it starts to create the requirements for this service or feature that I am building. That add user-stories, test scenarios, feature requirements. It’s worth noting that as you are using the slash commands that Specify injected into the project, having a **very detailed first prompt** will produce a much better specification that the agent can use for further project build-outs.

Copilot Coding Agent
--------------------

Then we have Copilot Coding Agent. This is distinct from the “agent mode” feature available in VS Code. Copilot coding agent works autonomously in a GitHub Actions-powered environment to complete development tasks assigned through GitHub issues or GitHub Copilot Chat prompts, and creates pull requests with the results. Copilot coding agent uses Claude Sonnet 4.5.

These Coding Agents can also use tools such as MCP and by default has access to use Playwright and Github MCP server. That means that all tools that are available trough the Github MCP Server can be triggered by the Coding Agent. These agents can either be triggered manually trough a pull request, issues that are delegated to it or manually in the portal.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-15.png?resize=650%2C499&ssl=1)

The cool thing is that you can have multiple of these agents that can be configured. Just as these security review agent create a pretty good overview. All agents create their own pull-request with new content or markdown files.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-16.png?resize=945%2C511&ssl=1)

And given that they use the MCP server built-in that also means that they can be used to do different tasks within Github. These agents are described as markdown files as well under /.github/agents such as securityreview.md. The markdown file needs the following description.

```
name: Security-reviewer 
description: This checks at security issues with the code
---

# My Agent

This Agents checks the security of the code in the repository and creates Github issues for each security issue that it finds. 
```


You can also delegate issues to these agents directly

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-19.png?resize=1024%2C318&ssl=1)

Summary
-------

So what did we end up with?

We ended with a developer IDE that combines the use of skills/agents/local LLMs with MCP servers using Remote Gateways and local for other needs, but also uses agent mode in Github to write README files, do security code review but also plan sprints using speckits. While much of this is still evolving from time to time, the ecosystem has gotten to a point where it can provide real value, if you use it properly.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-20.png?resize=784%2C704&ssl=1)
