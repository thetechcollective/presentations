# IDP vision

## Context

A management consulting bureau of ≈1800 people is onboarding more and more actual software developers, AI and ML developers, data analysts, security engineers – and engineers in general, who has special needs for their development infrastructure and equipment.

For historical reasons the IT department and infrastructure of the bureau is naturally aimed at serving _management consultants_ and advisors in a pure Microsoft environment, utilizing only Windows PCs that are enrolled in the corporate Intra ID, which runs full virus scans on all disk activity. The bureau's tool stack is predominantly based on Microsoft tools: MS365, Sharepoint and Teams (etc). There are strict policies on what can be installed on Intra ID enrolled PCs. Users do not have admin rights on their PCs.

The IT department runs an Azure tenant for serving their purpose. On this tenant there are no development or lab projects allowed. Consequently, projects that do development, R&D and engineering will have to swipe their own credit cards, pick their own cloud provider and build their own shadow infrastructure for development purposes. The Bureau does not have a recommended strategy for development.

It's estimated that there are currently ≈100 employees in the company that has an engineering or developer profile, as opposed to the classic management consultant profile. These engineers have special needs. Currently the IT department are serving these employees with more powerful PCs (Intel I7, 12 core CPU, 64 GB RAM 1TB disk) and with the option to obtain admin rights on the PC on demand. But the policy is that this is _not_ a dedicated developer PC. Developers do _not_ have two PC's, but instead they have a beefier Corporate PC. Other than the power specs these PCs are still standard corporate PCs; they are still enrolled in the Intra ID, they are still running virus scans in the background. And still Windows is the only OS offering available. Developers install _Windows Subsystem for Linux_ (WSL), but as WSL is headless, it covers only the very basic needs for running Docker containers.

As the bureau is aiming to attract and retain talent in the engineering and developer realm. It has been identified that there is a need to come up with a strategy for how the bureau can build, optimize and maintain a standardized _internal development platform_ (IDP) based on the principles of _Developer Experience_ (DevX), _Platform Engineering_ (PE) and _Site Reliability Engineering_ (SRE).

Some typical development scenarios are:

- Developers are using devcontainers and docker and need access to Linux OS
- Developers build _Infrastructure as Code_ (IaC) and need access to a cloud infrastructure they fully control
- Developers need to install all kinds of tools and libraries - Often Open Source tools
- Developers need access to GitHub repositories, GitHub Copilot
- Developers predominantly wish to work on MacOs or Linux
- Developers work in serverless platforms (Supabase, Firebase, Azure functions, lambda functions, etc)
- Developers utilize many different programming languages, with Python and TypeScript as the most dominating ones.

Two teams have jointly built – what could be regarded as an IDP infrastructure _contender_.

Although this is built over time, outside the realm of the IT department, to serve specific client delivery needs, with no funding other than billable efforts to the specific clients, it is nevertheless built with PE, DevX, SRE principles in mind and works in all practicabilities as a — kind of — self-service IDP. Although currently with a relatively steep learning and accessability curve, but with the potential to be optimized, standardized and to evolve into a corporate standard.

Characteristics of the current IDP contender (current fully implemented – as well as _half-baked_ — features)

- A separate GitHub organization
  - For version control and deploys
  - For CI and automation
  - For maintaining an internal _community_ across projects
- Slack for internal informal communications
- Templates and reusable components for...
  - Unit test with coverage
  - Spell checks
  - Linting (static code analysis)
  - Automated tests
  - Deploys (in multi repo products)
  - Docker files
  - Devcontainers
  - Git configuration
  - AI configuration
  - Tool integrations
  - ...and much more
- Developed GitHub CLI (`gh`) extensions to support developers Software Development Life Cycles (SDLC)
  - Branching strategies
  - Kanban downstream board
  - Semantic versioning
  - Customer voice
  - Metrics (DORA)
  - Workflow optimizations
- A separate Azure tenant, with its own unrelated Intra ID
- Supabase instance

## Strategic Plan for an Internal Development Platform (IDP)

In the following, we'll present the outlines of a strategic plan for how the bureau — given the context – can build and develop an Internal Development Platform (IDP) serving based on DevX, Platform Engineering (PE), and Site Reliability Engineering (SRE) principles. The plan is based on the following assumptions:

- The corporate IT department doesn't participate in building and maintaining the platform, other than ongoing advise and sparring.
- The IDP will serve approximately 100 developers
- It recognizing the need to operate independently from the existing IT infrastructure. 
- The approach prioritizes developer experience (DevX), leveraging PE to build a reliable and scalable platform, and integrating SRE principles for operational excellence.

### 1. Vision & Guiding Principles

The IDP's vision is to create a frictionless, secure, and self-service environment where developers can innovate rapidly and effectively. This is achieved by:

- **Developer First (DevX):** Prioritizing the developer workflow and providing a seamless, "golden path" for software delivery.
- **Platform as a Product (PE):** Treating the IDP itself as a product with a clear roadmap, user feedback loops, and dedicated product management.
- **Reliability by Design (SRE):** Integrating practices like observability, SLOs (Service Level Objectives), and a blameless culture from the outset to ensure the platform is stable and predictable.
- **Security by Default:** Embedding security into the platform's foundation, rather than adding it as an afterthought.

### 2. IDP Core Components

The IDP will take offset in the current initiative and expand to include essential components.

- **Developer Workstations:** Move away from the standard Windows PCs with strict policies. Provide developers with the free choice of **Windows, MacOs or Linux machines** with local administrator rights. Implement a lightweight device management solution based on relevant package managers (e.g. Chocolatey, Brew, Apt, etc), potentially wrapped in, generic tools like Ansible. The use of **devcontainers** will standardize development environments regardless of the host OS, ensuring consistency and mitigating "works on my machine" issues.
- **Source Control and CI/CD:** Formalize and expand the use of the **current GitHub organization**. All code, including platform infrastructure code, will reside here. Develop and standardize GitHub Actions workflows as the primary **CI/CD pipeline**, enabling automated testing, security scanning, and deployments. Leverage the existing GitHub apps and extensions for DORA metrics and workflow monitoring.
- **Cloud Infrastructure:** Consolidate all developer projects onto a single, purpose-built **Azure tenant** with its own, separate identity management (Intra ID). This centralizes costs, streamlines governance, and provides a stable, secure foundation. Utilize **Infrastructure as Code (IaC)** tools like Terraform or Pulumi to manage all cloud resources, ensuring reproducibility and version control.
- **Services and Tooling:** Beyond the existing Supabase and Firebase, the platform team will provide and manage a suite of essential shared services, including:
  - **Container Registry:** A private registry (e.g., Azure Container Registry) for storing Docker images.
  - **Observability Stack:** A unified logging, metrics, and tracing system (e.g., Grafana, Prometheus, OpenTelemetry).
  - **Secrets Management:** A secure way to store and access secrets (e.g., Azure Key Vault).
  - **Knowledge Management:** Continue using **Markdown** for all documentation, leveraging GitHub Wikis, GitHub Issues, and a dedicated internal knowledge base.
  - **Communication:** Maintain **Slack** as the primary channel for real-time communication. And even potentially expand Slack with ChatOps features that can utilize slack as a self-service interface to the automated infrastructure. 

### 3. IDP Team Structure and Governance

The IDP will be owned and operated by a dedicated **Platform Engineering team**.

#### Team Composition:
- **Platform Engineers:** The core team responsible for building, maintaining, and scaling the platform. They have a strong SRE mindset.
- **Developer Advocate / Product Manager:** A dedicated role to act as the liaison between the platform team and the developer community. This person gathers feedback, prioritizes features, and ensures the platform meets user needs (DevX).
- **Governance:** The team will operate under a "paved road" model. They provide and maintain the "golden path" (the recommended way of doing things), but developers will have the flexibility to go off-road if necessary or desired, provided they can justify and manage the additional complexity and security concerns by leaving "the paved road". The platform team maintains a clear **service catalog** of what is provided and what the service level agreements (SLAs) are.

### 4. Budgetary Estimates (for 100 Developers)

The budget is a rough estimate and can vary widely based on specific tool choices and usage.

| Category | Cost Breakdown | Estimated Annual Cost |
| :--- | :--- | :--- |
| **Cloud Services (Azure)** | Compute, storage, databases, networking, CI/CD runners. Assume a significant portion for production and dev/test environments. | €100,000 - €300,000 |
| **SaaS Tools** | GitHub, AI, CI/CD Runners, Slack (paid tiers) licensing. | €$0,000 - €50,000 |
| **Developer Hardware** | Purchase of MacBooks or Linux laptops. This is a one-time capital expense for new hires or a refresh cycle. | €2,500 per device, With 30 people onboarded per year €75,000 |
| **Personnel (Platform Team)** | 2 dedicated FTE Platform Engineers and 1 Product Manager/Advocate (0.5 FTE). Assume average annual salary of €150K for engineers. | €375,000 |
| **Miscellaneous** | Training, conferences, and unforeseen operational costs. | €20,000 - €50,000 |

### 5. Implementation Roadmap

- **Phase 1 (Months 1-3):** **Bootstrap.** Secure executive sponsorship and funding. Formalize the Platform team. Establish a dedicated budget and separate cloud tenant. Onboard the initial two-team IDP infrastructure. Start defining the first "golden path" (e.g., a simple web app template).
- **Phase 2 (Months 4-9):** **Expansion.** Onboard pilot developer teams. Gather feedback and iterate on templates and services. Build out the observability stack and secrets management. Formalize the documentation and communication channels.
- **Phase 3 (Months 10-18):** **Scale.** Onboard up to 100 developers. Focus on automation and self-service capabilities. Begin defining and measuring SLOs for platform reliability. The platform team shifts from building to hyper care, continuous improvement and scaling.


### 6. Perspective

The conceptual idea of separate parallel development platform and infrastructure is likely to cause some raised eyebrows from a traditional corporate strict control paradigm.

A traditional CIO would likely take the position that:

>_!I strongly prefer developers have the tools they need within the organizational framework"_

But it's important to understand, that from the perspective of a software developer or engineer we're not _software users_ — we're _software builders_. We acknowledge 100% that our way of working is not (and probably never will be) a dish that any corporate IT department will serve willingly.

#### Race car analogy

It's like running a Formula 1 race car, those cars are not something that should be mixed with public traffic - we have dedicated tracks for that!

Spending many resources trying to wrench the arm around on a software development process to so it looks like that of writing Excel sheets or PowerPoint presentations is not accommodating the developers - it's not what they need. 

The bureau will not win any races that way!

#### Concrete suggestions to bridge the gap between corporate ability to server _software users_ and developers need to be acknowledges as _software builders::

**Focus on Risk Mitigation:** If we can understand corporate fears, worries and risks, acknowledging that IT department's primary job is to protect the company's data and network. What could go wrong if we liberated our DEV PC's and it something we can mitigate?.

**Is an IDP a good solution for the bureau:** In DevSecOps communities – including DORA – it's recommended as the standard approach for tech companies. Despite the counter intuitive measures to "let go of control"  it's generally accepted, that it's actually enhancing overall security in the corporation, not weakening it. The developer's tools and intellectual property are contained in a dedicated, professionally managed environment (GitHub, Azure, etc.) that are secured with best practices (MFA, access controls, etc.) without involving the corporate network at all. The corporate network is like the _public traffic_ which is only used for things like email and payroll. And they are entirely separated from the dangerous _race track_.

**Create a Clear Policy and Workflow:** Developers are not asking for freedom _inside_ the corporate realm; Corporate devices are used only for corporate tasks (email, HR, internal communication). Development work is done only on self-managed devices within the IDP.

**No corporate data is ever stored or processed on the self-managed devices:** The IDP is secured too, an subject to GDPR compliancy at all times. Professional developers understand fully, the concept of separating _what_. from _how_.

**A Pilot Program:** Some advanced, security aware developers could become appointed alpha users. Potentially even take a security training or certificate to be adapted in the pilot program, to so in the pilot developer would only need to receive the grace, that they can work on sw projects using non-Intra ID enrolled PCs. This is a low-cost, low-risk way for the IDP team and the IT department to get some experience and concrete data on its effectiveness and security. 

**Show Financial Benefits:** Money talks. There are some financial benefit assumptions that we could uncover and estimate. And then measure ongoing for realizations. Assumptions are that a professionally run IDP wil have positive impact on recruitment, retention, lead times to product deliveries, shorter feed-back loops with clients, overall lower license costs to shadow IT, Freed up resources in the IT department.
