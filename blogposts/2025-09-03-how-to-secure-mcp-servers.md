# How to secure MCP Servers? - msandbu.org
While many have implemented MCP servers, not that many look at how to centrally manage and secure them.

The issue with many MCP servers is that they are developed by the community, where we have limited control over changes and whether there are any hidden prompt injections, where the MCP server might have some hidden instructions stored.

These MCP servers can simply be triggering remote API calls, but some of them can also be used to execute code locally on your own machine. We now also have MCP servers that can use the computer-use API to “control” your browser or machine.

For instance, this MCP Client for Windows PowerShell can execute code locally https://devblogs.microsoft.com/powershell/preview-6-ai-shell/

What if someone added malicious content to an MCP server that triggers a malicious command locally on your device?

Since the initial release of MCP back in November last year, there have been numerous updates to the specifications of the protocol, such as support for Remote MCP servers and OAuth support, meaning that these MCP servers are no longer limited to running locally on your own computer. This allows you to set them up centrally.

But how? MCP can be used in different ways, but the two main ones are:

• Through an Agent  
• Directly by a user from an MCP-enabled client

From a user, he or she sends a prompt to an MCP client (such as CLI, Claude, or VS Code) or other supported MCP clients. The MCP client needs to use context from the LLM to verify if it needs to trigger an MCP tool.

Which MCP tool is triggered depends on the description of the tool. Before the MCP client triggers the remote action, it needs to authorize the request if the MCP server has been configured with OAuth authentication.

Once the authentication process is complete, the MCP client will trigger the action against the MCP server.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/09/image-5.png?resize=529%2C466&ssl=1)

The other part is where the MCP client is an agent, which can be done trough agent platforms like Copilot Studio. As seen in the example below, I have a MCP server added to my agent in Copilot Studio.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/09/image-6.png?resize=908%2C282&ssl=1)

If you are using MCP through an agent, it will automatically limit what kind of access or actions it can trigger. If you are using a framework like Copilot Studio, it also limits MCP support to only supporting tools, and since it is running in a sandboxed environment, it limits how much “harm” it can do.

However, if you are trying to make MCP servers available to end users in a controlled manner, how do you do this?

Enter the MCP Gateway!

The MCP/AI Gateway is a component between the MCP Client and the MCP Servers, and is quite similar to an API Gateway. While the MCP Gateway is still in its infant stages, these gateways can have several features depending on which on you use.

Most MCP Gateways allows you to centrally configure which MCP servers should be available for your organization and allows for easier configuration and deployment of MCP configuration. This also means that users can only the ones that are distributed centrally instead of having a long list of multiple servers in their own MCP configuration.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/09/image-11.png?resize=644%2C332&ssl=1)

While there are many of these MCP Gateways available already, ill explain some of them.

*   IBM Context Forge https://github.com/IBM/mcp-context-forge (Is a open-source alternative) that can be used to create virtual servers where you can define a set of different MCP servers and define which MCP tools/resources that should be made available to your end-users.
*   Cloudflare AI Control – Cloud based offering as part of their Zero-trust ecosystem, that also allows you to control access trough a feature they called MCP Server Portals.
*   AgentGateway – another open source alternative that also provides LLM routing https://agentgateway.dev/

And I know that more and on their way, even Microsoft is working on something here as part of API management. However let us take a closer look at Cloudflares service.

Firstly I need to create a MCP server, which is pretty simple by just pointing to the URL of the deployed MCP server

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/09/image-13.png?resize=518%2C219&ssl=1)

Once the server is deployed, Cloudflare will connect and list the different tools/resources available to the MCP server

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/09/image-14.png?resize=1024%2C208&ssl=1)

Once we created a MCP server, we can add it to a MCP server portal and then assign different access policies.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/09/image-15.png?resize=762%2C333&ssl=1)

Once I am done with the configuration of the access policy I can go into the MCP server portal and download my MCP configuration, which in my case I will add to Claude which I am current using as my MCP Client.  

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/09/image-16.png?resize=475%2C184&ssl=1)

Once I add this configuration and reload MCP settings, it will trigger the MCP client to start an Oauth authentication to the MCP server.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/09/image-17.png?resize=572%2C354&ssl=1)

Once I have successfully authenticated it will list the available tools from my MCP server configuration in my client.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/09/image-20.png?resize=700%2C432&ssl=1)

Using this approach with a MCP Gateway I can control centrally which MCP servers that users can access. However this does not stop someone from altering their client to talk to another MCP server. This is one thing that is currently missing, since there are many supported MCP clients at the moment, and we do not have a standardized way of managing these clients (yet..)

One thing that can be used to detect the use of different MCP servers in your organization can be using Defender for Cloud Apps, but to block and restrict these settings is currently a missing puzzle.
