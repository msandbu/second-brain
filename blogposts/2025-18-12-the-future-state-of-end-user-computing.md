# The future state of End-User Computing - msandbu.org
This is a long overdue blog post focusing on what I believe will be the future state of the EUC, and is essentially a summary of a session I did at EUC Denmark back in March.

The current state:
------------------

When I am talking with customer these days I see much of the same topics being discussed.

*   Many organizations struggling with combining old and new technology, constant changes.
*   Wanting to solve and have a simple secure access (ZTNA)
*   Navigating all changes from the different vendors
*   Cyber security
*   Limited insight into user-experience (but most do not want to pay for it)
*   AI Fomo – Many want to see this as an oppurtunity to make it easier and save time.

And yes EUC is big and complex ecosystem, if we just look into this EUC Hexgrid from Dizzion, you can see most of the vendors in this ecosystem and most organisations have many of these products. Which is a good indicator of how complex it has gotten.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/07/image-11.png?resize=333%2C369&ssl=1)

Now with all the changes happening within AI, this is not going to make it any easier, since we see even MORE changes happening there on a yearly basis.

GenAI Evolution:
----------------

Let u stake a closer look at the Gen AI Evolution and how this will impact the end-users both from a usage perspective but also how we will see this more and more running directly on the users devices.

When we look at the evolution of GenAI the last 3 years, there has been so many improvements! (and this is not taking into account all the updates the last 3 weeks) with introduction of GPT 5.2, Gemini 3 Pro and Opus 4.5.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/07/image-10.png?resize=652%2C424&ssl=1)

We now have models that have gone from only being able to process 3500 words to now experimenting with 5 million words. The quality, performance and now with «pure» multimodal models can do thing that were nowhere possible two years ago.

We also now have new protocols that will make it easier to create integrations between LLMs and 3.party services such as MCP and A2A

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/07/image-9.png?resize=1024%2C666&ssl=1)

Microsoft has already built a new set of services called Copilot Runtime for Window that allows Window to run LLMs locally but have also brought MCP protocol natively to the OS, which will allow it to interact with 3.party services using the MCP protocol.They have also introduced a lot of new OS capabilities both to do Agent orchestration but also built-in “AI actions” that use local LLMs on the device.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/07/image-12.png?resize=1024%2C483&ssl=1)

They even added MCP support in Microsoft Teams which means that much of these standard integrations will allow us to publish «tasks and actions» instead of apps and using natural language trough Teams or another UI.

Also if you buy a Copilot+ PC today, you get a computer with a dedicated NPU (AI-chip) and an OS preloaded with different LLMs such as a Phi-3 and DeepSeek.

Of course one thing we will see much of in the future are **Agents, Agents everywhere!** And no wonder since all the cloud providers are building their own ecosystems and every ISV is trying to build their own agent.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/07/image-14.png?resize=1024%2C593&ssl=1)

So we need to be careful of agent sprawl, which platform or product should we standardize on? We already have different AIOps Agents available to us from different platform such as NowLLM from Service Now and agents from Microsoft such as the Azure SRE Agent

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/07/image-9.png?resize=1024%2C666&ssl=1)

GenAI is going to impact (and already has) the way that we work. Both how we consume it on a personal level (Copilot, Gemini, ChatGPT) but also on a business level with agents, RAG services or others.

It will also impact the way that we work on IT operations with custom agents that will troubleshoot things for us.

Big changes the last year
-------------------------

Of course in addition to all the stuff happening within GenAI, there has been a lot of announcements from the different vendors.

*   Big shake-up with the VMware/Broadcom changes
*   License cost changes
*   Many dicussions around cloud-exit
*   More developer focus on VDI

So let us go trough some of them, firstly is that Omnissa and Citrix are expanding their platform support. Citrix even introduced support for OpenShift and Omnissa announced a partnership with Nutanix now that they are no longer part of VMware.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/07/image-13.png?resize=1024%2C551&ssl=1)

I see that many are now looking into alternatives to VMware because of the license changes. Microsoft however are still only focused on supporting Azure Local, even if their product can technically work on other platforms.

Microsoft is doing a lot of improvements to both Windows 365 and AVD

*   Enhanced Host pool management for AVD
*   Window 365 for Frontline workers
*   App-V integrated into AppAttach
*   New AppAttach (support for Entra ID)
*   Hardware Acceleration for H.265 (Preview)
*   Global Turn Relay support
*   Unidirectional clipboard
*   New AMD vGPU SKUs
*   Azure Files with Metadata caching
*   Improvements for Premium Disks Azure
*   New Windows App for Remote Access (supports Token Protection)
*   Windows Link (a new thin client that ONLY supports Windows 365)

However Citrix have also done a lot of improvements and have also aquired a lot of companies the last year to improve their core portfolio.

*   Aquired Unicon (thin client vendor) DeviceTrust (Contexual Conditional Access) and Strong Networks (Developer based workspaces)
*   Support for Nutanix Prism
*   Session Remote Start (starts a workspace when a users stamps their employee card at the door)
*   Intune and Entra ID Joined MCS Catalogue
*   Boot to desktop with Linux Workspace App
*   Integration with Device Posture from Linux App
*   Azure GPU Hibernation support
*   Cost modelling for Azure support
*   UberAgent now part of the Citrix VDA
*   Citrix also entered into a partnership with Google Chrome Enterprise (while Omnissa is of the few partners with Microsoft on their new Edge for Business)
*   H.264 and H.265 hardware decoding Linux
*   H.264 for seamless apps
*   AV1 Codec
*   Intelligent Build to Lossless feature
*   EDT MTU Discovery
*   Audio Quality Enhancer

So there area lot of improvements to the HDX Protocol itself, and one could ask themselves, does the protocol actually matter anymore? And the answer is yes…

Just look at this recent protocol performance benchmark from Julian Jakob that showed a big difference between AVD and HDX.

While VDI or a cloud PC is one way to access internal resources, we also have the other aspect of «other» services which can require regular TCP/UDP or even internal web applications that you need to access.

The last year we have been riddled with high severity vulnerabilities on remote access services such as VPN providers (Fortinet, Ivanti) and now lately with Citrix Bleed 2.0 on NetScaler Appliances. Also many are looking to move away from regular VPN based access to more of a ZTNA based approach.

The problem here as well is that we have so many different vendors to choose from, and a ZTNA solution needs to integrate with other services such as EDR and iDP to get health signals. Another important thing here as well is the performance of the solution.

You do not want to implement a ZTNA service that is slower then your existing VPN solution? Even if it is more secure, your users are not going to care. Here we also have significant differences between the different providers, aka the protocol matters.

Here is an overview of some of the vendors in the market

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/07/image-16.png?resize=1024%2C551&ssl=1)

As I mentioned initially, the IT landscape within EUC is complex and to try and figure out if something is not working and why it is not working is like finding a needle in a haystack. More and also looking into DEX to measure the users experience and being proactive in terms of detection issues or if services are unavailable.

If Microsoft Teams or Exchange online has an outage I would like to know and be able to inform my end-users directly without them needing to contact help desk to get that information. The issue with most is that not everybody wants to pay for an additional product that can monitor this. While there are some features included in other products from Omnissa, Citrix and Microsoft they are nowhere as advanced as features from Nexthink and now with ControlUp.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/07/image-15.png?resize=1024%2C452&ssl=1)

What the future workspace will look like:
-----------------------------------------

So what will the future look like? I imagine something like (picture below..) this within a few years time, where we have more services and tasks becoming available trough agents in different shapes and forms. We will still have those legacy applications living side-by-side by the new ones.

Agents will be used either as part of business applications, stand-alone that are using for self-service or integrated locally on the device for certain tasks. So with all these moving parts and added complexity it might also push more businesses to add DEX to get the necessary insight into how things are actually going and if they are working or not.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/12/image.png?resize=800%2C481&ssl=1)

Still given the slow adoption of agents this year, I do not expect this to happen within the first 2 years but more towards 2029. While many ISVs are now embedding agents into the products and services, many are still reluctant and still do not see the value. But we can expect that the new LLMs that are coming the next couple of years can be even 2x as effective as the current ones and even cheaper and the framework surrounding GenAI as well will mature making it easier to adopt.
