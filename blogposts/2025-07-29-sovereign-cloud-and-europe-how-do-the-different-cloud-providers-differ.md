# Sovereign Cloud and Europe – How do the different Cloud providers differ? - msandbu.org
Given all the turmoil happening in the US, many companies in Europe have become more skeptical of the use of US based cloud providers (Google, AWS, Microsoft and Oracle). Many customers now have many concerns about using US based cloud technology, where I have had many meetings with customers about topics like

*   The risk of FISA orders (US **Foreign Intelligence Surveillance** that can give them access to your data in the cloud)
*   Cloud provider theoretical access (Insider or someone else that can get a hold of your data)
*   Geopolitical changes
*   The President of US implements specific changes.
*   Lastly what I see is that European organizations are demanding **local control** over their data.

![](https://i0.wp.com/msandbu.org/wp-content/uploads/2025/07/image-8.png?resize=705%2C470&ssl=1)

While the risk of things like the US president making changes that will have large impacts on how the EU can consume cloud platforms happening are rather slim, or that an insider in a cloud provider can get access to your data, it is still something that organizations need to understand. Some also want to lessen their reliance on US based technology, such as in Denmark some municipalities have decided to ditch Microsoft Office and will move to using Linux and Libre Office instead (https://www.euronews.com/next/2025/06/12/two-city-governments-in-denmark-are-moving-away-from-microsoft-amid-trump-and-us-big-tech-)

In recent years, cloud providers have made significant efforts to assure their customers of safety, introducing numerous new features to ensure data is accessed and processed securely within the EU.

*   Microsoft announced the EU data boundary (https://blogs.microsoft.com/on-the-issues/2025/02/26/microsoft-completes-landmark-eu-data-boundary-offering-enhanced-data-residency-and-transparency/) and recently introduced new sovereign solutions for Europe https://blogs.microsoft.com/blog/2025/06/16/announcing-comprehensive-sovereign-solutions-empowering-european-organizations/
*   AWS announced European Sovereign Cloud https://www.aboutamazon.eu/news/aws/built-operated-controlled-and-secured-in-europe-aws-unveils-new-sovereign-controls-and-governance-structure-for-the-aws-european-sovereign-cloud
*   Google introduced Sovereign Cloud https://cloud.google.com/blog/products/identity-security/google-advances-sovereignty-choice-and-security-in-the-cloud
*   Oracle announced new Sovereign and air-gapped cloud offerings https://www.oracle.com/nl/news/announcement/oracle-advances-national-security-with-new-sovereign-air-gapped-cloud-offering-2025-06-17/

Reading the announcements and documentation they’ve published can be quite challenging to understand. That’s why I decided to write a brief summary of what these four providers have done, making it easier to see the differences and what they offer.

*   Confidential Computing = Is a way to encrypt data during runtime within virtual machines. I have a blog post summarizing the different encryption methods in Microsoft Azure (https://msandbu.org/encrypting-of-data-within-microsoft-azure/))
*   External Key Management = Is a way to encrypt data using your own encryption keys
*   EU based operations = Means that they have an EU entity that delivers cloud services



* Feature: Confidential Computing
  * Oracle Cloud: AMD SEV
  * Microsoft Azure: AMD SEV and SGX enclaves
  * Amazon Web Services: Nitro enclaves
  * Google Cloud: AMD SEV and Intel TDX
* Feature: External Key Management
  * Oracle Cloud: External Key Management Service
  * Microsoft Azure: Currently developing*
  * Amazon Web Services:  AWS KMS External Key Store (XKS)
  * Google Cloud: Cloud External Key Manager
* Feature: EU based operations
  * Oracle Cloud: Oracle EU Sovereign Cloud
  * Microsoft Azure: National Partner Clouds (Bleu – France and Delos Cloud in Germany)
  * Amazon Web Services: AWS European Sovereign Cloud
  * Google Cloud: Google Cloud Dedicated
* Feature: EU based operator
  * Oracle Cloud: Separate EU entities, operations/support EU-residents only
  * Microsoft Azure: Trough Bleu and Delos not directly trough it own European entity
  * Amazon Web Services: New EU parent + subsidiaries in Germany, EU citizens only
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


There are some important distinctions between the four major cloud providers. **Oracle** and **AWS** are introducing sovereign cloud offerings that go beyond just data residency and are structured to meet strict EU digital sovereignty requirements. Both are establishing **fully independent EU-based legal entities** that operate, control, and support their EU sovereign cloud services, with all data, personnel, and operations based within the EU, and independent of their US-based parent companies. Oracle’s EU Sovereign Cloud is already operational, while AWS’s European Sovereign Cloud is launching its first region in Germany by the end of 2025.

**Microsoft** and **Google** both provide features such as the **EU Data Boundary**. This enables customers to process and store most core cloud data within the EU, but both companies’ clouds remain ultimately operated by US-based parent companies. The data boundary adds strong controls, but, legally and operationally, ultimate authority remains with the US parent, posing potential concerns over extraterritorial US law (e.g., the CLOUD Act)

To address European sovereignty and regulatory demands, **Microsoft** has partnered with Orange and Capgemini to launch **Bleu**, a French company that will offer Azure and Microsoft 365 cloud services fully operated by and within France, distinct from standard Azure[](https://www.lemagit.fr/actualites/366566434/Cloud-souverain-Bleu-demarre-officiellement-ses-prospections)
[](https://www.datacenterdynamics.com/en/news/orange-capgemini-to-finally-launch-bleu-sovereign-cloud-service/). Similarly, **Google** partners with local European firms such as Thales (France) and T-Systems (Germany) to offer sovereign versions of Google Cloud—Thales provides additional controls and assurances, though Google itself is still the technology provider at the core.

It is also important to note that while the other Cloud provider like (Google, Amazon and Oracle) provide their own self-hosted versions of their platforms in ready-to install racks as a converged solution consisting of hardware and software. Microsoft has evolved their Hyper-V and S2D (Storage Space Direct) service into Azure Local which is their alternative to self-hosted.
