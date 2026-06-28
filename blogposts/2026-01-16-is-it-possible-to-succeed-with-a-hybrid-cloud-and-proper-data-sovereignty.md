# Is it possible to succeed with a Hybrid Cloud and proper data sovereignty? - msandbu.org
To be honest I did not think that I would start 2026 with so many discussions on Cloud Exit / Hybrid Strategy and sovereignty, but it seems with all that is doing on in the world that more and more organisations are starting to consider their options/alternatives when it comes to IT-services.

And it is funny to think about all this talk about sovereignty while the old Latin term it derives from means “Chief or ruler”, Webster has a better definition of it **“freedom from external control”**

Many organisations I have worked with have either taken a “full cloud” approach where they build new services and applications (even migrating) some applications to a public cloud from one of the three hyperscalers (Google, AWS and Microsoft) or others that have been reluctant to use public cloud and are still running their on-premises virtualisation stack, and fine with that.

So what is going on that are making so many evaluate their options now?

*   **License price changes** (Changes from VMware, Citrix and even Microsoft to name a few)
*   **The complexity of product** – Many products have become essentially “bloated” where they have so many features, but many might only need 1 of the 50 available features.
*   **The Geo political aspect** (With that is going on with the war and tensions between different countries(\*cough\* Greenland). Many are now evaluating alternatives to public cloud to ensure availability of service, regardless if the Internet or changes that would make it not available.
*   **Movement from others** – Where we have now seen municipalities in Denmark have stated that they are moving away from Microsoft to adopt more Open-Source technology, same in Germany. Many are also looking to “tag” along.
*   **AI Innovatio**n – With many of the technology companies building AI into all their interfaces,systems and platforms people are getting more concerned about privacy with the use of these systems. While they see the benefit of AI, many are sceptical on the direction it is going and want to make sure that they are in control on the data that is being used.
*   **EU Focus** – Many are also evaluating what kind of alternatives are EU based, to lessen their dependencies on US based technology and services.

It is difficult to discuss all these details without some sub-sections, therefore I have some different sections to discuss some of the main points like above. Namely

*   Virtualisation (Hypervisor) alternatives
*   Maturity of Hybrid Cloud and Tooling options
*   Sovereign Cloud Options
*   Local AI Infrastructure alternatives

Virtualization alternatives
---------------------------

Many organizations are now evaluating their VMware alternatives, given the recent changes to the SKU, licenses and which direction the company is moving. So what options do we have?

Before one can consider the alternatives, it is important to understand that changing hypervisors can also impact other products/features that we are using. Many products today rely on specific hypervisor APIs, features and integrations, which may not be available on other platforms. To name a few features

*   **Backup services** like Veeam, which either use APIs or rely on installed agents to manage snapshots and data copies.
*   **VDI services** such as Omnissa Horizon and Citrix Virtual apps and desktop.
*   **Storage solutions** like CSI drivers for Kubernetes and other 3.party storage solutions. Or providing fileshare capabilities directly from VSAN (Which is a VMware native service)
*   **Networking appliances** such as F5, NetScaler, Cisco, and Palo Alto. Many have VMware specific appliances.
*   **Security tools** like Trend Micro, which connect directly to security APIs.
*   **Monitoring tools** that integrate with your current platform and using VMware specific APIs.

Might be other things that are not listed here, but the most important part is do to this assessment. Depending on what you have, this can also impact what kind of alternatives you can use. If we for instance are reliant on using a specific service that is only supported on VMware and Hypervisor X, well it limits our options.

So what options do we have?

*   Proxmox
*   XCP-ng
*   XenServer
*   Hyper-V
*   Azure Local
*   Nutanix
*   KVM
*   Kubevirt

1.  Proxmox and Nutanix AHV are KVM based hypervisors while XCP-ng and Xenserver are based upon Xen.
2.  Azure Local is the same as Windows Server with Hyper-V but is a pure HCI based offering compared to Hyper-V. While Azure Local has also announced that they will support SAN and also a disconnected options model (which is currently in preview)
3.  Kubevirt is an extension to Kubernetes and allows you to manage virtual machines as Kubernetes resources.Kubevirt only makes sense if your organization has gone the route with cloud-native and only have a few set of virtual machines that for legacy reasons cannot be converted to run as a container.
4.  Nutanix AHV is Nutanix’s own hypervisor, but Nutanix as a distributed storage service that can run across both AHV, VMware and Microsoft. However Nutanix have also stated that their support for Hyper-V is going EOL, and is focusing more on AHV support.

But consider the following – You are tasked with evaluating your options in regards to virtualization, the needs you have for running virtual machines in 2026 are probably a lot less then it was for 10 – 15 years ago when you made the jump into VMware. Do I need all the functionality? Or do I just need a platform that can support my ever smaller set of virtual machines + some need to do backup of those services? Well maybe Proxmox can be “good” enough alternative. If you need some more advanced features? well then you might need to do in another direction.



* Feature: Type
  * Proxmox: Open-source
  * Azure Local / Hyper-V: Proprietary
  * Kubevirt: Open-source
  * Nutanix AHV: Proprietary
  * XenServer: Open-source
* Feature: Virtualization
  * Proxmox: KVM & LXC
  * Azure Local / Hyper-V: Hyper-V
  * Kubevirt: KVM-based, runs on Kubernetes
  * Nutanix AHV: KVM-based
  * XenServer: Xen-based
* Feature: Air Gap Support
  * Proxmox: Yes
  * Azure Local / Hyper-V: No (Unless you run Hyper-V natively or Azure Local disconnected but that is currently in preview
  * Kubevirt: Yes
  * Nutanix AHV: Yes
  * XenServer: Yes
* Feature: SDN Capabilities
  * Proxmox: Yes
  * Azure Local / Hyper-V: Yes
  * Kubevirt: Yes (leverages Kubernetes networking)
  * Nutanix AHV: Yes
  * XenServer: No
* Feature: SDS Capabilities
  * Proxmox: Yes (via Ceph)
  * Azure Local / Hyper-V: Yes
  * Kubevirt: Yes (via Kubernetes storage classes)
  * Nutanix AHV: Yes
  * XenServer: No
* Feature: Live Migration
  * Proxmox: Yes
  * Azure Local / Hyper-V: Yes
  * Kubevirt: Yes
  * Nutanix AHV: Yes
  * XenServer: Yes
* Feature: High Availability
  * Proxmox: Yes
  * Azure Local / Hyper-V: Yes
  * Kubevirt: Yes
  * Nutanix AHV: Yes
  * XenServer: Yes
* Feature: Storage Types
  * Proxmox: Local, SAN, NAS. SDS
  * Azure Local / Hyper-V: Local, SAN, NAS, SDS
  * Kubevirt: Local, SAN, NAS, VSAN (SDS)
  * Nutanix AHV: Hyperconverged
  * XenServer: Local, SAN, NAS
* Feature: Backup Solutions
  * Proxmox: Built-in & 3rd party
  * Azure Local / Hyper-V: 3rd party
  * Kubevirt: 3rd party
  * Nutanix AHV: 3rd party
  * XenServer: 3rd party
* Feature: Clustering
  * Proxmox: Yes
  * Azure Local / Hyper-V: Yes
  * Kubevirt: Yes
  * Nutanix AHV: Yes
  * XenServer: Yes
* Feature: Container Support
  * Proxmox: Yes (LXC)
  * Azure Local / Hyper-V: Yes (AKS)
  * Kubevirt: Native
  * Nutanix AHV: Yes (NKE)
  * XenServer: No
* Feature: GUI Management
  * Proxmox: Yes
  * Azure Local / Hyper-V: Yes
  * Kubevirt: Yes
  * Nutanix AHV: Yes
  * XenServer: Yes
* Feature: vGPU Support
  * Proxmox: No
  * Azure Local / Hyper-V: Yes (GPU-P) NVIDIA
  * Kubevirt: Yes
  * Nutanix AHV: Yes
  * XenServer: Yes
* Feature: API Support
  * Proxmox: Yes
  * Azure Local / Hyper-V: Yes
  * Kubevirt: Yes
  * Nutanix AHV: Yes
  * XenServer: Yes


While this table above just serves the purpose of showing “some” capabilities, and does NOT give a well enough showcase of the difference but for instance support for vGPU if you are relying on the use of GPU for your workloads well Proxmox might not still be the best alternative.

Maturity of Hybrid Cloud and Tooling options
--------------------------------------------

Another topic that I have worked with that feels like an eternity is “Hybrid Cloud”, but what does an Hybrid Cloud actually consist of? It is like the best of both worlds? or the worst of both? and do I actually need it? or is my requirement so dead simple that I just need to have some services running locally because of “proximity” to the user and application? Well that has been the majority of most cases.

While the definition of the term is quite simple – **Combining public and private cloud**. There are levels of maturity that many organisations miss out on. Many set up an identity sync and a VPN tunnel and they are “hybrid” however that is something I consider the lowest level of maturity of hybrid cloud (Network and Identity). What about automation & orchestration and a common set of tooling to use on both? **That is the second level**. Then have applications and services that can run on a cloud-native workloads and can easily be deployed across any platform with a standardised zero-trust based service network across platform and combined with identity, automation and orchestration, that is the most mature level of hybrid cloud adoption. Also + points if they have a datamesh where data is easily replicated across the different cloud, but again a hybrid cloud should ONLY be built based upon which requirements you have.

But, if you want to build a mature hybrid cloud with all bells and whistles its difficult, since there is no “platform” that can magically solve all of this (like some kind of swiss army knife.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-22.png?resize=384%2C266&ssl=1)

Back in the “earlier” days we had products called CMP (Cloud Management Platform) that would abstract away the underlying platforms regardless if it was VMware, Hyper-V, AWS or Azure and could manage network and service automation across. While most of them died out because the market was not there, and they had a lot of issues trying to keep up with all the updates, one has managed to survive which is Morpheus that HPE has acquired. These CMP tools were useful to handle self-service with a standardised approach, and even Morpheus in a later stage added support for tools like Terraform to handle automation.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-24.png?resize=1024%2C719&ssl=1)

However Morpheus does not solve – **Networking – Identity – Data layer – Operations Tooling – Backup**. Hence one needs to evaluate those as well for which tools one should use across different platforms. Another approach for hybrid is using cloud based management (aka control plane from the vendors) planes such as Google Distributed Cloud, Microsoft Azure Stack Hub or AWS Outposts, where you get services from the cloud providers running locally.

The main advantage with this type of approach is that it solves some of the pains with a unified management plane, consistent APIs and some of the same services such as Storage and networking. However I still need tools to handle backup, monitoring and such across the different platforms.



* Feature: Deployment Model
  * Azure Stack Hub: On-premises (rack or servers)
  * AWS Outposts: On-premises (rack or servers)
  * Google Distributed Cloud: On-premises (rack or servers)
* Feature: Hardware Requirements
  * Azure Stack Hub: Specific OEM hardware (Dell, Lenovo, HPE)
  * AWS Outposts: AWS-designed hardware
  * Google Distributed Cloud: Google-designed hardware
* Feature: Air-gapped
  * Azure Stack Hub: Both connected or offline supported
  * AWS Outposts: Only connected
  * Google Distributed Cloud: Both connected or offline supported
* Feature: Core Services
  * Azure Stack Hub: Compute, Storage, Networking
  * AWS Outposts: Compute, Storage, Networking
  * Google Distributed Cloud: Compute, Storage, Networking
* Feature: Scaling
  * Azure Stack Hub: Scale-out by adding nodes (4-16 servers per scale unit)
  * AWS Outposts: Scale by adding racks or servers
  * Google Distributed Cloud: 6-12 server machines
* Feature: Features
  * Azure Stack Hub: Virtual Machines, Blob Storage, App Service, AKS, Azure container Registry
  * AWS Outposts: Elastic Compute Cloud (EC2)Elastic Container Service (ECS)Elastic Kubernetes Service (EKS)Elastic Block Store (EBS)EBS SnapshotsSimple Storage Service (S3)Relational Database Service (RDS)ElasticacheEMRApplication Load Balancer (ALB)Route 53 ResolverIoT GreengrassElastic Disaster RecoveryVMware Cloud
  * Google Distributed Cloud: GKE, Virtual Machines, Block and object storage, Vertex AI. Database engine (PostgreSQL, Oracle and AlloyDB)


So if you want to have the ultimate hybrid cloud you need to have a solution for each of the following points! Consider the following examples I use here, which can be one way to provide a good overall hybrid cloud experience.

*   Monitoring – Datadog/Dynatrace
*   Data Protection – Veeam
*   Management – Azure Arc or RMM
*   Automation – Terraform (supports most providers)
*   Self-service – Service Now / Aria
*   Networking – Cilium (depending on workloads)
*   Access Management – Entra ID (most use SAML/OIDC tooling)
*   Security – Sentinel – Defender for Cloud
*   Data (Files – Object – Block) – Depending on requirement or demand.

The problem with these services listed above, is that some of them are cloud only which undermines the need for self-control (in case of emergency). Because it could be a big issue if something where to happen (Internet is gone, cloud services unavailable) then suddenly I do not have monitoring, security tooling or even IAM….

But back to the main point! many do not need a fully mature hybrid cloud. Some just have services running on some local DC because of proximity to applications, however there are benefits to having one product to solve different platform instead of having people to manage multiple tools/products to manage different platforms.

Sovereign Cloud alternatives
----------------------------

This week AWS launched their EU Sovereign cloud in the State of Brandenburg, Germany. So this is a clear indication that the public cloud providers also want to meet the requirements/demands that the customers want to ensure that they can use public cloud services but with an EU umbrella. While AWS is one example, but all the cloud providers are scrambling to trying to meet this demand.

Such as Microsoft, Google and Oracle all have different EU offerings. Because there is no denying that these cloud providers have the widest range of services and capabilities, so for customers that want to use a public cloud provider but want to have it placed and using the EU umbrella, the logical choice is to use one of the big four.

ISG released a public cloud sovereign report in December to showcase some of the different providers, while this report is NOT good, it shows some of the alternatives. You can read the report here –> 25-EMEA-en-US-isg-other-ardm-provider-lens-sovereign-cloud-infrastructure-services-eu-reprint.pdf (One requirement to be part of this is to have external key management capabilities which Microsoft is currently developing, but for some reason they are still on this map)

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-27.png?resize=822%2C456&ssl=1)

But how “free” would you be when using some of these cloud providers? Such as the big four… Right now there are currently two (hyperscaler) cloud providers that have a dedicated EU Cloud offering that is its own EU based operations = Means that they have an EU entity that delivers cloud services. This means that they avoid situations like this –> Microsoft: U.S. Access to EU Data Confirmed

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-28.png?resize=976%2C782&ssl=1)

The only cloud providers that have this now is **AWS and Oracle Cloud**, this table below showcases some of the features and capabilities that have been added to support an EU based cloud.



* Feature: Confidential Computing
  * Oracle Cloud: AMD SEV
  * Microsoft Azure: AMD SEV and SGX enclaves
  * Amazon Web Services: Nitro enclaves
  * Google Cloud: AMD SEV and Intel TDX
* Feature: External Key Management
  * Oracle Cloud: External Key Management Service
  * Microsoft Azure: Currently developing….
  * Amazon Web Services:  AWS KMS External Key Store (XKS)
  * Google Cloud: Cloud External Key Manager
* Feature: EU based operations
  * Oracle Cloud: Oracle EU Sovereign Cloud (Frankfurt and Madrid)
  * Microsoft Azure: National Partner Clouds (Bleu – France and Delos Cloud in Germany)
  * Amazon Web Services: AWS European Sovereign Cloud (Brandenburg – Germany)
  * Google Cloud: Google Cloud Dedicated
* Feature: EU based operator
  * Oracle Cloud: Separate EU entities, operations/support EU-residents only
  * Microsoft Azure: Trough Bleu and Delos not directly trough it own European entity
  * Amazon Web Services: EU parent + subsidiaries in Germany, EU citizens only
  * Google Cloud: Data & workloads Hosting in France. Support provided by European staff (S3NS)
* Feature: EU Data Boundary
  * Oracle Cloud: 
  * Microsoft Azure: Yes
  * Amazon Web Services: 
  * Google Cloud: Yes
* Feature: EU based entity
  * Oracle Cloud: Yes
  * Microsoft Azure: No trough partner
  * Amazon Web Services: Yes
  * Google Cloud: No trough partner
* Feature: Self-hosted Cloud services
  * Oracle Cloud: Oracle Compute Cloud@Customer
  * Microsoft Azure: Azure Local (Hyper-V and S2D)
  * Amazon Web Services: AWS Outposts
  * Google Cloud: Google Distributed Cloud
* Feature: Self-hosted air-gapped
  * Oracle Cloud: Oracle Compute Cloud@Customer Isolated
  * Microsoft Azure: Azure Local Disconnected (Preview)
  * Amazon Web Services: No
  * Google Cloud: Google Distributed Cloud air-gapped


It should be noted that EU Data Boundary “feature” (Still a US entity) is the alternative to an EU based operator where you have a separate EU entity. So for Oracle and AWS, both have establishing **fully independent EU-based legal entities** that operate, control, and support their EU sovereign cloud services, with all data, personnel, and operations based within the EU, and independent of their US-based parent companies. Oracle’s EU Sovereign Cloud is already operational, while AWS’s European Sovereign Cloud launched this week.

**Microsoft** and **Google** both provide features such as the **EU Data Boundary**. This enables customers to process and store most core cloud data within the EU, but both companies’ clouds remain ultimately operated by US-based parent companies. The data boundary adds strong controls, but, legally and operationally, ultimate authority remains with the US parent, posing potential concerns over extraterritorial US law (e.g., the CLOUD Act)

To address European sovereignty and regulatory demands, **Microsoft** has partnered with Orange and Capgemini to launch **Bleu**, a French company that will offer Azure and Microsoft 365 cloud services fully operated by and within France, distinct from standard Azure[](https://www.lemagit.fr/actualites/366566434/Cloud-souverain-Bleu-demarre-officiellement-ses-prospections)
[](https://www.datacenterdynamics.com/en/news/orange-capgemini-to-finally-launch-bleu-sovereign-cloud-service/). Similarly, **Google** partners with local European firms such as Thales (France) and T-Systems (Germany) to offer sovereign versions of Google Cloud—Thales provides additional controls and assurances, though Google itself is still the technology provider at the core.

So what does this mean? For customers using Sovereign Cloud from AWS or Oracle, if something was to happen with the collaboration between EU and USA or you have requirements that all data, operations and supports needs to be provided from EU, these two are the only options from the largest cloud providers. Of course many go this route, because this is where you can find people with knowledge and expertise. While there of course other cloud providers as listed in the ISG report such as **OVHCloud, Hetzner** and others.

Why dont we use them? Just to give an example, setting up a virtual server in **Hetzner is ACTUALLY 10x cheaper compared to Google, AWS, Azure with a similar specification**. So why go for the more expensive approach? Well often it is a combination of things such as **Ecosystem – Features – Competency** – **Requirements**, which often have a higher priority compared to price.

Local AI Options
----------------

Public cloud LLMs are powerful, but they don’t always meet security and compliance needs. Fortunately more and more models are becoming open-weights and therefore it also means that they can be ran on our own infrastructure. While they are not as powerful as the main ones from Google, OpenAI and Anthropic they are becoming better and better with each release.

Artificial Analysis has a series of different benchmarks that these different LLMs are tested against, and we already now see open-weight LLMs among the top 10.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-29.png?resize=857%2C394&ssl=1)

To run LLMs efficiently within our own infrastructure, we need GPUs and a lot of it.  
LLMs are resource-intensive, particularly in terms of computational power, and they demand significant GPU memory to store both model parameters and intermediate data during inference (aka processing prompts)

GPUs (Especially NVIDIA) are optimised for high-performance and its high speed and bandwidth is essential for running LLMs effectively, allowing them to handle complex computations without being hindered by bottlenecks from memory-to-processor data transfers. When sizing a LLM deployment a general rule of thumb is that the size of the model (in billion parameters) x2 +20% overhead is the amount of GPU memory required to have the model loaded into memory.

As an example, if we have a model like LLaMa 3.2 11 Billion parameters, it would require at least (11 (Billion parameters) x 2 = 22 + 20% overhead) = 26.4 GB GPU Memory. Therefore it is recommended to use at least a GPU card like the NVIDIA A100 which has 40 GB of GPU Memory. This allows it to have enough resources to both store the model but also handle some inference processing.

> Required\_GB of vGPU Memory ≈ (Model\_params\_in\_Billions × 2) × 1.20  
> The 2× factor keeps activations resident; +20 % covers framework overhead and small batches.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-30.png?resize=1024%2C744&ssl=1)

However this formula does not take into effect how many tokens/sec this hardware will generate, luckily NVIDIA has some good benchmark content that shows the performance of a model on their GPUs also with tokens context size (Performance — NVIDIA NIM LLMs Benchmarking)

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-31.png?resize=800%2C679&ssl=1)

However, if the use-case was to build a service that would be used for a large number of users, the hardware requirement would be even higher.

Also AMDs cards are also known for having higher memory capacity compared to NVIDIAs, allowing us to have larger models on a single GPU.


|GPU         |GPU Memory|GPU Memory bandwidth|
|------------|----------|--------------------|
|NVIDIA H100 |80  GB    |3.35 TB/s           |
|NVIDIA H200 |144 GB    |4.80 TB/s           |
|AMD MI300X  |192 GB    |5.30 TB/s           |
|AMD MI325X  |256 GB    |6 TB/s              |
|MI400 (2026)|432 GB    |19.6TB              |


In addition there are also other scenarios, for instance if we plan to train the model using fine-tuning. Fine-tuning is a process that requires even more GPU memory and should even be deployed on a dedicated hardware so it does not impact the LLM service for regular users.

When it comes to providing a centralised service that supports multiple concurrent users, such as an internal chatbot, developer assistants or a company-wide RAG (Retrieval-Augmented Generation) service, or be a framework for underlying virtual agents, the architecture must be designed for handling it at scale.

Therefore some key considerations are important

1.  **Load Balancing and Model Parallelism  
    **In multi-user scenarios, a single instance of a model may not be sufficient to serve all incoming requests. To handle this, load balancing and model sharding can be employed. Model parallelism splits the model across multiple GPUs, while data parallelism replicates the model across GPUs and handles different requests. Frameworks like **vLLM** are useful tools to manage inference at scale.
2.  **Serving Frameworks  
    **Tools like **vLLM** (optimized for serving LLMs with high throughput and low latency) or **Triton Inference Server** by NVIDIA can serve multiple models simultaneously, manage batching efficiently, and even support dynamic model loading. These tools integrate with Kubernetes for orchestration and can expose APIs to frontend applications. 
3.  **Model Quantization and Optimization  
    **Running LLMs at scale can be optimized further through quantization techniques, such as INT4 or INT8 precision. This can reduce memory usage significantly, with minimal accuracy loss.
4.  **Multi-Tenant Architecture  
    **If the LLM service is shared across departments or teams, it’s important to isolate workloads and manage quotas. Techniques such as request throttling, per-user model sessions, or fine-tuned models for different user groups can be introduced. Using an API gateway with authentication and logging helps secure and monitor usage, with tools like OpenLLM.
5.  **Storage and Vector Databases for RAG  
    **RAG applications require document stores or vector databases to retrieve relevant content. Tools like **Chroma**, **Weaviate**, **AstraDB**, or **Qdrant** integrate well with private LLM infrastructure.

So one can go in the direction of using turnkey ready platforms from vendors like

**•HPE Private Cloud AI  
•OpenShift Enterprise AI  
•VMware Private Cloud AI  
•Nutanix Enterprise AI  
•Open-source with vLLM  
•NVIDIA AI Enterprise (RUN:AI)**

While some are more integrated then others such as VMware that combines all with virtualisation, while Openshift is more from a Cloud native perspective. Most of them use vLLM underneath and if you also want to provide additional isolation between workloads running on GenAI to support multi-tenancy you can also use for instance NVIDIA MIG Isolation. NVIDIA MIG also allows you to run dedicated workloads in a isolated partition on the GPU (as seen below) the problem is that with most cases you limit the amount of GPU memory so that it can no longer run the LLM.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/01/image-32.png?resize=791%2C446&ssl=1)

Most of the services listed above provide a set of management capabilities that can run inferencing, fine-tuning but also MLOps services. Most of these also use vLLM (in combination with other inferencing runtimes).

However it should be noted that building an agent ecosystem on top of private infrastructure requires inferencing API that supports or uses the OpenAI compatible API.

Summary
-------

Can we have **freedom from external control**, have access to the **“cheapest” alternative for virtualization** , **leverage AI** as we want but also have **hybrid cloud with built-in** option for workloads where it is required or beneficial?

What matters the most? What is your business drivers? Everything is possible, but the main thing I want to highlight in this article is that there are options available, many alternatives to each of the topics but it requires some research into the alternatives and your own needs to determine what is the right choice.
