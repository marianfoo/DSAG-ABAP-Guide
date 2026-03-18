---
layout: page
title: Quality assurance and monitoring
permalink: /application-lifecycle-management/ensuring-quality/
parent: ALM
nav_order: 2
---

{: .no_toc}
# Quality assurance and monitoring

1. TOC
{:toc}

In software development, there are different testing procedures to measure the software quality of your developments at specific points in time. The use of static code analysis tools is widespread, which are used in the software development process to check development activities at specified test times (quality gates) for the validation of development guidelines. For further details on the topic of static code analysis with SAP tools, we would like to refer you to the [DSAG ATC Guide](https://dsag.de/wp-content/uploads/2021/12/dsag_leitfaden_atc_2020_06.pdf) linked below.

In addition, there are software analysis tools that are more holistic in nature and focus on monitoring and the evolutionary development of the software architecture. This tool category offers options for graphically preparing the information from the static code analysis and, for example, depicting it as a trend in a timeline, as a 3D city model or as a heat map. For this purpose, further data about usage behavior, organizational circumstances, such as the number of different developers or the frequency of changes to certain source code artifacts, are read in and used to identify potential hotspots, from which organizational measures for quality improvements can then be derived.

In addition to the processes, practices and tools listed below for identifying quality defects, what is most important is how you deal with the identified defects. According to the motto "Better is the enemy of good", we recommend that you deal appropriately and consciously with the issue of software quality. A suitable definition for this is a [Custom Code Strategie](/ABAP-Leitfaden/organization/#definition-der-passenden-custom-code-strategie) tailored to your company, which specifically specifies which quality standard must be adhered to for which category of development.

## Continuous developer self-review


The earlier a defect is found in software development, the cheaper it is to fix. For developers in particular, these places high demands on their own responsibility to keep an adequate eye on code quality and to eliminate problems at an early stage. Two factors play a crucial role:

1. The developer's discipline to continually check the code for defects
2. The tool the developer works with

>**The development environment used is crucial for the early detection and elimination of defects**

- Do you prefer the ABAP Development Tools for Eclipse (ADT) as a development environment for ABAP: This allows you to access integrated refactoring options, extended syntax highlighting and extended code completion, autocorrection of selected ATC occurrences through quick fixes, inline display of ATC references access the line of code that appears after the ATC test has been carried out and a freely configurable user interface.
- Use the Eclipse ecosystem to increase the efficiency of your developers: By providing the [ADT-SDKs](https://www.sap.com/documents/2013/04/12289ce1-527c-0010-82c7-eda71af511fa.html), there is the possibility of expanding the ABAP development tools via standardized interfaces. As a result, various projects have emerged in recent years that, among other things, offer extensions to the IDE and simplify developer life in many ways. As an example of such an extension, we would like to mention the [ABAP Cleaner](https://github.com/SAP/abap-cleaner), which supports code refactorings that primarily focus on the use of modern ABAP syntax and compliance with a uniform style guide.
- Pay attention to security-relevant conditions when using Eclipse plug-ins: This guide is not intended to be an invitation to use all open source or available Eclipse plug-ins in your productive development environment. Before installing the plug-ins, please pay attention to your company's procedures for security checks and approval processes for the use of new software.

{: .note }
> - [ABAP Open Source Projects](https://dotabap.org/)

## Code Review

Code reviews are an important means of ensuring the quality of the code and sharing knowledge within the team. Code review generally means that a person other than the author reads the code, tries to understand it, and leaves comments and suggestions for improvements.

In many software projects, code reviews are carried out based on so-called *pull requests*. To do this, code changes are made in the version control system on a separate branch and, once the implementation is in an initial complete state, handed over to another member of the team for review. Platforms such as GitHub, GitLab or Azure DevOps offer options for clearly displaying all changes on this branch and adding comments. Evaluation functions are often also available, so that a pull request can only be released if the code review has been completed with positive results. Since there is currently no standard tool for code reviews in SAP development, coordination with non-SAP teams is recommended. If reviews on pull requests in GitHub or Azure DevOps are used, existing prior knowledge in the company can be used when selecting the same tool.

The following section provides some general code review best practices. It will then be discussed to what extent these can be used in ABAP development and what special features may need to be taken into account.

### Best Practices

#### Allgemeine Prinzipien
- Small changes, frequent reviews: Large code changes are harder to keep track of. Instead, reviews should be carried out on manageable units.
- Static analysis as an entry criterion: Only invest manual effort in code reviews when automated procedures such as unit tests and static code analysis no longer find problems in the code.
- Clear expectations: Define within the team what should be checked in a code review. For this purpose, it is recommended to create a common review guideline. Examples are linked below.
- Feedback culture: Code review should not be seen as an additional approval process, but rather as a means of exchanging experiences with the common goal of improving quality. This means that both code author and reviewer should be open to constructive criticism.
- Short review cycles: Long waiting times can slow down the development process. Care should be taken to ensure that changes are reviewed quickly and, if necessary, reworked. For this purpose, it is advisable to agree on and monitor internal goals, such as ensuring that no change has to wait longer than 2 days for code review.

#### For the author
- Code comments: Explain the reasons for certain decisions and the context of the code. If a reviewer doesn't understand the code, they probably won't, even after a few months.
- Review yourself before reviewing: Review the code yourself thoroughly before submitting it for review.
- Be willing to accept changes: Be open to feedback and willing to adapt your code.


#### For the reviewer
- Focus on intention: understand what the author wanted to achieve with the code.
- Be respectful: Feedback should always be about the code, not the person. Questions for understanding are also valuable feedback.
- Be constructive: give concrete suggestions for improvement.
- Focus: Concentrate on topics such as understandability, architecture, algorithms or testability of the code.
- A sense of proportion: A flood of comments can overwhelm the author. If revision is necessary anyway, focus on the most important suggestions first.

{: .note }
> - [ABAP Code Reviews - A practical guide](https://github.com/SAP/styleguides/blob/main/abap-code-review/ABAPCodeReview.md)
> - CQSE Blog "Lessons from Code Review" ([Teil 1](https://teamscale.com/blog/en/news/blog/lessons-from-code-reviews-pt1), [Teil 2](https://teamscale.com/blog/en/news/blog/lessons-from-code-reviews-pt2))
> - [Google Engineering Practices Documentation](https://google.github.io/eng-practices/)

### abapGit

One way to provide ABAP code in a Git repository with support for pull requests is [abapGit](https://abapgit.org) (see also chapter [Version Management](../version-management/)).

In particular, ABAP development teams often rely on a process that includes abapGit for code review. This has been shown by various practical lectures in the Development working group ([Event page on DSAGNet](https://dsagnet.de/event/netzwerk-treffen-ak-development-ag-devops-ag-ui-technologien)). The procedure here is analogous to the non-SAP world: changes are made on a branch and published there via Git commit. This happens either [manually via the abapGit UI](https://docs.abapgit.org/user-guide/projects/online/stage-commit.html) or automatically via a [Background Push](https://docs.abapgit.org/user-guide/repo-settings/background-mode.html).

A [Beispielprojekt](https://github.com/abapGit/abapgit-review-example) is also published on GitHub, which automatically creates or updates a pull request via abapGit when the task is released. According to the authors, however, this should not be seen as a finished product, but rather as a starting point for your own implementation, which is based on the specific requirements and processes of your own company.

### Git-based CTS (gCTS)

Although the SAP style guide explicitly mentions [ABAP Code Reviews - A practical guide](https://github.com/SAP/styleguides/blob/main/abap-code-review/ABAPCodeReview.md) gCTS, it does not currently represent a viable solution for conducting code reviews (as of May 2025). It has several properties that contradict the requirements mentioned above. Specifically:

- Commits are only carried out when the transport is released. Ideally, a code review should be part of the “done criteria” of a transport request. The code must therefore be available *before* in the repository.
- The committer in gCTS is the person who released the transport. The repository does not contain any information about the person who created the code. This makes the discussion during the code review more difficult.

These two points can be solved to a certain extent by custom code, for example by already having [A commit is created when a developer task is released](https://community.sap.com/t5/technology-blogs-by-sap/create-a-commit-in-git-when-an-abap-task-is-released/ba-p/13483954). However, the biggest obstacle to code reviews on gCTS repositories is that neither file paths nor contents in gCTS repositories are easily readable by humans. In some cases, technical identifiers are used as file names; for other object types, the code is displayed on a single line as part of a large JSON structure. For this purpose, SAP, together with the community, has defined the [ABAP File Formats](https://github.com/SAP/abap-file-formats), which addresses the problems mentioned. However, these are currently not implemented in gCTS. The GitHub page of the ABAP File Formats states that this will be the case in the future. However, the authors do not have any concrete schedules or commitments from SAP.

### Fazit

In summary, for conducting reviews for ABAP code, *abapGit* is currently the only viable solution.
However, abapGit is an additional tool that developers must use. Without further adaptation, it does not integrate naturally into existing development processes. A successful solution for code reviews therefore requires some initial effort to ensure the most seamless integration into your own development process.
However, practical examples show that this is certainly possible and can ultimately be a valuable component for developing high-quality code. Last but not least, the fact that SAP itself relies on code reviews in ABAP development should be argument enough to deal with the topic.

## Quality gates in the release process

Before releasing a new feature into the release process, it is recommended to carry out a final and automated quality control that checks the created code for critical security findings and blocks release if there are any hits. This does not mean that you should skip security checks during continuous quality testing or code review. On the contrary! The security check must be an integral part of the other test procedures so that you can react to this sensitive issue at an early stage. Rather, the quality gate in the release process is the final control instance to detect and prevent the unintentional or intentional introduction of security gaps before they are imported into downstream systems. The test serves as an assurance that no vulnerability that can be identified by static code analysis tools can escape your notice.

All other findings, such as violations of maintainability, robustness and efficiency criteria, should be appropriately addressed in advance through the developer's continuous quality check and the code review process. If you neglect the upstream checks, you either end up with unhappy business users who have to put off waiting for a new release date because of serious quality defects that were discovered too late, or in an increasingly complex, difficult to understand and maintenance-intensive system in the long run. You should definitely avoid both scenarios and carry out quality checks early and continuously.

**Quality Gate Support Processes**

- Define a procedure for systematically identifying false positive reports and exceptions during quality control. Static code analysis tools usually offer mechanisms with which you can suppress the identified findings accordingly. Avoid bottlenecks and use the process before the final quality control.
- When introducing quality control processes, use the so-called baseline procedure to suppress quality reports that arose before the introduction of the quality control process. This is particularly useful in existing systems with a large code base of old developments where you want to distinguish messages from the existing code from newly added quality defects. Be careful not to include safety-critical tests in the baseline. These must be considered separately, analyzed and, if necessary, excluded via a false positive report or resolved in a separate correction initiative.
- Adopt a zero-tolerance strategy for security-critical locations in customer and partner code. SAP ERP systems are a popular target for cybercrime due to their central roles in corporate IT. An unrecognized or intentionally installed security vulnerability can lead to operational interruptions and [erheblichen finanziellen Schaden](https://onapsis.com/de/blog/sap-security-breach-cited-in-companys-bankruptcy/). If your stakeholders nevertheless force you to grant an exception, request the support of your information security officer in the company and clarify whether a risk acceptance process has been defined for such a need. Further information on this topic can be found in chapter [Sicher ABAP Programmierung](/ABAP-Leitfaden/security/).
- Perform a security review of all source code artifacts before incorporating them into your system. Have SAP add-on providers provide you with extinguishing transport before you import their products into your system. Import and scan third-party transports for the first time only in a sandbox system if they do not provide you with a deletion transport.<br>
Please contact your purchasing department or the contract management department in your company if the provider is uncooperative and does not provide you with corrections to the findings or detailed false positive descriptions.<br>
Do not take any legal risks and refrain from publishing the identified vulnerabilities. Under German law (see [$202c Strafgesetzbuch](https://www.gesetze-im-internet.de/stgb/__202c.html)), the use or publication of exploits may be considered a preparatory act for a criminal offense. In hardship cases, it makes sense to speak to an IT lawyer or contact a recognized body such as the [Federal Office for Information Security - BSI](https://www.bsi.bund.de/DE/Service-Navi/Kontakt/Kontaktformular/kontaktformular_node.html) or a bug bounty platform.

**Manipulation of Quality Gates**

- Pay attention to the implementation of a manipulation-free testing and release process: The freedom that a developer has in the development system can represent a challenge that should not be underestimated in time-critical situations (development and quality assurance distributed in several time zones / decentralized release management / etc.). Especially in companies that have no upstream continuous self-control by the developer, a lack of pair programming or code review processes, releases that are too large and spread out over long periods of time, this can lead to developers with a fixed delivery date on their backs tending to react in short-circuits and override the quality gates and associated quality checks via the existing debug and replace authorizations. Manipulation of the testing and release process can only be detected through continuous monitoring of debug and replace activities in the system log (SM21) and can only be partially prevented through authorization restrictions for the release of transport requests and transport tasks. Resourceful developers almost always find a way to bypass existing quality gates.
- Fix the cause of the problem, not just the symptom: When detecting quality gate manipulation, it is advisable to first talk to the developer and identify the cause that led to the need for manipulation. Often the "hardship" under which the developer acts is due to ignorance of the development process or a lack of flexibility in the development process. It is helpful to invest in lightweight and easily understandable on-boarding material for the developer and those involved in the process. Additionally, an awareness initiative within product teams about the need for early and ongoing quality assurance measures may be useful.
- Take consistent action in the event of repeat cases and non-compliance with the processes: To do this, you must have coordinated the process in advance with the management and decision-making level and obtain authorization to act. Of course, the psychological safety of the developers has a high priority, which is why, in the event of first or second violations, a conversation with the developer must be sought in a confidential manner. At the third occurrence at the latest, it can be assumed that there has been fraudulent deception or intentional damage to the company. Especially if security vulnerabilities are leaked, a cybersecurity incident can be assumed that could have legal consequences. Unless there is an alibi-free justification, such intended security incidents should be consistently punished the first time they occur.  

## Holistic view and continuous quality control

Continuous quality control represents a strategic approach that serves to sustainably protect your investments in customer-specific developments. The aim is to identify potential weak points and critical development patterns at an early stage in order to specifically optimize system security, performance, maintainability and portability.

A central instrument in this context are modern custom code analytics tools. These offer more extensive analysis options than classic static code analysis tools. While static code analysis focuses primarily on checking syntax, style guidelines and known programming errors, custom code analytics tools take a more comprehensive approach: They analyze customer-specific developments in the overall context of the system - taking into account frequency of use, performance effects, upgrade compatibility and dependencies on standard modules and other in-house developments.

Another added value lies in the ability of these tools to perform hotspot analysis. This involves identifying code areas that are changed disproportionately often, have a high level of complexity or have proven to be particularly maintenance-intensive. This enables targeted prioritization of refactoring measures and contributes substantially to increasing long-term code quality and system stability.

In addition to technical optimization, the use of Custom Code Analytics also opens up considerable economic potential: By identifying and eliminating duplicate or no longer used code as well as detecting outdated or critical standard module usage, maintenance efforts can be reduced, upgrade projects can be simplified and unnecessary license or development costs can be avoided.

For SAP Business Suite customers with SAP Enterprise Support, the SAP Solution Manager from version 7.2 SP5 contains a compilation of tools that offer a very extensive portfolio of analysis and administration tools under the term Custom Code Lifecycle Management. A well-known representative of these tools is the Custom Code Decommissioning Cockpit, which is often used when preparing migration projects from SAP ECC to SAP S/4HANA in order to cost-effectively decommission customer code that is no longer used before migration. You can find a detailed description of the functionality with presentation material and videos in the linked Expert Content [Custom Code Management with SAP Solution Manager](https://help.sap.com/docs/SUPPORT_CONTENT/sm/3627184393.html?locale=en-US).

Unfortunately, to this day (as of May 2025) there is still no official known adequate successor product for Custom Code Lifecycle Management in the SAP Solution Manager that comes close to covering its scope and performance. Instead, there are scattered, specialized isolated solutions and services that unfortunately only ensure point-in-time analyses, but not holistic and evolutionary monitoring (SAP for Me Custom Code Analytics Application, S/4HANA Readiness Check, Clean Core Cockpit, Intelligent Custom Code Management Service). Especially in view of the technology-open ecosystem in the SAP environment, it makes sense to exchange ideas with colleagues from other technology areas and, as an alternative, to access a software analysis tool with ABAP evaluation options that already exists in your company.

In addition to the tools offered by the SAP, there are a number of commercial and available tools that differ greatly from one another in terms of functionality, scope of services, support and further development. As potential representatives and without making a recommendation for the tools, we would like to briefly introduce you to the following candidates:

[**ABAP2CodeCharta**](https://github.com/BenjaminWeisheit/ABAP-2-CODE-CHARTA)

ABAP2CodeCharta is an open source tool that converts ABAP source code into a CodeCharta format. It is used to visualize ABAP code structures in so-called code cities, i.e. three-dimensional representations in which e.g. B. Complexity, size or frequency of changes of code components can be visually recorded. The tool supports hotspot detection, promotes understanding of large code bases and helps prioritize refactoring measures.

[**Teamscale**](https://teamscale.com/)

Teamscale is a commercial custom code analytics tool for continuous analysis and evaluation of software quality. It supports many programming languages ​​(including ABAP) and combines static code analysis with usage evaluations, change behavior and architecture metrics. Teamscale recognizes e.g. E.g. technical debt, unused or redundant code, hotspots and quality policy violations. It offers dashboards, trends and integrations into DevOps processes and is a tool for sustainable quality control, especially in complex corporate landscapes.

{: .note }
> - [Intelligent Custom Code Management](https://community.sap.com/t5/enterprise-resource-planning-blogs-by-sap/intelligent-custom-code-management/ba-p/13472631)
> - [Managing Custom Code - SAP Cloud ALM or SAP Solution Manager?](https://community.sap.com/t5/enterprise-resource-planning-blog-posts-by-sap/managing-custom-code-sap-cloud-alm-or-sap-solution-manager/ba-p/13524454)
