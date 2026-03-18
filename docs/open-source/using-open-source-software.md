---
layout: page
title: Use of open source software
permalink: /open-source/using-open-source-software/
parent: Open Source
nav_order: 2
---

{: .no_toc}

# Use of open source software

This section describes the use case as integrating open source software into your own development process or specially developed software. He addresses the first [Ausbaustufe]({{ site.baseurl }}/open-source/#ausbaustufen).

1. TOC
{:toc}

## abapGit for obtaining open source software

The pivotal point in the context of open source in the ABAP development is abapGit. Without the Git client for ABAP, collaboration on a software product across system boundaries is not possible. In our use case, the use of open source components, obtaining these is very easy with the help of abapGit. The installation instructions can be found at [Installation](https://docs.abapgit.org/user-guide/getting-started/install.html). The standalone version is usually sufficient.

With abapGit you install a tool in your system that allows versioning of objects in a package hierarchy with [git](https://git-scm.com/). To do this, it either connects directly to a Git host using online repositories, such as github.com, or exchanges ZIP files, in the case of offline repositories. The latter are particularly helpful when network connectivity between the SAP system and the Internet is not desired.

{: .note }
**Bulk processing with abapGit**  
In both cases, the tool allows you to import large amounts of development objects into your system or to export development objects from your system. This may be an unwanted effect for some people, whereas otherwise all development activities in the ABAP platform can be comprehensively protected and restricted via permissions.  
However, you should say goodbye to this idea. Although you can also restrict the use of abapGit based on permissions, even [Exits](https://docs.abapgit.org/user-guide/reference/authorizations.html) can be implemented to further refine the permission logic. However, as long as developers have the opportunity to develop in the system what their actual activity is, they can implement their own data export program or assign themselves the necessary authorizations with just a few lines of coding, bypassing all authorization checks. Too extensive regulation of tooling inevitably leads to the construction of workarounds and hinders the development process.  
It is therefore recommended to define a process for how the available tooling can be used sensibly and in a coordinated manner within the team.

## Wer stellt ABAP-Open-Source-Software bereit?

A comprehensive list of open source ABAP projects published on GitHub can be found on [dotabap.org](https://dotabap.org). You can submit your own projects that meet the requirements for listing to [dotabap-list](https://github.com/dotabap/dotabap-list) via a pull request.

![Screenshot dotabap.org]({{ site.baseurl }}/open-source//img/dot-abap-dot-org.png)

Screenshot dotabap.org
{: .img-caption}

## Wer nutzt ABAP-Open-Source-Software?

On page [Who Uses abapGit?](https://docs.abapgit.org/user-guide/other/where-used.html) of the abapGit documentation you will find a list of companies that use abapGit and have actively decided to be listed. From this it can be deduced that they use at least abapGit itself as open source software. SAP also uses open source ABAP. abapGit is in a customized version in SAP S/4HANA Cloud Public Edition and the SAP BTP ABAP Environment [vorinstalliert](https://help.sap.com/docs/btp/sap-business-technology-platform/working-with-abapgit?locale=en-US). Projects such as [Code Pal for ABAP](https://github.com/SAP/code-pal-for-abap-cloud), [Project Kernseife](https://github.com/SAP/project-kernseife) and [RAP Generator](https://github.com/SAP-samples/cloud-abap-rap) are available on GitHub and are provided with the Apache 2.0 open source license.

## Integration of open source tools in the development process

You can take a first step towards dealing with open source software in ABAP development by considering the use of open source tools in your development process. This can result in a reduction in effort without having to develop an extensive open source strategy.

- **Chancen**
  - Reduction of expenses through the use of generators
  - Increasing code quality through the use of additional code analysis tools
- **Risiken**
  - Installation of third-party software in the development system / developer PCs / continuous integration environments

Many of the opportunities of this use case have already been mentioned with examples under [Motivation and opportunities]({{ site.baseurl }}/open-source/#motivation-und-chancen). In summary, the use of open source tools in the development process relieves the burden on developers, as work steps are automated or the quality specifications are automatically checked / violations of the specifications can be corrected early and in some cases automatically.

In order to take advantage of the opportunities, the selected open source software must be installed. Depending on the software, this happens on developer PCs, in continuous integration environments or in the SAP system. As can be seen at [Lizenzen]({{ site.baseurl }}/open-source/licenses.md), open source licenses exclude liability and warranty unless a separate agreement is made. There are consequently security-relevant implications for the installation and use of the software. This topic is discussed in more detail in [Assessment and life cycle of an external dependency](#bewertung-und-lebenszyklus-einer-externen-abhängigkeit).

## Use of open source libraries in your own software

An optional extension of this expansion level is the use of open source libraries in your own software. In this case, you integrate the selected libraries using API calls and deliver them. There is even greater added value here, as functions can be provided in your applications that would otherwise not have been possible to develop or maintain with relative effort. However, the question inevitably arises as to how such open source components are handled in productive environments and in the delivery of software. This significantly increases the importance of [Assessment and life cycle of an external dependency](#bewertung-und-lebenszyklus-einer-externen-abhängigkeit).

- **Chancen**
  - Reduction of effort through integration of finished components
  - Increasing the functionality of your applications
- **Risiken**
  - Installation and delivery of third-party software

## Assessment and lifecycle of an external dependency

Using externally developed open source dependencies (hereinafter also referred to as "components") profitably requires a thorough assessment in advance,
in order to weigh up the opportunities and risks mentioned in the previous sections.

There are already published criteria, particularly with regard to risks, which can be used to make such an assessment
can be, e.g. [Bauer et al., "A structured approach to assess third-party library usage"](https://doi.org/10.1109/ICSM.2012.6405311). Criteria include:

- **Adequacy** captures how well the selected component helps solve the problem at hand.
- **Documentation** summarizes the availability, completeness and quality of the documentation.
- **License compatibility** records whether the license of a component is suitable for the application scenario and whether the license is compatible with the licenses of other components used.
- **Degree of distribution** summarizes the market penetration of a component.
- **Tool support** records whether the component is specifically supported by tools such as development environments or whether their use even hinders them. This criterion is not equally applicable to all components.
- **Manufacturer support** describes the extent to which maintenance and further development of a component by the manufacturer (the publishing company or the open source community) is guaranteed in the long term.
- **internal quality and security** records the extent to which a component takes into account internal quality criteria such as maintainability, understandability and whether mechanisms exist to check security and react to security deficiencies.

<!--
  author    = {Veronika Bauer and Lars Heinemann and Florian Deissenboeck},
  booktitle = {28th {IEEE} International Conference on Software Maintenance {ICSM}},
  title     = {A structured approach to assess third-party library usage},
  year      = {2012},
  pages     = {483--492},
  publisher = {IEEE Computer Society},
  biburl    = {https://dblp.org/rec/conf/icsm/BauerHD12.bib},
  url       = {https://doi.org/10.1109/ICSM.2012.6405311},
-->

In order to adequately evaluate these criteria, an in-depth review (due diligence) is required.
Some “red flags” for corporate use are easy to identify and can be understood as initial exclusion criteria:
Has it been a long time since the last commit? Are there open issues that have not been responded to for a long time? Is there no license information available or does the license contradict your own company's specifications?
In these cases you should refrain from using the component.

The decision *for* use requires a number of further considerations and is always the result of a weighing up:
How much of your own development effort do you save by using the open source component, and what risk do you expose yourself to?

### Best Practices: Bewertungskriterien

**Appropriateness:** In order to identify the component that best meets a requirement, research should first be carried out, which ideally provides several candidates. In addition to the pure functionality, the effort required to implement the functionality should also be estimated compared to licensing a commercial component. Especially for common functionality, it is often recommended to use a third-party component instead of your own implementation. Nevertheless, the expected effort of in-house development should be taken into account in the decision, as should the expected risk. In particular, if third-party code in a production system potentially has access to business-critical data, this must be part of the assessment.

Appropriateness describes the extent to which the planned intended use corresponds to the scenario intended for the component. If only a few details are missing from an identified open source component to meet your own requirements, it is also possible to provide these as your own contribution to the open source component (see [Beteiligung an Open Source](../contributing-to-open-source/)). In this case, it is recommended that you return the customization or addition to the original project to ensure that it remains compatible with future updates.

An important aspect of appropriateness is the extent to which the component should become part of your own application, i.e. be executed in the production system, or be used exclusively for development, i.e. for generating code from API descriptions. This also plays an important role when considering the license (see "License compatibility").

**Internal quality and security:** Since open source components are published as code, this should be examined in detail before deciding to use it. The use of code analysis tools is particularly recommended for larger components. In some cases, the component repositories may already contain result reports from tools such as *abaplint*. In any case, automatic checks should be carried out against your own security specifications, provided that tools are already in use for this purpose. The presence of automated tests is also a good indicator of the reliability and maintainability of an open source component.

In addition, the understandability of the code should be considered. On the one hand, this concerns the clarity of the interfaces (APIs) of the component used in order to integrate them as easily as possible, and on the other hand also internal features such as the commenting of classes and methods or the descriptive naming of classes or variables. Understandable code makes it easier to find errors and, if necessary, make future extensions or adjustments. See also the section on [Code Reviews](../../application-lifecycle-management/ensuring-quality/). This is an important aspect, especially if the component is to be expanded in perspective (see above).

**Documentation:** A success factor for using open source is the documentation available, especially the interfaces provided by the component (API). Particular attention should be paid to the scope, comprehensibility and topicality. On the one hand, documentation helps with the correct use of the component and often avoids the time-consuming look into the source code. On the other hand, it also signals that the component is intended for use by the public and can therefore also be an indication that the component itself is well maintained (see also "Manufacturer Support").

Even in the event that improvements, adjustments or additions are to be restored, it is advisable to pay attention in advance to documentation on how to contribute changes. Open source projects often contain a “contribution guide”, for example in the form of a file `Contributing.md`.

**License compatibility:** The license of an open source component is of essential importance, especially in a corporate context. It is important to check that the component is released under a license that is compatible with the intended use and that complies with your company's policies. Some licenses might require, for example, that if a component is used and delivered as part of a larger application, the entire application must be made available under the same license, i.e. the entire source code must be disclosed. However, if a component is used exclusively as development tooling and is not delivered to a production system, such a clause may not apply at all. In this case, it is always advisable to coordinate with your own legal department.

You should also make sure that the license allows you to modify the component. This could be crucial to fix bugs or add features if community support wanes. When using multiple open source components, it is also important to ensure that their licenses are compatible with each other and do not contradict each other. It should also be noted that open source does not automatically mean free. A component could, for example, only allow private use free of charge, while a license fee is charged for commercial use. There are often different licenses depending on the application (private, commercial).

**Degree of distribution:** When evaluating an open source component, its degree of distribution plays an important role. The main argument for using popular and widely used components is the lower dependency on the respective provider.

To evaluate the distribution, various criteria can be used, such as the number of "stars" or forks on GitHub, or the number of results in an Internet search. When conducting internet research, the type of search results should of course also be taken into account. An active discussion or blog posts about the successful use of the component can send positive signals, while desperate requests for help or frequent complaints can send negative signals. Particularly in the context of the ABAP development, SAP's attitude towards the respective project is also an important indication: Does SAP mention the project itself or even use it in its own products? It can then be assumed that using it in your own project probably involves little risk.

**Tool support:** An important feature when selecting open source components is the ability to integrate with the existing development infrastructure. Since this is quite uniform in the ABAP world, this criterion plays a minor role. A plus point would be if ATC checks were included directly for common sources of error in relation to the use of the component. Another example of tool support is portability to your own namespace as described under [Delivery in our own products](#auslieferung-von-open-source-abhängigkeiten-in-eigenen-produkten). The approach outlined there via *abaplint* in a pipeline basically works, but does not support all types of code objects.

**Manufacturer support:** When using an open source component, you essentially become dependent on the provider. It is therefore advisable to check in advance to what extent the component is being actively developed further by the provider. This is the only way to assume that, in the event of errors or security deficiencies, they will be remedied promptly. Indicators for this can be the number of contributors, the frequency of code changes (“commits”) and the release frequency. In addition to the pure activity, the handling of releases and versions must also be taken into account. Are there major and minor versions? Are changes to a release clearly documented and any incompatible changes explicitly pointed out?

The terms “manufacturer” or “provider” expressly *do not* mean that it has to be a company. Many successful open source components are maintained by a community of volunteers and can still be used in a corporate context with a clear conscience, as long as a certain continuity is guaranteed and the company's own guidelines do not require anything to the contrary. Community projects of this type often do not offer commercial support contracts, which can make them difficult to use in some companies. However, if the component comes from a well-known company such as the SAP itself, this often makes the internal approval process easier. On the other hand, open source projects from the community are often particularly quick at fixing errors.

### Best practices: approach and process

**Regular resubmission:** When using open source components, it is generally recommended to carry out a regular check of all of the above criteria in order to be able to react to changes on the part of the open source projects or in your own application. An adjustment to one's own functional scope can lead to a different assessment of the appropriateness of a component, or a change in the project structure, its activity or license can lead to a new risk assessment. Ideally, such a review also includes research for newer open source projects that may be even better suited to your own use case.

**Skills:** Working with the open source community requires a certain level of teamwork skills, such as reporting bugs or change requests to the relevant projects, or submitting pull requests to make your own customizations and give back to the community. If your team lacks experience at this point, you should plan training so that you can work with the open source projects as effectively as possible.

**Updates:** Procedure and responsibilities for updating external dependencies should be defined. Whenever a component becomes available in a new version, this change must be evaluated in terms of relevance to your own application. If positive, the change must be integrated and tested until it can finally be adopted into the production environment. A well-rehearsed procedure is particularly relevant when a security problem in an open source component becomes known in order to be able to react quickly.

## Delivery of open source dependencies in your own products

A problem when using open source components in your own software arises when delivering them to external systems. If you develop a product/add-on that is installed in customer systems, then the delivery of the dependent open source components must be particularly considered.

Most open source ABAP projects use the customer namespace (`Z`/`Y`). Customers to whom your software is delivered also use the customer namespace. If your add-on uses a reserved namespace (`/NSPC/`) to prevent name collisions, this guarantee does not apply to the dependent open source components. In addition, customers may express concerns if software providers “invade” their customer namespace. It may even be that the open source component is already installed in the customer system and is being actively used there, but in a version that is not suitable for you.

{: .solution }
A possible solution is to copy the open source component into your namespace and thus deliver and update it in isolation. With [abaplint](https://github.com/abaplint/abaplint) it is possible to set up a CI pipeline that sets up and automatically updates a mirror repository of the open source component in your reserved namespace. You can then deliver this repository. abapGit uses this technique to ship the [ajson-Projekt](https://github.com/sbcgua/ajson) together with abapGit. You can read details in the following blog post: [Automagic standalone renaming of ABAP objects](https://community.sap.com/t5/application-development-and-automation-blog-posts/automagic-standalone-renaming-of-abap-objects/ba-p/13499851).
