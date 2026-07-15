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

In software development, there are various testing methods used to measure the software quality of your developments at specific points in time. The use of static code analysis tools is widespread; these are employed in the software development process to review development activities at defined checkpoints (quality gates) for the validation of development guidelines. For further details on the topic of static code analysis with SAP tools, we would like to refer you to the [DSAG ATC Guide](https://dsag.de/wp-content/uploads/2021/12/dsag_leitfaden_atc_2020_06.pdf) linked below.

In addition, there are software analysis tools with a more holistic focus that concentrate on the monitoring and evolutionary development of the software architecture. This category of tools offers options for graphically presenting information from static code analysis and visualizing it, for example, as a trend on a timeline, as a 3D city model, or as a heatmap. To this end, additional data on usage behavior and organizational factors – such as the number of different developers or the frequency of changes to specific source code artifacts – is incorporated and used to identify potential hot spots, from which organizational measures for quality improvements can then be derived.

In addition to the processes, practices and tools listed below for identifying quality defects, what is most important is how you deal with the identified defects. In keeping with the adage “The best is the enemy of the good,” we recommend that you approach the topic of software quality in a measured and deliberate manner. A suitable definition for this is a [custom code strategy]({{ site.baseurl }}/organization/#defining-the-appropriate-custom-code-strategy) tailored to your company, which specifically specifies which quality standard must be adhered to for which category of development.

## Continuous developer self-review


The earlier a defect is found in software development, the less costly it is to fix. This places a high demand on the developer’s personal responsibility to adequately monitor code quality and resolve issues early on. Two factors play a crucial role:

1. The developer’s discipline in continuously checking the code for defects
2. The tool the developer uses

>**The development environment used is crucial for the early detection and elimination of defects**

- Do you prefer the ABAP Development Tools for Eclipse (ADT) as a development environment for ABAP: This allows you to access integrated refactoring options, extended syntax highlighting and extended code completion, autocorrection of selected ATC occurrences through quick fixes, inline display of ATC references access the line of code that appears after the ATC test has been carried out and a freely configurable user interface.
- Use the Eclipse ecosystem to increase the efficiency of your developers: By providing the [ADT-SDKs](https://www.sap.com/documents/2013/04/12289ce1-527c-0010-82c7-eda71af511fa.html), there is the possibility of expanding the ABAP development tools via standardized interfaces. This has led to the emergence of various projects in recent years that, among other things, offer IDE extensions and simplify developers’ work in many ways. As an example of such an extension, we would like to mention the [ABAP Cleaner](https://github.com/SAP/abap-cleaner), which supports code refactorings that primarily focus on the use of modern ABAP syntax and compliance with a uniform style guide.
- Pay attention to security-relevant conditions when using Eclipse plug-ins: This guide is not intended to be an invitation to use all open source or available Eclipse plug-ins in your productive development environment. Before installing the plug-ins, please follow your company’s established procedures for security checks and approval processes regarding the use of new software.

{: .note }
> - [ABAP Open Source Projects](https://dotabap.org/)

## Code Review

Code reviews are an important tool for ensuring code quality and sharing knowledge within the team. A code review is generally defined as a process in which a person other than the author reads the code, attempts to understand it, and provides comments and suggestions for improvement.

In many software projects, code reviews are conducted based on so-called pull requests. To do this, code changes are made in the version control system on a separate branch, and as soon as the implementation is in a complete initial state, it is handed over to another team member for review. Platforms such as GitHub, GitLab, or Azure DevOps offer features to clearly display all changes on this branch and add comments. In addition, rating functions are often available, so that a pull request, for example, can only be approved if the code review has been completed with a positive result. Since there is currently no standard tool for code reviews in SAP development, coordination with non-SAP teams is recommended. If those teams use reviews on pull requests in GitHub or Azure DevOps, selecting the same tool allows you to leverage existing expertise within the company.

The following section provides some general best practices for code reviews. It then discusses the extent to which these can be applied in ABAP development and what specific considerations may need to be taken into account.

### Best Practices

#### General principles
- Small changes, frequent reviews: Large code changes are harder to keep track of. Instead, reviews should be carried out on manageable units.
- Static analysis as an entry criterion: Only invest manual effort in code reviews when automated procedures such as unit tests and static code analysis no longer find problems in the code.
- Clear expectations: Define within the team what should be checked in a code review. For this purpose, it is recommended to create a common review guideline. Examples are linked below.
- Feedback culture: Code review should not be seen as an additional approval process, but rather as a means of exchanging experiences with the common goal of improving quality. This means that both code author and reviewer should be open to constructive criticism.
- Short review cycles: Long waiting times can slow down the development process. Care should be taken to ensure that changes are reviewed quickly and, if necessary, reworked. To this end, it is recommended to agree on and monitor internal goals, such as ensuring that no change has to wait longer than two days for a code review.

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
> - CQSE Blog "Lessons from Code Review" ([Part 1](https://teamscale.com/blog/en/news/blog/lessons-from-code-reviews-pt1), [Part 2](https://teamscale.com/blog/en/news/blog/lessons-from-code-reviews-pt2))
> - [Google Engineering Practices Documentation](https://google.github.io/eng-practices/)

### abapGit

One way to provide ABAP code in a Git repository with support for pull requests is [abapGit](https://abapgit.org) (see also chapter [Version Management](../version-management/)).

ABAP development teams, in particular, often rely on a process that includes abapGit for code review. This has been shown by various practical lectures in the Development working group ([Event page on DSAGNet](https://dsagnet.de/event/netzwerk-treffen-ak-development-ag-devops-ag-ui-technologien)). The procedure here is similar to that in the non-SAP world: changes are made on a branch and published there via a Git commit. This happens either [manually via the abapGit UI](https://docs.abapgit.org/user-guide/projects/online/stage-commit.html) or automatically via a [Background Push](https://docs.abapgit.org/user-guide/repo-settings/background-mode.html).

A [sample project](https://github.com/abapGit/abapgit-review-example) is also published on GitHub, which automatically creates or updates a pull request via abapGit when the task is released. According to the authors, however, this should not be seen as a finished product, but rather as a starting point for your own implementation, which is based on the specific requirements and processes of your own company.

### Git-based CTS (gCTS)

Although the SAP style guide [ABAP Code Reviews – A Practical Guide](https://github.com/SAP/styleguides/blob/main/abap-code-review/ABAPCodeReview.md) explicitly mentions gCTS, gCTS does not currently provide a viable solution for conducting code reviews (as of May 2025). Several of its characteristics conflict with the requirements described above:

- Commits are not executed until the transport is released. Ideally, a code review should be part of a transport request’s “done criteria.” Consequently, the code must be available in the repository beforehand.
- The committer in gCTS is the person who approved the transport. The repository contains no information about the person who created the code. This complicates discussions during the code review.

Custom code can mitigate these two issues to some extent, for example by [creating a commit when a developer task is released](https://community.sap.com/t5/technology-blogs-by-sap/create-a-commit-in-git-when-an-abap-task-is-released/ba-p/13483954). However, the greatest obstacle to code reviews in gCTS repositories is that neither the file paths nor the file contents are consistently human-readable. Some object types use technical identifiers as filenames; others represent code on a single line inside a large JSON structure. SAP and the community have defined [ABAP File Formats](https://github.com/SAP/abap-file-formats) to address these problems, but they are not yet implemented in gCTS. Although the project states that support is planned, the authors are not aware of a concrete schedule or commitment from SAP.

### Conclusion

In summary, abapGit is currently the only viable solution for conducting ABAP code reviews.
However, abapGit is an additional tool that developers must use. Without further customization, it does not integrate naturally into existing development processes. A successful solution for code reviews therefore requires some initial effort to ensure the smoothest possible integration into your own development process.
Practical examples, however, show that this is entirely possible and can ultimately be a valuable component in the development of high-quality code. Not least, the fact that SAP itself relies on code reviews in ABAP development should be reason enough to address this topic.

## Quality gates in the release process

Before a new feature is released into the release process, it is recommended to perform a final, automated quality check that scans the code for critical security vulnerabilities and blocks the release if any are found. This does not mean that you should omit security checks during continuous quality assurance or code reviews. On the contrary! Security checks must be an integral part of the other testing procedures so that you can respond to this sensitive issue at an early stage. Rather, the quality gate in the release process serves as the final control mechanism to detect and prevent the unintentional or intentional introduction of security vulnerabilities before they are imported into downstream systems. This check serves as assurance that no vulnerability detectable by static code analysis tools can slip through.

All other issues, such as violations of maintainability, robustness, and efficiency criteria, should be adequately addressed in advance through the developer’s continuous quality checks and the code review process. If you neglect these upstream checks, the result will either be dissatisfied business users whom you must put off with a new release date due to serious quality defects detected too late, or a system that becomes increasingly complex, difficult to understand, and maintenance-intensive over time. You should avoid both scenarios at all costs and conduct quality checks early and continuously.

**Quality Gate Support Processes**

- Define a procedure for systematically flagging false-positive reports and exceptions during quality control. Static code analysis tools typically provide mechanisms that allow you to suppress the identified findings accordingly. Avoid bottlenecks and implement this procedure before the final quality control.
- When introducing quality control processes, use the so-called baseline procedure to suppress quality reports that arose before the quality control process was implemented. This is particularly useful in legacy systems with a large codebase of older developments, where you want to distinguish reports from the legacy code from newly added quality defects. Be sure not to include security-critical checks in the baseline. These must be considered and analyzed separately and, if necessary, excluded via a false-positive report or resolved through a separate remediation initiative.
- Adopt a zero-tolerance strategy for security-critical issues in customer and partner code. SAP ERP systems are a popular target for cybercrime due to their central roles in corporate IT. An unrecognized or intentionally installed security vulnerability can lead to operational interruptions and [significant financial damage](https://onapsis.com/de/blog/sap-security-breach-cited-in-companys-bankruptcy/). If your stakeholders nevertheless pressure you to grant an exception, seek support from your company’s information security officer and clarify whether a risk acceptance process has been defined for such a requirement. Further information on this topic can be found in chapter [Secure ABAP development]({{ site.baseurl }}/security/).
- Perform a security review of all source code artifacts before integrating them into your system. Request that SAP add-on providers provide you with deletion transports before you import their products into your system. Import and scan third-party transports for the first time only in a sandbox system if they do not provide you with a deletion transport.<br>
Please contact your purchasing department or the contract management department in your company if the provider is uncooperative and does not provide you with corrections to the findings or detailed false positive descriptions.<br>
Do not take any legal risks and refrain from publishing the identified vulnerabilities. Under German law (see [$202c Strafgesetzbuch](https://www.gesetze-im-internet.de/stgb/__202c.html)), the use or publication of exploits may be considered a preparatory act for a criminal offense. In hardship cases, it makes sense to speak to an IT lawyer or contact a recognized body such as the [Federal Office for Information Security - BSI](https://www.bsi.bund.de/DE/Service-Navi/Kontakt/Kontaktformular/kontaktformular_node.html) or a bug bounty platform.

**Manipulation of Quality Gates**

- Ensure that a tamper-proof review and approval process is implemented: The level of freedom a developer has within the development system can pose a significant challenge in time-sensitive situations (such as development and quality assurance spread across multiple time zones or decentralized release management, etc.). Especially in companies that lack upstream continuous self-monitoring by the developer, lack pair programming or code review processes, or have releases that are too large and spread out over long periods of time, this can lead to developers, with a fixed delivery date looming, resorting to knee-jerk reactions and using their existing debug and replace permissions to bypass quality gates and associated quality checks. Manipulation of the testing and release process can only be detected through continuous monitoring of debug and replace activities in the system log (SM21) and can only be partially prevented by restricting permissions for the release of transport requests and transport tasks. Resourceful developers almost always find a way to bypass existing quality gates.
- Address the root cause of the problem, not just the symptom: Upon discovering quality gate manipulation, it is advisable to first speak with the developer and identify the cause that led to the need for manipulation. Often, the “necessity” driving the developer’s actions stems from a lack of knowledge about the development process or a lack of flexibility within it. It is helpful to invest in lightweight and easy-to-understand onboarding materials for developers and other stakeholders involved in the process. Additionally, an awareness initiative within the product teams regarding the necessity of early and continuous quality assurance measures can be beneficial.
- Take consistent action in cases of recurrence and non-compliance with processes: To do this, you must have coordinated the process in advance with management and decision-makers and obtained authorization to act. Of course, the psychological safety of developers is a high priority, which is why, as a general rule, a confidential discussion with the developer must be sought in the event of a first or second violation. By the third occurrence at the latest, it can be assumed that there has been fraudulent misrepresentation or intentional harm to the company. Especially in the case of security vulnerabilities that have been deliberately introduced, a cybersecurity incident can be assumed, which should result in legal consequences. Such intentional security incidents should be consistently punished upon the first occurrence, unless there is a valid justification.  

## Holistic Approach and Continuous Quality Control

Continuous quality control is a strategic approach designed to ensure the long-term protection of your investments in custom software development. The goal is to identify potential vulnerabilities and critical development patterns at an early stage in order to systematically optimize system security, performance, maintainability, and portability.

Modern custom code analytics tools are a key instrument in this context. These offer more extensive analysis capabilities than traditional static code analysis tools. While static code analysis focuses primarily on checking syntax, style guidelines, and known programming errors, custom code analytics tools take a more comprehensive approach: They analyze customer-specific developments within the overall context of the system—taking into account usage frequency, performance impacts, upgrade compatibility, and dependencies on standard modules and other in-house developments.

Another key benefit lies in these tools’ ability to perform hotspot analyses. This process identifies code sections that are modified disproportionately often, exhibit high complexity, or have proven to be maintenance-intensive. This enables targeted prioritization of refactoring efforts and contributes substantially to improving long-term code quality and system stability.

In addition to technical optimization, the use of Custom Code Analytics also unlocks economic potential: By identifying and eliminating duplicate or unused code, as well as detecting outdated or critical standard module usages, maintenance efforts can be reduced, upgrade projects simplified, and unnecessary licensing or development costs avoided.

For SAP Business Suite customers with SAP Enterprise Support, SAP Solution Manager starting with version 7.2 SP5 includes a suite of tools that, under the term Custom Code Lifecycle Management, offer a comprehensive portfolio of analysis and management tools. A well-known example of these tools is the Custom Code Decommissioning Cockpit, which is frequently used in the preparation of migration projects from SAP ECC to SAP S/4HANA to cost-effectively decommission unused customer code prior to migration. You can find a detailed description of the functionality with presentation material and videos in the linked Expert Content [Custom Code Management with SAP Solution Manager](https://help.sap.com/docs/SUPPORT_CONTENT/sm/3627184393.html?locale=en-US).

Unfortunately, as of today (as of May 2025), no adequate successor product for Custom Code Lifecycle Management in SAP Solution Manager has been officially announced that even comes close to covering its scope and capabilities. Instead, there are scattered, specialized siloed solutions and services that, unfortunately, only provide point-in-time analyses but do not ensure holistic and evolutionary monitoring (SAP for Me Custom Code Analytics Application, S/4HANA Readiness Check, Clean Core Cockpit, Intelligent Custom Code Management Service). Especially given the technology-agnostic ecosystem in the SAP environment, it makes sense to exchange ideas with colleagues from other technology areas and, if necessary, to use a software analysis tool with ABAP evaluation capabilities that is already available in your company as an alternative.

In addition to the tools offered by SAP, there are a number of commercial and freely available tools that differ significantly from one another in terms of functionality, scope of features, support, and further development. As potential examples—and without making any specific recommendations for these tools—we would like to briefly introduce the attached candidates:

[**ABAP2CodeCharta**](https://github.com/BenjaminWeisheit/ABAP-2-CODE-CHARTA)

ABAP2CodeCharta is an open-source tool that converts ABAP source code into CodeCharta format. It visualizes ABAP code structures as code cities: three-dimensional representations of characteristics such as complexity, size, and change frequency. The tool supports hotspot detection, improves understanding of large codebases, and helps prioritize refactoring work.

[**Teamscale**](https://teamscale.com/)

Teamscale is a commercial custom-code analytics tool for continuously analyzing and evaluating software quality. It supports many programming languages, including ABAP, and combines static code analysis with usage, change, and architecture metrics. Teamscale identifies technical debt, unused or redundant code, hotspots, and violations of quality policies. Its dashboards, trend analyses, and DevOps integrations support sustainable quality control, particularly in complex enterprise environments.

{: .note }
> - [Intelligent Custom Code Management](https://community.sap.com/t5/enterprise-resource-planning-blogs-by-sap/intelligent-custom-code-management/ba-p/13472631)
> - [Managing Custom Code - SAP Cloud ALM or SAP Solution Manager?](https://community.sap.com/t5/enterprise-resource-planning-blog-posts-by-sap/managing-custom-code-sap-cloud-alm-or-sap-solution-manager/ba-p/13524454)
