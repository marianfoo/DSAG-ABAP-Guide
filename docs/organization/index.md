---
layout: page
title: Organization
permalink: /organization/
nav_order: 1
---

{: .no_toc}
# Organization

1. TOC
{:toc}

Why should management invest in software quality and a well-structured development organization? While stakeholders generally take software quality for granted, they often provide little support for the measures needed to ensure it, because “there is no glory in prevention.”

From a management perspective, such an investment (in time, resources, and tools) should be supported by a business case, which is easiest to develop for your company by taking a close look at the current challenges facing your business and your IT department. If you recognize some of the following issues in your organization, optimizing your development department and organizational culture with a focus on quality and technology could be a potential solution:

* (Too) slow implementation of innovations and regulatory requirements compared to your competitors
* End customers who are dissatisfied due to IT issues, errors, processes, or unmet SLAs, etc.
* Erroneous processes and data in your systems, requiring significant effort to correct
* Constant overload on the IT department, a tendency toward burnout, high staff turnover, knowledge silos, and loss of knowledge
* Difficulties in collaboration between business units and IT
* Implementations do not meet the business requirements of the departments
* Long project timelines and feedback processes, high need for rework
* Complex system configurations and codebases that have evolved over time

Solutions to these problems generally fall into two categories, for which this DSAG guide and other guides outline possible options:

* Cultural and organizational: cross-functional teams, breaking down silos, clear role assignments and responsibilities, trust, communication structures, a shared goal and vision, fostering cooperation rather than competition, etc.
* Software quality: automation, professional testing, development guidelines, software architecture management, enterprise architecture management (EAM), targeted training, pair programming, code reviews, communities of practice, etc.
  

Some of these solutions can provide quick wins; others can be evaluated through small pilot initiatives and then established sustainably. It is worth examining software-engineering practices that have been used outside the SAP world for many years and adapting them to your organization. The following section provides an overview.


## The Building Blocks of an Effective Development Organization

From a business perspective, the transformation into a successful S/4HANA technology team is a complex and often underestimated challenge. Depending on the maturity level and direction of your IT organization, adjustments to cultural and organizational factors are necessary to achieve the strategic vision.

The greater the proportion of customer-specific adaptation and expansion of your existing SAP software is or should be strategic (see [Chapter Clean Core]({{ site.baseurl }}/clean-core/problems-and-challenges/)), the more important is the entrepreneurial focus on the efficiency and effectiveness of your development organization. The following excerpt touches on what we believe to be the most important subject areas that will support you on your way to becoming a successful development organization.


### Definition of the appropriate structural and process organization

The orientation of your development organization depends on the amount, complexity and frequency of customer adjustments in your SAP systems (_Make-or-Buy_ _or “Do nothing”_ _Decision_). If you are one of the customers who can use SAP software as part of standard software without major adjustments, investing in your own SAP development department is generally not worth it from an economic perspective. In this case, it is recommended to rely on external specialists with the appropriate core competence and reputation and to handle the small amount of customer adjustments in the SAP system under the umbrella of defined documentation guidelines (change documentation, operating manuals, etc.) and clearly defined service levels / KPIs.  The exact nature of the decision depends on the individual case in your company and can vary from minor changes to complete platform operation by your own team or an external service partner.

If you frequently need to customize your SAP systems through customer-specific development—due to a lack of functionality in your core business processes or the need to integrate unique selling points that give you a competitive edge—it is worth considering investing in your own SAP development organization. Building a successful development organization is a complex undertaking and must take into account not only technological issues but also socio-economic aspects. Use the following points to tailor your company’s approach to your specific needs.


### Team Organization and Team Composition

Software development teams are the key to successfully executing and implementing your development projects. This is where the magic happens when it comes to translating business requirements into technology and ensuring that the solution remains cost-effective and maintainable for decades to come. For the team to meet this challenge, it must be equipped with the necessary skills, resources, and processes and receive the appropriate support. For example, if you notice that your teams are spending a lot of time and energy defending themselves against accusations from other teams, or that there are long wait times between the individual steps in your software development process, this could be a sign of a suboptimal team structure that urgently needs to be optimized. The following recommendations can help prevent problems with team organization.

* The right team composition is essential for effectively accomplishing the tasks assigned to the team. Team size, cultural background, professional and technical expertise, and the availability of resources all play a significant role in this regard. Ensure that the team can perform all activities necessary to complete the tasks and deliver results independently whenever possible, and that dependencies on upstream or downstream processes are kept to a minimum.
* When putting together a team, take into account the business and technical complexity. Especially in the SAP environment, managing complexity across different application areas often poses a challenge. In addition to the business context, the team must also grapple with application-specific frameworks, existing customer code, technology trends, and different technology stacks. Ensure that the team does not work on too many different tasks and can instead focus on a manageable area, such as a specific business module. Take your team seriously if they complain about having to manage excessive complexity. Otherwise, you risk long-term health issues and reduced productivity due to frequent context switching and cognitive overload.
* Also ensure that developers can focus on their core competency—designing and creating high-quality software—and do not have to worry about additional tasks such as requirements management or process documentation. An exception to this is the temporary performance of these activities in order to gain a more precise understanding of the technical problem domain and better grasp the underlying concepts. As a rule, a deeper understanding of the problem domain leads to more efficient software design and thus provides added value for the developer.
* Provide your software development teams with the appropriate freedom for experimentation, training and product optimization. Avoid burning out your developers permanently with 100% utilization. Enable developers to learn from each other through measures such as creating a community of practice. For example, experiment with [Pair-Programming](https://en.wikipedia.org/wiki/Pair_programming) and benefit from the associated [Vorteilen](https://medium.com/the-liberators/in-depth-the-costs-and-benefits-of-pair-programming-b4b54b27c6ff), such as potentially higher code quality and better software design.
* Give teams the means and tools to gain transparency about their work area. Effective optimization can only be carried out on the basis of numbers, data and facts see [Chapter ALM]({{ site.baseurl }}/application-lifecycle-management/ensuring-quality/). If the information about custom code and process metrics is not available, it is almost impossible to make a business-wise decision about a worthwhile investment in an optimization project.
  
{: .note }
>
> Artikel & Blogposts
> - [Inverse Conway Maneuver – ThoughtWorks](https://www.thoughtworks.com/en-de/insights/blog/customer-experience/inverse-conway-maneuver-product-development-teams)
>
> Webseiten & Ressourcen
> - [Team Topologies](https://teamtopologies.com/)
> - [Flow Engineering](https://flowengineering.org/)
> - [Core Domain Charts – GitHub](https://github.com/ddd-crew/core-domain-charts)
> - [Managing the Unmanageable](https://managingtheunmanageable.net/)
>
> Books
> - Lean Software Development – An Agile Toolkit [Pearson Verlag](https://www.pearson.de/lean-software-development-an-agile-toolkit-an-agile-toolkit-9780133812954)

### Defining the Appropriate Custom Code Strategy

A clearly defined custom code strategy helps you communicate your technology-based investments transparently. Based on this strategy, you can make targeted investment decisions—such as those regarding workforce planning and training initiatives, as well as in-house or outsourced activities—and determine the specific approach to development activities.

* Create a technology radar and use it to unify the selection process for specific technologies and tools. Use the radar to determine which technologies you want to invest in strategically, which ones will only be maintained but not further developed, and which technologies should be withdrawn from in a planned manner. Concentrate on a manageable selection of key technologies to ensure manageability (maintenance cycles, lifecycle management tools, internal expertise, etc.) and to sustainably control the associated complexity. Example: [SAP Tech Radar](https://tobiashofmann.github.io/sap-dev-tech-radar/)
  
* Identify the critical business areas that give your company a competitive advantage or are of existential importance and align the focus of your technology, human resources and software development strategy accordingly.  For example, as a material management or production planning specialist, it makes sense to distribute the knowledge about the customer's own expansion in the variant configuration to an internal development team rather than being dependent on an external service provider in critical cases. Concepts such as [Core Domain Pattern](https://medium.com/nick-tune-tech-strategy-blog/core-domain-patterns-941f89446af5) (Domain Driven Design) or practices from the discipline of Enterprise Architecture Management can support you in your decisions.
  
* Use the [Vermeidungsprinzip](https://blog.codinghorror.com/the-best-code-is-no-code-at-all/) when deciding on the creation of individual developments:  

    1. Before you start developing a new functionality, you should check whether the SAP standard with Customizing and customer extensions would be sufficient.
    2. Check whether your requirement can be solved using an (organizational) workaround.
    3. If this is not the case, or the workaround costs too much, check whether a standard solution from a third-party provider meets your requirements and benefit from the fact that the provider takes care of maintenance and further development (ideally outside of your system landscape).
    4. Only after examining the above options should you consider individual development. Please note that each additional line of code in your namespace requires ongoing support: in addition to the initial development of your new solution, it must be read, debugged and maintained by your employees in the long term, which means additional resources and costs.
  
* Follow official coding standards such as the [SAP ABAP Programming Guidelines](https://help.sap.com/doc/abapdocu_latest_index_htm/latest/en-US/index.htm?file=abenabap_pgl.htm), [SAP Code Style Guides](https://github.com/SAP/styleguides), and the recommendations in this guide. Automate rule checks wherever possible, give developers tools with short feedback cycles and correction suggestions, and supplement automated checks with manual code reviews.
* Define specific types of development and establish development-type-specific quality standards and procedures. For example, a one-time correction program is short-term and purpose-driven, with the focus on efficiency, time savings, and low costs. A developer-on-stack application for customer-specific business processes, on the other hand, requires higher quality standards, as it is used long-term and is regularly expanded and maintained. Here, maintainability, scalability, and the minimization of long-term costs are crucial. The different standards help developers focus on the core task and use their limited time effectively. Additionally, we recommend defining an abstract macro-quality standard as a guideline, from which development-type-specific scenarios can be derived.

* [See example “What is good ABAP code?”]({{ site.baseurl }}/abap/oo-design/#modern-business-applications-require-modern-software-development-practices)



* Define code ownership at the team level. Two roles are crucial for code ownership: On the business side is the Product Owner, who is responsible for prioritizing changes and can make decisions regarding the lifecycle and the appropriateness of technical quality for customer development. On the technical side, this is complemented by an architect/lead developer, who takes responsibility for the conceptual integrity of technical designs and for communicating necessary cleanup tasks within the software architecture under their purview. The package and software component concept is available as a tool to clearly assign technical artifacts to a role.
* Obtain the mandate for the continuous improvement of your customized software. Ensure that your developers can deal with structural optimization for better maintainability using [Refactorings](https://refactoring.com/) or the [Tidy First approach](https://software-architektur.tv/2024/07/26/episode225.html). Make sure there is a balance between functional extensions and structural optimization. Convince stakeholders with numbers, data and facts from the application lifecycle and custom code management and show the causal relationships why it makes sense to invest in code quality.
  
The first draft of a software solution is rarely long-lasting. In companies with a high level of maturity in software development, the first delivery is often based on a conscious decision to go live in a short time with a reduced range of functions and low software quality in order to achieve strategic, market-oriented or operational goals (see [Lean Startup / MVP](https://www.atlassian.com/agile/product-management/minimum-viable-product)). After achieving the goal, companies usually focus on bringing the software quality to an appropriate level to minimize the negative impact on the user experience and long-term stability of the product. If necessary, the first delivery will be completely discarded and redeveloped from scratch with the experience gained and with appropriate quality right from the start.

Companies with a low level of maturity in software development often take a similar approach, with the fatal difference that they make their decision to take on technical debt unconsciously and sooner or later end up in the so-called [C.R.A.P. Cycle](https://visualstudiomagazine.com/articles/2015/07/01/domain-driven-design.aspx). The problem is often exacerbated by a lack of know-how in dealing with [long-lived software architecture](https://www.informatik-aktuell.de/entwicklung/methoden/langlebige-architekturen-technische-schulden-erkennen-und-beseitigen.html) and reduced to absurdity by a change process that is purely focused on expanding functions under high time pressure and little willingness to invest. Be sure to avoid this mistake for an ERP system with a life cycle of 10 - 20 years!

* Establish clear rules for using the version control system. Define how long a transport may remain in the development system before the development must be rolled back and set up appropriate monitoring for this purpose. For system landscapes with multiple production systems and a central development system, specify that the source code must be identical across all production systems. Define how to handle source code used across multiple system landscapes, how to ensure backward compatibility with different release versions, and how to manage namespaces and forks.
  
{: .note }
> - [Langlebige Softwarearchitekturen](https://www.langlebige-softwarearchitekturen.de/)
> - [Refactoring.com](https://refactoring.com/)
> - [Software-Architektur.tv](https://software-architektur.tv/)
> - [SAP Application Extension Methodology](https://help.sap.com/docs/sap-btp-guidance-framework/sap-application-extension-methodology/sap-application-extension-methodology-overview)
> - [SAP Architecture Center](https://architecture.learning.sap.com/)

## Processes and Methodology

If you have a development department, you should also invest in processes and methodologies.

In addition to cultural and technological issues, another key aspect is the organization’s approach from the initial idea or requirement through to the go-live of the corresponding solution. The “how”—that is, the actual development process—varies widely across the market and is strongly influenced by the size of the organization, the industry, the regulatory framework established by a regulator, central guidelines from parent companies, and expertise.

It is therefore not possible to offer a universal recommendation; however, we would like to share a few insights from our experience that can help guide an individualized approach:

* For years, many organizations have been using traditional project management with clearly defined roles, concepts, and deliverables. Changing these process models is, in itself, a major change project that requires a great deal of thought, time, and expertise—and must be implemented consistently over the course of several years.
* It is often suggested that organizations should “become more agile.” Ultimately, stakeholders are frequently dissatisfied with the level of innovation or the speed at which requirements are implemented, and they view agile methods as a suitable tool. In some cases, these suggestions also come from within the development organization itself, as employees there are dissatisfied with current processes.
* Process models, methods, processes, and strategies are context-dependent—not every organization, team, or project is a good fit for every model. Therefore, it makes sense not to start with a declaration like “We’re agile now!” or “We’re doing Scrum now!”, but rather to first assess where challenges and problems exist, in which areas the company wants to improve, and how expertise and resources are distributed. The problem should then be addressed on this basis, rather than a potential solution. Involve the people who perform the value-adding work and who need to solve the problems.
* In some companies, attempts to implement “agile” have failed, giving the term a negative connotation. The causes of this are varied and multifaceted: too little coaching, too much workload combined with a complex project, insufficient training, poor tooling, no reason or willingness to change, “big bang” approaches, etc. If you want to use agile methods, you must take this context—or the history of your company and your employees—into account.
* The desired outcomes of a path toward agility cannot be achieved in isolation: it is of little use if a development department works in an agile manner, but upstream and downstream teams and processes continue to operate as before. For example, if a change advisory board meets only every two months to approve developments, the development department cannot be more flexible than this given framework allows.
* One hope attached to agile methods is that they deliver results more quickly. This is not necessarily the case: Agile methods aim for flexibility, i.e. changing requirements and priorities, as well as quick feedback - the knowledge of how to implement the right thing, since requirements often cannot be sufficiently determined in advance. This addresses three central problems: constant change, uncertainty and communication.
* Methods require a technical foundation and support—if time-consuming manual processes still exist today, you should optimize them.
* There are many strategies and methods that differ in their approach, ideas and degree of freedom. Examples of these are:
* At team level: [Scrum](https://www.scrum.org/), [Kanban](https://de.wikipedia.org/wiki/Kanban_\(Entwicklung\)), [Extreme Programming](https://de.wikipedia.org/wiki/Extreme_Programming), [Scrumban](https://de.wikipedia.org/wiki/Scrumban)
* Cross-team / organization-wide: [LeSS](https://less.works), [Nexus](https://www.scrum.org/resources/scaling-scrum), [SAFe](https://scaledagileframework.com/), Scaled Kanban
  
In addition, “agile” is defined by values and principles, so that no framework is necessary, but each organization can create its own process based on it.

* Within these values and principles, there are also different levels and degrees of maturity along which an organization can develop. The [Kanban Maturity Modell](https://www.kanbanmaturitymodel.com/) is an example of this
  

Whatever change is right for your company—keep in mind that, ultimately, it’s all about people and communication. Try to establish a shared goal, a “unity of purpose,” against which you can measure your approach and resolve conflicts. Otherwise, there is a risk that your initiative will be torn apart by conflicting directions (“fewer rules and structure” vs. “more guidelines”) or interests (e.g., conflicting annual goals among executives). Often, there is also a situation where an agile team still has a project manager or project lead, resulting in a hybrid structure. In this case, it is advisable to assess, within the context of the organization, whether a shift from “projects to products” could be helpful.

## The Status Quo in Mature Landscapes

Based on our experience within the DSAG network, we know that the quality of software development depends heavily on the expertise and motivation of the development teams, as well as on the conditions within the company. Management often lacks the necessary technical understanding.

Requirements imposed from outside or from above rarely have a motivating effect. The result: poor implementation of quality measures or their deliberate circumvention. Short-term incentives, such as the use of gamification elements or direct coaching with experts, can help, but long-term organizational changes are necessary to motivate developers to set high standards for quality and development. This process often begins by raising awareness that high software quality and its positive effects are not merely an implicit or explicit expectation of various stakeholders, but above all also benefit the developers themselves.


### Best Practice

There is a large selection of development standards, which can be found, for example, in the ABAP Guide 2016 [dsag\_handlungsempfehlung\_abap\_2016\_0.pdf](https://www.dsag.de/wp-content/uploads/2021/12/dsag_handlungsempfehlung_abap_2016_0.pdf), [Clean ABAP]({{ site.baseurl }}/abap/clean_and_modern_abap/) and various books. From our point of view, the rough pillars on which there is consensus are:

{: .recommendation}
> - Naming conventions for customer-specific developments, optionally in a separate name space
> - Structured package concept, optionally with clear package interfaces
> - Static code checking (e.g. ATC checks) as part of the transport sector with testing according to the following code criteria: performance, security, compliance, robustness, maintainability, extensibility (ABAP Cloud). See also the DSAG ATC guide [dsag\_leitfaden\_atc\_2020\_06.pdf](https://www.dsag.de/wp-content/uploads/2021/12/dsag_leitfaden_atc_2020_06.pdf)
> - Documentation of public methods/function modules
> - Creation of [appropriate documentation]({{ site.baseurl }}/documentation/documentation_tipps/) .
> - The use of ABAP Unit and Code Coverage
> - Approval process for Classical Extensibility – the so-called Level D developments [see chapter Clean Core]({{ site.baseurl }}/clean-core/solution-approach/)
> - Adaptation of business process and technical documentation after a program change

### Why Should I Change Anything?

The SAP development culture among existing customers is often established and heterogeneous. There are many implementations with different ABAP variants and developer preferences. In contrast, the new S/4HANA technologies, such as On-Stack Extensibility, are based on object-oriented ABAP, Modern ABAP (Syntax 7.4+), ABAP Unit, ABAP Core Data Services, and the ABAP RESTful Application Programming Model. These newer parts of the ABAP language must be used in an S/4HANA system to be able to utilize standard applications, Fiori apps, and standard services.

Modern ABAP development requires development guidelines as a common foundation. Technology stacks are becoming increasingly complex, and a single developer cannot master all of them in depth. However, guidelines alone are not enough.

It is only through organizational changes—such as a development factory, a community of practice, or an interdisciplinary team—that the actual change process begins.

If you are pursuing a Clean Core strategy, it is all the more important that you approach change management correctly. Retraining existing developers will not be enough to bring about change.


### The next step

Without key individuals driving quality, teams tend to prioritize functionality over quality under the constant pressure of project work and departmental demands. Oversight and quality checks are also crucial for external contributors. The initiative needs dedicated lead developers who are intrinsically motivated to support and manage change over the long term (= change management).

There must be a clear vision, a strategy, and defined goals that are supported by management or, ideally, explicitly mandated by senior management. The strict separation of SAP standard code and in-house developments - the so-called Clean-Core strategy - is pursued in order to keep the system maintainable, expandable and capable of development in the long term [see chapter Clean Core]({{ site.baseurl }}/clean-core/solution-approach/). We therefore focus on the vision and implementation of the strategy.


## Practical Experience Report: Brownfield Conversion to S/4HANA

The following example illustrates the implementation of the Clean Core strategy at an SAP customer operating in a mature brownfield environment. Here, a bottom-up approach to change management was adopted; global development teams define the development landscape and guidelines for SAP development through representatives on a Clean Core governance committee.


### Vision

We aim to make effective use of ABAP Cloud technologies and SAP standards. We use custom code correctly, cleanly, and strategically to gain a competitive edge. This allows us to reduce errors and maintenance costs by 90%!


### Implementation

**Year 1**: **"Find the strategy"**

* Defining a clean-core strategy, taking into account various SAP and non-SAP software solutions
* Building a Community of Practice: Senior ABAP Coaches
* Implementation of the initial ATC checks (e.g. Security and HANA Readiness) by focusing on "low-hanging fruit" findings
* Training for ABAP developers, as needed
* Introduction of a package concept that defines responsibilities for all package hierarchies
  

**Year 2** **"Implement the strategy"**

* A phased rollout of Clean Core development
* Definition and implementation of roles for change management: Lead Developer (according to SAFe: Product Architect), responsible for: communicating guidelines in the team, code reviews [see chapter ALM]({{ site.baseurl }}/application-lifecycle-management/ensuring-quality/), pair programming, ATC checks - distributing code findings for your team packages, bringing ABAP unit into the development landscape.
* Procurement of quality assurance tools
* Implementation of code reviews and static code checks as mandatory components of the development process
* Further training for all ABAP developers, in part through train-the-trainer programs


## Final Thoughts

Effectively aligning SAP development teams with corporate goals and the organizational structure is a demanding task that can pose a challenge due to its complexity. We believe that the human factor plays a vital role even in a highly mechanized and technology-driven world. It is worthwhile to invest in a socio-economic system with well-trained and intrinsically motivated employees. The days of Chuck Norris developers and cowboy coders should finally become a thing of the past, replaced by professional teams whose members can learn from one another.

Remember: A system is only as strong as its weakest link. The localized optimization efforts within your development team may only address the symptoms and a small but significant part of your software development process. Look beyond your team’s boundaries and identify the bottleneck that is negatively impacting the entire system. It is often lengthy governance or approval processes that cause cost of delay.  Speak openly with those responsible and support them with numbers, data and facts to improve the overall process. Consistent coordination across all involved processes is the key to unlocking the full potential of your development department—and beyond.
