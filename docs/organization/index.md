---
layout: page
title: organization
permalink: /organization/
nav_order: 1
---

{: .no_toc}
# Organization

1. TOC
{:toc}

Why should management invest in software quality and a well-positioned development organization? Software quality as a basis is usually implicitly and automatically expected by stakeholders, but necessary measures are often given little support because “There is no glory in prevention”.

From a management perspective, such an investment (time, resources, tooling) needs to be backed up with a business case, which is easiest to develop individually for your company if you take a look at the current problems of your company and its IT. If you recognize some of these, optimizing your development department and culture with a focus on quality and technologies could be a solution:

* (too) slow implementation of innovations and legal requirements compared to their competitors
* Dissatisfied end customers due to IT issues, errors, processes or SLAs not being met, etc.
* Incorrect processes and data in your systems with corresponding effort for corrections
* Permanent overload of the IT department, tendency to burnout, staff turnover, knowledge silos, loss of knowledge
* Difficult cooperation between specialist departments and IT
* Implementations do not meet the technical requirements of the departments
* Long project durations and feedback processes, high need for rework
* Historically grown complex system constellations and code bases

The solutions to these problems can usually be divided into two categories, for which this DSAG guide and other guides show possible solution options:

* Cultural-organizational: Cross-sectional teams, dissolution of silos, clear distribution of roles and responsibilities, trust, communication structures, common goal and vision, promotion of cooperation instead of competition, etc.
* Software quality: automation, professional testing, development guidelines, software architecture management, enterprise architecture management (EAM), targeted training, pair programming, code reviews, community of practice etc.
    

Parts of these solutions can be quick wins for you as a company or they can be evaluated and made sustainable with small germ cells. It is worth taking a look at what has been going on in the area of ​​software engineering outside the SAP world for many years and adapting it. The following chapter gives you an outlook on this.


## Building blocks of an effective development organization

From a company perspective, the transformation into a successful S/4HANA technology team represents a complex and often underestimated challenge. Depending on the level of maturity and the orientation of your IT organization, an adjustment of cultural and organizational adjustment screws is necessary in order to achieve the strategic goal.

The greater the proportion of customer-specific adaptation and expansion of your existing SAP software is or should be strategic (see [Chapter Clean Core]({{ site.baseurl }}/clean-core/problems-and-challenges/)), the more important is the entrepreneurial focus on the efficiency and effectiveness of your development organization. The following excerpt touches on what we believe to be the most important subject areas that will support you on your way to becoming a successful development organization.


### Definition of the appropriate structural and process organization

The orientation of your development organization depends on the amount, complexity and frequency of customer adjustments in your SAP systems (_Make-or-Buy_ _or “Do nothing”_ _Decision_). If you are one of the customers who can use SAP software as part of standard software without major adjustments, investing in your own SAP development department is generally not worth it from an economic perspective. In this case, it is recommended to rely on external specialists with the appropriate core competence and reputation and to handle the small amount of customer adjustments in the SAP system under the umbrella of defined documentation guidelines (change documentation, operating manuals, etc.) and clearly defined service levels / KPIs.  The exact nature of the decision depends on the individual case in your company and can vary from minor changes to complete platform operation by your own team or an external service partner.

If there is a need to frequently adapt your SAP systems due to a lack of functionality in your core business processes, or the necessary integration of unique selling points that give you competitive advantages through customer-specific development, it is worth considering investing in your own SAP development organization. Building a successful development organization is a complex project and, in addition to technological issues, must pay particular attention to socio-economic aspects. Use the following points to adapt the adjustment screws in your company to your needs.


### Team organization and team composition

Software development teams are the key element for the successful implementation and implementation of your development projects. This is where the music plays when it comes to pouring the technical requirements into technology and keeping the solution cost-effective and maintainable for decades. In order for the team to be able to meet this requirement, it must be equipped and supported with the appropriate skills, resources and processes. For example, if you notice that your teams are spending significant time and energy trying to protect themselves from blame from other teams, or that there are long waits between steps in their software development process, this could be an indication of a suboptimal team performance that urgently needs to be optimized. Attached you will find some recommendations for action to avoid problems with team organization.

* The right team composition is essential for the effective completion of the tasks assigned to the team. The size of the team, cultural background, professional and technical competence and the equipment available play an important role. Make sure that the team can carry out all tasks to fulfill tasks and deliver results independently if possible and that dependencies on upstream and downstream processes are as low as possible.
* When putting together a team, take the professional and technical complexity into account. Especially in the SAP environment, managing complexity in the different application areas is often a challenge. In addition to the technical context, the team also has to deal with application-specific frameworks, customer existing code, technology trends and different technology stacks. Make sure that the team does not work in too many different areas of responsibility and can instead focus on a manageable area, such as a technical module. Take your team seriously if they complain that they are dealing with too much complexity. Otherwise, you risk long-term health damage and negative productivity through too frequent context switching and cognitive overload of the team.
* Pay particular attention to ensuring that developers can concentrate on their core competency, designing and creating high-quality software, and do not have to additionally worry about issues such as requirements management or process documentation. An exception here is the time-limited implementation of these activities in order to capture the technical problem domain more precisely and to better understand the underlying concepts. As a rule, a deeper understanding of the problem domain leads to more efficient software design and thus creates added value for the developer.
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

### Definition of the appropriate custom code strategy

A clearly defined custom code strategy supports you in transparently communicating your technology-based investments. Based on the defined strategy, targeted investment decisions can be made, such as in personnel planning and training measures, as well as in- or outsourcing activities, and the specific handling of development activities can be determined.

* Create a technology radar and use it to unify the selection process for specific technologies and tools. Use the radar to determine which technologies you want to invest in strategically, which ones will only be maintained but not further developed, and which technologies should be withdrawn from in a planned manner. Concentrate on a manageable selection of key technologies to ensure manageability (maintenance cycles, lifecycle management tools, internal expertise, etc.) and to sustainably control the associated complexity. Example: [SAP Tech Radar](https://tobiashofmann.github.io/sap-dev-tech-radar/)
    
* Identify the critical business areas that give your company a competitive advantage or are of existential importance and align the focus of your technology, human resources and software development strategy accordingly.  For example, as a material management or production planning specialist, it makes sense to distribute the knowledge about the customer's own expansion in the variant configuration to an internal development team rather than being dependent on an external service provider in critical cases. Concepts such as [Core Domain Pattern](https://medium.com/nick-tune-tech-strategy-blog/core-domain-patterns-941f89446af5) (Domain Driven Design) or practices from the discipline of Enterprise Architecture Management can support you in your decisions.
    
* Use the [Vermeidungsprinzip](https://blog.codinghorror.com/the-best-code-is-no-code-at-all/) when deciding on the creation of individual developments:  

    1. Before you start developing a new functionality, you should check whether the SAP standard with Customizing and customer extensions would be sufficient.
    2. Check whether your requirement can be solved using an (organizational) workaround.
    3. If this is not the case, or the workaround costs too much, check whether a standard solution from a third-party provider meets your requirements and benefit from the fact that the provider takes care of maintenance and further development (ideally outside of your system landscape).
    4. Only after examining the above options should you consider individual development. Please note that each additional line of code in your namespace requires ongoing support: in addition to the initial development of your new solution, it must be read, debugged and maintained by your employees in the long term, which means additional resources and costs.
    
* Follow official coding standards such as [SAP ABAP Programmierrichtlinien](https://help.sap.com/doc/abapdocu_latest_index_htm/latest/en-US/index.htm?file=abenabap_pgl.htm), [SAP Code Style Guides](https://github.com/SAP/styleguides) and of course the recommendations from the current document. Ensure that rule checking is carried out automatically where possible, that developers use tools with short feedback cycles and correction suggestions, and that manual code reviews also take place in addition to automatic rule checking.
* Define specific development types and establish development type-specific quality standards and procedures. For example, a one-off correction program is short-term and dedicated to a specific purpose, which focuses on efficiency, time savings and low costs. A developer-on-stack application for customer-specific business processes, on the other hand, requires higher quality standards because it is used long-term, regularly expanded and maintained. Maintainability, scalability and minimizing long-term costs are crucial here. The different standards help developers to concentrate on the core task and use their limited time effectively. In addition, we recommend defining an abstract macro quality standard as a guideline, on the basis of which development type-specific scenarios can be derived.

* [See example “What is good ABAP code?”]({{ site.baseurl }}/abap/oo-design/#moderne-gesch%C3%A4ftsanwendungen-erfordern-moderne-softwareentwicklungsmethoden)


 
* Regulate the assignment of code ownership at the team level. Two roles are crucial in code ownership: On the technical side is the product owner, who is responsible for prioritizing changes and can make statements about the life cycle and the appropriateness of the technical quality for customer development. On the technical side, this is supplemented by an architect/lead developer who takes responsibility for the conceptual integrity of technical concepts and for communicating necessary clean-up work in the software architecture for which they are responsible. The package and software component concept is available as a tool for clearly assigning technical artifacts to a role.
* Obtain the mandate for the continuous improvement of your customized software. Ensure that your developers can deal with structural optimization for better maintainability using the [Refactorings](https://refactoring.com/) or the [Tidy First Ansatz](https://software-architektur.tv/2024/07/26/episode225.html). Make sure there is a balance between functional extensions and structural optimization. Convince stakeholders with numbers, data and facts from the application lifecycle and custom code management and show the causal relationships why it makes sense to invest in code quality.
    
The first draft of a software solution is rarely long-lasting. In companies with a high level of maturity in software development, the first delivery is often based on a conscious decision to go live in a short time with a reduced range of functions and low software quality in order to achieve strategic, market-oriented or operational goals (see [Lean Startup / MVP](https://www.atlassian.com/agile/product-management/minimum-viable-product)). After achieving the goal, companies usually focus on bringing the software quality to an appropriate level to minimize the negative impact on the user experience and long-term stability of the product. If necessary, the first delivery will be completely discarded and redeveloped from scratch with the experience gained and with appropriate quality right from the start.

Companies with a low level of maturity in software development often take a similar approach, with the fatal difference that they make their decision to take on technical debt unconsciously and sooner or later end up in the so-called [C.R.A.P. Cycle](https://visualstudiomagazine.com/articles/2015/07/01/domain-driven-design.aspx). The problem is often exacerbated by a lack of know-how in dealing with [langlebiger Softwarearchitektur](https://www.informatik-aktuell.de/entwicklung/methoden/langlebige-architekturen-technische-schulden-erkennen-und-beseitigen.html) and reduced to absurdity by a change process that is purely focused on expanding functions under high time pressure and little willingness to invest. Be sure to avoid this mistake for an ERP system with a life cycle of 10 - 20 years!

* Establish clear rules for dealing with the version control system. Define how long a transport can remain in the development system until the development has to be dismantled and set up appropriate monitoring for this. For system landscapes with multiple productive systems and a central development system, specify that the source code must be identical in all productive systems. Define how to handle source code that is used across multiple system landscapes, how to ensure backward compatibility with different release levels, and how to handle namespaces and forks.
    
{: .note }
> - [Langlebige Softwarearchitekturen](https://www.langlebige-softwarearchitekturen.de/)
> - [Refactoring.com](https://refactoring.com/)
> - [Software-Architektur.tv](https://software-architektur.tv/)
> - [SAP Application Extension Methodology](https://help.sap.com/docs/sap-btp-guidance-framework/sap-application-extension-methodology/sap-application-extension-methodology-overview)
> - [SAP Architecture Center](https://architecture.learning.sap.com/)

## Processes and methodology

If you have a development department, you should also invest in processes and methodology.  
In addition to cultural and technological issues, an important aspect is the organization's approach from the point of the idea or requirement to the go live of the corresponding solution. The “HOW”, i.e. the lived development process, is diverse in the market and strongly influenced by the size of the organization, industry, legal framework by a regulator, central specifications from parent companies and know-how.

A general recommendation cannot therefore be given, but we would like to share a few points from our experiences that enable a classification for an individual approach:

* Many organizations have been doing classic project management with clearly defined roles, concepts and artifacts for years. Changing these process models is in itself a major change project that requires a lot of thought, time and know-how. Consistently and over the years.
* Often a suggestion is to “become more agile”. Ultimately, stakeholders are often dissatisfied with the innovative strength or speed of implementation of requirements and see agile methods as a suitable instrument. Some of these suggestions also come from the development organization itself, as employees there are dissatisfied with the current processes.
* Procedure models, methods, processes and strategies are context-dependent - not every organization, team or project makes sense for every model. Therefore, it makes sense not to use the statement “We are now agile!” or “We’re doing Scrum now!” to start, but first to check where challenges and problems exist, in which areas the company would like to improve and how the know-how and resources are distributed. The problem should then be addressed on this basis and not a potential solution. Include the people who need to do the value-added work and solve the problems.
* There are some failed implementations of “agile” in companies, so this word has a negative connotation. The causes for this are varied and multifactorial: too little coaching, too much load in combination with a complex project, too little training, poor tooling, no reason or willingness to change, big bangs, etc. If you want to use agile methods, you have to take this context or the history of your company and employees into account.
* The desired results of a path to agility cannot be achieved in isolation: It is of little use if a development department works agilely, but upstream and downstream teams and processes continue to work as before. For example, if a Change Advisory Board only meets every 2 months to release developments, the development department cannot be more flexible than this given framework allows.
*One hope attached to agile methods is that they deliver results more quickly. This is not necessarily the case: Agile methods aim for flexibility, i.e. changing requirements and priorities, as well as quick feedback - the knowledge of how to implement the right thing, since requirements often cannot be sufficiently determined in advance. This addresses three central problems: constant change, uncertainty and communication.
* Methods require a technical basis and support - if complex manual processes still exist today, they should be optimized.
* There are many strategies and methods that differ in their approach, ideas and degree of freedom. Examples of these are:
* At team level: [Scrum](https://www.scrum.org/), [Kanban](https://de.wikipedia.org/wiki/Kanban_\(Entwicklung\)), [Extreme Programming](https://de.wikipedia.org/wiki/Extreme_Programming), [Scrumban](https://de.wikipedia.org/wiki/Scrumban)
* Cross-team / organization-wide: [LeSS](https://less.works), [Nexus](https://www.scrum.org/resources/scaling-scrum), [SAFe](https://scaledagileframework.com/), Scaled Kanban
    
In addition, “agile” is defined by values ​​and principles, so that no framework is necessary, but each organization can create its own process based on it.

* Within these values ​​and principles, there are also different levels and degrees of maturity along which an organization can develop. The [Kanban Maturity Modell](https://www.kanbanmaturitymodel.com/) is an example of this
    

Whatever change is good for your company, remember that ultimately it's about people and communication. Try to create a common goal, a “unity of purpose” against which you can measure your actions and resolve conflicts. Otherwise, there is a risk that your initiative will be crushed by different directions (“less rules and structure” vs. “more guidelines”) or interests (e.g. conflicting annual goals from managers). There is often a constellation in which an agile team still has a project manager or project manager, which creates a hybrid structure. In this case, it is advisable to examine in the context of the organization whether a switch from “projects to products” can be helpful.

## Status quo in established landscapes

From our experience in the DSAG network, we know: The quality of software development depends heavily on the competence and motivation of the development teams and the conditions within the company. Management often lacks technical understanding. Instructions from outside or above rarely have a motivating effect. The result: inadequate implementation of quality measures or their deliberate circumvention. Short-term incentives, such as the use of gamification elements or direct coaching with experts, can help, but long-term organizational changes are necessary to motivate developers to set high quality and development standards. This process often begins with creating awareness that high software quality and its positive effects are not an implicit or explicit requirement of various stakeholders, but above all help the developers themselves.


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

### Why should anything change?

The SAP development culture among existing customers is often evolved and heterogeneous. There are many implementations with different ABAP variants and developer preferences. In contrast, the new S/4HANA technologies such as *On-Stack Extensibility* are based on object-oriented ABAP, *Modern ABAP* (Syntax 7.4+), ABAP Unit, ABAP Core Data Services and the ABAP RESTful Application Programming Model. These newer parts of the ABAP language must be used in a S/4HANA system to use standard applications, Fiori apps and standard services.

Modern ABAP development requires development guidelines as a common basis. The “technology stacks” are becoming increasingly extensive and a developer cannot master all technologies in depth. However, guidelines alone are not enough.

Only through organizational changes, such as a development factory, community of practice or an interdisciplinary team, does the actual change process begin. If you are pursuing a Clean-Core strategy, then it is even more important that you approach change management correctly. Retraining existing developers will not be enough to embrace change.


### The next step

Without key people driving quality, teams tend to prioritize functionality over quality under the constant pressure of project work and discipline. Control and quality checks are also crucial for external contributors. The initiative requires dedicated lead developers who are intrinsically motivated to support and manage changes over the years (= change management).

There must be a clear vision, strategy and defined goals that are supported by management, or ideally explicitly requested by senior management. The strict separation of SAP standard code and in-house developments - the so-called Clean-Core strategy - is pursued in order to keep the system maintainable, expandable and capable of development in the long term [see chapter Clean Core]({{ site.baseurl }}/clean-core/solution-approach/). We therefore focus on the vision and implementation of the strategy.


## Experience report from practice: Brownfield in S/4HANA

The following example is intended to show the implementation of the Clean Core strategy using a SAP customer in a grown brownfield. The bottom-up approach to change management was chosen here; The global development teams define the development landscape and the guidelines in SAP development through representatives in a Clean-Core governance committee.


### Vision

We want to effectively use the ABAP Cloud technologies and the SAP standard. We use custom code correctly, cleanly and specifically to gain competitive advantages. This means we reduce errors and maintenance effort by 90%!


### Umsetzung

**Jahr 1**: **„Strategie finden“**

* Definition of a Clean-Core strategy, considering various SAP and non-SAP software
* Building a Community of Practice: Senior ABAP Coaches
* Activation of the first ATC checks (e.g. Focus Security, HANA Readiness) based on the "low hanging fruits"
* Training ABAP developers where needed.
* Introducing a package concept with naming of responsibilities for all package hierarchies.
    

**Jahr 2** **„Strategie umsetzen“**

* A phased rollout of Clean-Core development
* Definition and implementation of roles for change management: Lead Developer (according to SAFe: Product Architect), responsible for: communicating guidelines in the team, code reviews [see chapter ALM]({{ site.baseurl }}/application-lifecycle-management/ensuring-quality/), pair programming, ATC checks - distributing code findings for your team packages, bringing ABAP unit into the development landscape.
* Procurement of tools for quality assurance
* Introducing code reviews and static code checks as mandatory elements of the development process
* Further training for all ABAP developers, partly through train-the-trainers


## Final Thoughts

Effectively aligning SAP development teams with company goals and organizational structure is a demanding task that can pose a significant challenge due to its complexity. We believe that the human factor plays an essential role even in a highly mechanical and technology-oriented world. It is worth investing in a socio-economic system with well-trained and intrinsically motivated employees. The days of Chuck Norris developers and cowboy coders should finally be a thing of the past and replaced by professional teams whose members can learn from each other.

Remember: a system is only as good as the weakest link in its chain. The localized optimization measures in your development team may only alleviate symptoms and a small but essential part of your software development process. Look beyond your team boundaries and find the bottleneck that is negatively affecting the entire system. It is often lengthy governance or approval processes that cause cost of delay.  Speak openly with those responsible and support them with numbers, data and facts to improve the overall process. Consistent coordination across all processes involved is the key to unlocking the full potential of your development department – ​​​​and beyond.
