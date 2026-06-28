# Microsoft 365 Local and Azure Local Disconnected Released - But does it solve anything? - msandbu.org
Yesterday Microsoft published a blogpost stating that Microsoft 365 Local and Azure Local Disconnected are now generally available –> https://blogs.microsoft.com/blog/2026/02/24/microsoft-sovereign-cloud-adds-governance-productivity-and-support-for-large-ai-models-securely-running-even-when-completely-disconnected/

Both of these new features allow you to run both in an Airgapped or completely offline scenario, which ensures that you have no requirement to connect these services to the cloud. However still the need to get updates/patches but this has always been the case. But let us dig into what Microsoft 365 Local and Azure Local actually is.

Microsoft 365 is a combination of Skype for Business Server SE – SharePoint Server SE and Exchange Server SE delivered as a reference architecture, preferably as a predefined template that you use to deploy on Azure Local. However there is little to no documentation on the feature and capabilities when it comes to lifecycle management of the product.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/02/image.png?resize=975%2C557&ssl=1)

Secondly when you look at the roadmap there is also little to no indication on what kind of capabilities or features that are planned for the product. Also in order to get access to the service you need to signup using this form –> https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR\_hLIVFWovtOlco788BqmedUQURKTklSS1dSNERYU0NXMFMxSThaNjJSTCQlQCN0PWcu&route=shorturl

Secondly we have Azure Local Disconnected, which is pretty much Azure Local but with a local control plane (which is managed by the management appliance) that provides a Azure portal and ARM experience similar to the Azure Portal.

For those that have worked with Azure Stack (Before it was called Azure Stack Hub…) it is much of the same requirements but provides a lot less capabilities. If you want to set up disconnected you need to have Active Directory and ADFS to handle authentication. The platform itself provides VMs, Kubernetes, Container Registry, Key Vault and Azure Policy and a similiar Azure Web Portal with ARM.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2026/02/image-1.png?resize=1024%2C657&ssl=1)

To get access Azure Local Disconnected you also need to apply via the form here –> https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR32dmnCNvLNAhNlErhkTKo5UQk1WWk9WVUxNNkw0TkdDVVpMVTdGTlhPWiQlQCN0PWcu

When I first saw the release article for Microsoft 365 Local I thought, huh this is just SharePoint, Exchange and Skype For Business wrapped in a reference architecture and I think I was right! Then my second though was, who is this for? I know the nightmare it was to manage Exchange and Skype/Lync/OCS before, so who would want to get back to it? Well those that require….

*   Complete offline/air gapped scenarioes (Defence / Healthcare / Oil & Gass) where you have limited Connectivity
*   Data Sovereignty (Because of the geopolicital situation)

But arent there other options available?

Yes!

You can still run these services standalone without the need of deploying it “as-a-service” model from Microsoft, since Skype, Exchange, SharePoint is still available as a subscription edition and the same goes for Hyper-V which can also be deployed without the need for Azure Local.

While Microsoft does offer other capabilities on Azure Local such as Azure Virtual Desktop and other Arc services, these are not available to Azure Local Disconnected. Same goes with the capabilities of support for SAN, support for non AD deployments and such.

What other capabilities does it provide compared to a Hyper- standalone version? Except the self-service capabilities as part of Azure Local and some additional features not much. In addition the Azure Local appliance running on the management cluster needs at least 64 GB of memory. You can also deploy other solutions like Proxmox in combination with OSS modules that can provide self-service capabilities if that is what is needed https://github.com/The-Network-Crew/Proxmox-VE-for-WHMCS or you can also go with VMware or Nutanix depending on how much $$$$ you have.

However I have seen more and more moving towards using Nutanix since all the broadcom license changes.

When it comes to providing SharePoint / Skype / Exchange I guess there is not a lot of options for on-premises deployments. There are however a few factors I want you to consider when looking into the options if you are evaluating these options.

*   What is the roadmap of the product? Are there plans to further development on it?
*   Get the details of Microsoft 365 local, what is the difference between that and setting it up using SE edition on your own hypervisor?
*   What kind of capabilities do we get and what do we miss?
*   When will features go out of preview and into GA? (Such as AKS on Azure Local Disconnected)

So do these new offerings solve anything? Time will show!
