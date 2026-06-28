# What does Anthropic Mythos ACTUALLY mean for Cybersecurity? - msandbu.org
These last weeks I have seen so many wierd blogposts and articles on Linkedin and other social media stating that Mythos is a GAMECHANGER and that we now have to rethink how we need to handle security, or that this is the first step to AGI and other similiar topics. Much of it is just pure BS, and many fail to grasp what it actually means. Therefore I want to try and share a few perspectives on this, which might be a bit more realistic and try to describe the advantage that Mythos has.

First of, let us look at the current state of LLMs. When we are looking at the development of the LLMs we have seen how they have improved quite significantly over the last two years. We saw a big jump going from 2024 – 2025, but the biggest impact was Desember 2025. The screenshot below is from the Artificial Analysis own intelligence benchmark, which combines multiple benchmarks to determine an overall “intelligence” of a model.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/04/image.png?resize=1024%2C611&ssl=1)

All these LLMs have also improved a lot when it comes to tasks related to OS navigation (OS-world) or tasks in CLI (Terminal-bench). Which allows the LLM to navigate and run tasks directly on a machine. They have gotten quite good and doing security code analysis (Cybergym) as can be seen in the screenshot below.

_Also Mythos is mentioned here as the LLM with highest success rate on Cybergym but I will get back to that._

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/04/image-1.png?resize=1024%2C571&ssl=1)

Source: https://www.cybergym.io/

Still it is important to note that most language models have limited amount of context they can process (similiar to what you can store on 4 floppy disks, approx 750,000 words in pure text).

Benchmarks alone do not say much about the actual quality of what these LLMs can do. Therefore I wanted to highlight what Daniel Stenberg (The creator of Curl) posted on Linkedin last week about vulnerability reports that he gets for Curl.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/04/1776326019183.jpeg?resize=1024%2C576&ssl=1)

That in the period 2020 – 2024, the average time between security reports were close to 110 hours, while now in 2026 it is closer to 20 hours.  
While the average tine in 2025 was also quite low, the issue was that it contained a lot of which Daniel himself described as “AI Slop”. However so far in 2026 there has been a change, where he now sees more quality vulnerability reports.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/04/1776326019276.jpeg?resize=1024%2C576&ssl=1)

This is what we see in this last picture where close to 17% of security reports contained a confirmed vulnerability, which is higher then it was in earlier periods and also given how much faster these security reports now come in where more of these are now AI assisted reports. Lastly when we look at the CVE statistics for the last years, we can also see that this is going in the wrong direction….

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/04/Skjermbilde-2026-04-17-kl.-23.28.09.png?resize=1024%2C512&ssl=1)

So we can see that more and more people are using LLMs to assist them in finding vulnerabilities. In addition, we now have multiple agent frameworks that allow LLMs to perform tasks directly against an application, such as clicking around a UI, navigating through a browser, reading source code, running commands in a CLI, writing code. So does this mean we can also use LLMs to carry out more offensive attacks and not just regular static code analysis?

And the answer is yes! Even now there are mulitple different open-source LLM Pentest agent frameworks such as Sharon (no I am not kidding) https://github.com/KeygraphHQ/shannon which uses mulitple agents combined with predefined skills to perform tasks. The problem is now that with this type of knowledge, the know-how to do pentesting is being democratizes (not at the same level as a experienced pentester), but Anthropics own approach when they tested Mythos was as simple as this..

> _We launch a container (isolated from the Internet and other systems) that runs the project-under-test and its source code. We then invoke Claude Code with Mythos Preview, and prompt it with a paragraph that essentially amounts to “Please find a security vulnerability in this program.”_  

So what is Mythos?
------------------

Claude Mythos (Which is an new frontier LLM) shows Anthropic’s move into more specialized, capability-dense model territory. While Anthropic has not released a full technical breakdown of its architecture (except the system card) Mythos demonstrates significantly hetter performance on tasks requiring deep technical knowledge in specialized domains specifically cybersecurity.

It has successfully found and exploit zero‑day vulnerabilities across major operating systems, browsers, and critical software—often without human guidance. Some of the things that Anthropic announced in terms of vulnerabilities that it found.

*   **A 27‑year‑old OpenBSD SACK bug.**
*   **A 16‑year‑old FFmpeg H.264 bug.**
*   **Browser JIT heap sprays** leading to cross‑origin bypasses and sandbox escapes and also several thousands of additional high‑severity vulnerabilities.

You can read more about the vulnerabiltiies that was discovered by Mythos in their blogpost –> https://red.anthropic.com/2026/mythos-preview/

Alongside these developments, Anthropic launched Project Glasswing, an initiative designed to give defenders early access to these capabilities before comparable models become broadly available. For now, the Mythos LLM is restricted to a select group of specialized partners who can evaluate it against their own software stacks.

It should also be noted that a few days ago, OpenAI released a fine-tuned version of GPT 5.4 called GPT 5.4 Cyber –> https://openai.com/index/scaling-trusted-access-for-cyber-defense/ but details on the model is still unknown.

So how much better is Mythos compared to the other “best” models available today?



* Benchmark: Cybergym
  * Anthropic Mythos: 83.1%
  * Anthropic Opus 4.7: 73.1%
  * Anthropic Opus 4.6: 66.6%
  * Google Gemini 3.1 Pro: 38.3%
  * GPT 5.4: 66.3%
* Benchmark: Terminal-Bench 2.0
  * Anthropic Mythos: 82%
  * Anthropic Opus 4.7: 69.4%
  * Anthropic Opus 4.6: 65.4%
  * Google Gemini 3.1 Pro: 68.5%
  * GPT 5.4: 75.1%
* Benchmark: OSWorld
  * Anthropic Mythos: 79.6%
  * Anthropic Opus 4.7: 78%
  * Anthropic Opus 4.6: 72.7%
  * Google Gemini 3.1 Pro: 
  * GPT 5.4: 75%
* Benchmark: SWE-bench Pro
  * Anthropic Mythos: 77.8%
  * Anthropic Opus 4.7: 64.3%
  * Anthropic Opus 4.6: 53.4%
  * Google Gemini 3.1 Pro: 54.2%
  * GPT 5.4: 57.7%
* Benchmark: GPQA Diamond
  * Anthropic Mythos: 94.5%
  * Anthropic Opus 4.7: 94.2%
  * Anthropic Opus 4.6: 91.3%
  * Google Gemini 3.1 Pro: 94.3%
  * GPT 5.4: 92.8%
* Benchmark: USAMO 2026
  * Anthropic Mythos: 97.6%
  * Anthropic Opus 4.7: 
  * Anthropic Opus 4.6: 66.2%
  * Google Gemini 3.1 Pro: 74.4%
  * GPT 5.4: 95.2%
* Benchmark: HLE (no tools)
  * Anthropic Mythos: 56.8%
  * Anthropic Opus 4.7: 46.9%
  * Anthropic Opus 4.6: 40%
  * Google Gemini 3.1 Pro: 44.4%
  * GPT 5.4: 39.8%


The benchmarks themselves show quite impressive advantage that Mythos has, particularly Cybergym where it clear has a bigger advantage over the other models at least at this time. The AI Security Institute (AISI) Our evaluation of Claude Mythos Preview’s cyber capabilities | AISI Work did its own evaluation of Mythos, where they did both capture-the-flag (CTF) challenges and more complex ranges designed to simulate multi-step attack scenarios.

On Advanced CTF challenges On expert-level tasks — which no model could complete before April 2025 — Mythos Preview succeeds 73% of the time.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/04/image-2.png?resize=1024%2C570&ssl=1)

So their initial conclusion so far:

*   **Significant Capability Leap:** Mythos Preview represents a major advancement in AI cyber capabilities. It can autonomously perform complex tasks that would typically take human professionals days to complete.
*   **Autonomous Multi-Step Attacks:** The model is the first to successfully complete “The Last Ones,” a 32-step simulated corporate network takeover. It finished the entire sequence in 3 out of 10 attempts, averaging 22 out of 32 steps.
*   **Current Limitations:** While powerful, the model struggled with operational technology (OT) environments. Furthermore, the testing environments lacked “active defenders,” meaning its effectiveness against high-security systems with real-time monitoring is still unproven.

When looking ahead with the current LLMs I believe that they are still bound today by compute capacity, given that they are now building new datacenters such as the largest 2026 facility (xAI Colossus 2) will have the compute equivalent of 1.4M H100 GPUs. The largest datacenter today has “only” 500k equivalent of H100 GPUs. For instance the new datacenter from Microsoft will deliver 10X the performance of the world’s fastest supercomputer today. Same also goes for OpenAI with their stargate initiative and are already in process of building out multiple new AI datacenters. I reckon that this will allow these tech companies to train and build more “frontier” models even faster.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/04/image-4.png?resize=819%2C1024&ssl=1)

### **The Mythos of Precision: Beyond the Headlines**

While Mythos shows impressive results, the “noise” remains a mystery. Anthropic reports an 89% agreement rate on severity, but we don’t know the false-alarm rate. Frontier models that are aggressive enough to catch every bug often “hallucinate” vulnerabilities in perfectly safe code.

This is a critical distinction: a model with surgical precision is a game changer, but a model that generates thousands of false alarms is a productivity sink that still requires a small army of human experts to verify the output.

### **The Training Bias Trap**

LLMs are products of their training data. Mythos works well at what it has seen most like the Linux kernel and popular web frameworks. While this helps major vendors patch common software, it leaves a massive blind spot. Software outside the “mainstream” such as industrial control systems, medical firmware, or bespoke financial infrastructure is exactly where Mythos is most likely to struggle out of the box. This can of course be “mitigated” with the use of Skills & RAG to point the model directly at the documentation of the system or framework.

### **The Force Multiplier Effect**

The real danger isn’t that Mythos might fail in niche domains; it’s that it succeeds for those who bring their own expertise. A motivated attacker with deep knowledge of a specialized field can use Mythos’s reasoning as a force multiplier. By combining domain expertise with AI speed, they can audit systems that even the model’s own creators wouldn’t know how to probe. The risk isn’t just AI autonomy; it’s the power it grants a specialist. In addition to this, with future frontier models, the multiplier effects will be even higher

### **Zero-Day Clock is close to the second**

A final comment…Now with attackers having access to frontier LLMs like Mythos, we have reached the threshold which Zero-Day Clock has predicted. The Zero Day Clock tracks how quickly vulnerabilities move from public disclosure to active exploitation.

The takeaway: the window between disclosure and weaponization is shrinking dramatically. What used to be months is now often days—or hours.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/04/image-5.png?resize=979%2C665&ssl=1)

They predict that within 2028, the mean time-to-exploit will be down to 1 minute. I reckon that with these new fronter models we will be down to that 1 minute before 2028. Do we still then have time to apply a patch to sort out a vulnerability before it is to late? probably not.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/04/image-6.png?resize=946%2C295&ssl=1)

A somewhat summary and what should businesses do?
-------------------------------------------------

So how are these LLMs going to impact the way that we work with IT-security? Firstly in many cases the answer to a vulnerability is installing a patch or other ways to mitigate/contain it. Secondly installing patches on some IT systems can be cumbersome because of contrains or because of internal processes (change processes, which can take time) and we are also dependent on waiting on the vendor to issue an patch. Security teams will most likely get overwhelmed by AI-discovered vulnerabilities, exploits and autonomous attacks in the near term. One should adjust risk calculations for higher patch volumes, shorter remediation windows, and more complex attacks anddouble down on fundamentals like segmentation, MFA, and defense-in-depth. Secondly Project Glasswing is the first iteration of Mythos-level capabilities which will soon be widely available, dramatically increasing attack frequency and complexity (such as with the release of GPT 5.4-Cyber.

It should also be noted that while vulnerability discovery capabilities comparable to Mythos have shown to be present through earlier AI models, the Mythos announcement has grabbed the attention of the CISOs/CIO and other C-level executives.

I recommend that you prioritize dependency management and embed automated/LLM-powered security assessments into development pipelines. LLM-based vulnerability discovery is already mature and you should start now by using an agent to security-review your code. Many capabiltiies are already available in OpenAI Codex or Claude Code.

*   Lastly – Empower your teams to use AI for defense!

PS: I want to point to the Cloud Security Alliance which authored this amazing whitepaper already on how to become Mythos Ready –> https://labs.cloudsecurityalliance.org/wp-content/uploads/2026/04/mythosreadyv92.pdf
