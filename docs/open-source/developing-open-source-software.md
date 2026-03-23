---
layout: page
title: Open source software development
permalink: /open-source/developing-open-source-software/
parent: Open Source
nav_order: 4
---

# Open source software development
{: .no_toc}

This section describes the use case as a company developing its own components as an open source project. This corresponds to the third [maturity level]({{ site.baseurl }}/open-source/#maturity-levels) and therefore the most demanding.

1. TOC
{:toc}

## Added value from a company perspective

In this use case, you decide to publish and further develop a ABAP-based component of your software as an open source project. This means that you open and make this component available to other users outside of your company. You choose a [open source license]({{ site.baseurl }}/open-source/licenses) and thereby expressly allow the use, modification and distribution of the component's source code within the scope of the specific license conditions.

This may not initially sound like a desirable model. Specifically, however, you do not use your proprietary implementation of your company's business model, but rather you select suitable components. The following are particularly suitable:

- Reusable components ("Reuse Services") that solve recurring technical problems (e.g. logging, maintenance dialogs, unit testability, ...)
- SDKs zur Anbindung Ihrer Kunden, beispielsweise zur Einbindung Ihrer bereitgestellten Webservices
- Proof of concepts and technical demos

Developing as an open source project gives you the following advantages:

- **Involvement by external developers**  
  External developers can test your component on other systems with different release levels or installed dependencies. You can suggest features or add them with your support in the component itself. Your open source component gains in quality and functionality without necessarily incurring development costs in your company.  
  This scenario is described from the perspective of the participating developer in [Participation in Open Source Software]({{ site.baseurl }}/open-source/contributing-to-open-source-software.md).
- **Developer perspectives outside the box**  
  Through external participation you gain new perspectives. This can occur because external parties use a different release level, a different runtime environment or a different SAP product to deploy your component or because they have different technical experiences and know different architectures or design patterns. You get to know these perspectives and can evaluate them and, if necessary, incorporate them into other projects, including internal ones.
- **Development as an independent component**  
  In order to be able to publish the component as an open source project, you inevitably have to deal with some technical questions about the software architecture that usually do not arise, especially in in-house development. Addressing this topic can increase your software quality. Some of these questions are described in section [Architecture](#architecture).
- **External appearance**  
  By publishing your component as open source software, you as a company show that you are confident in your development skills and processes and can develop high-quality software. This can serve as a figurehead and present itself positively in recruiting.

## Adaptation of the development process to take external developers into account

Once you have decided on a component that you would like to "open source", there are a few points to consider in order to make access as easy as possible for external participation.

### Documentation

Provide documentation on how external parties can participate in your project. This includes a README file with installation instructions and details about dependencies and supported products and releases. This also includes, for example, issue templates as a template for bug reports and contribution guidelines with the naming conventions and architectural patterns used. This is not ABAP specific, for tips see [Open Source Guides](https://opensource.guide/starting-a-project/#launching-your-own-open-source-project).

### Namespaces

The namespace concept in ABAP means that participation is only possible in the customer namespace without additional steps. However, the customer namespace increases the likelihood of name conflicts across different projects. There are two different approaches to solving the problem:

#### Collision checking on dotabap.org

If your project is listed on [dotabap.org](https://dotabap.org), the objects it contains are automatically checked for name collisions with all other projects listed there. In addition to the namespace, the identifiers of your development objects should contain a project abbreviation, often a three-character acronym, which is not yet used.

#### Own Reserved Namespace

You can use a self-reserved namespace (`/NSPC/`). However, in this case, you must provide the external developers with a development or repair key to participate. abapGit offers built-in support for this and automatically serializes/deserializes the repair license in the community version ([documentation](https://docs.abapgit.org/user-guide/reference/namespaces.html)). The SAP version of abapGit in the public Cloud systems does not provide the functionality. The intended way to install namespaces via the Maintain Namespaces app is also unsuitable because you cannot share the namespace with just any person or company ([documentation](https://help.sap.com/docs/sap-btp-abap-environment/landscape-portal/maintain-namespaces?locale=en-US)). A solution for this is the ABAP open source namespaces.

#### ABAP Open Source Namespaces

A ABAP open source namespace is a reserved namespace whose repair license is publicly viewable. They are automatically available in the Maintain Namespaces app and thus solve the problem of installation in public Cloud systems. The level of difficulty compared to using the customer namespace is still increased because the permissions to access the app are usually very limited in companies. In particular, such a namespace can be requested without access to the Maintain Namespaces app in SAP for Me or a business relationship with SAP. Details can be found at [ABAP Open Source Namespaces](https://github.com/SAP/abap-open-source-namespaces).

### Architecture

Your component should be usable by external developers outside of your development system. This means it must not have any dependencies on objects that are not available in the supported SAP product and release. This also includes your own utility libraries, which would either have to be published as an open source project and therefore as an installable dependency, or whose use in the component must be removed. Even within the SAP standard, you should be concerned about limitations. If you are developing a helper library that solves technical problems, you should avoid unnecessarily using objects from the SAP standard that are located, for example, in the `SAP_APPL` or `S4CORE` software components. This restricts participation to a group of people who have access to a SAP ERP / SAP S/4HANA system and excludes the use of the [ABAP Cloud Developer Trials](https://community.sap.com/t5/technology-blog-posts-by-sap/abap-cloud-developer-trial-2023-available-now/ba-p/14057183). This is particularly popular in the open source community because it can be operated locally, is free and does not require an active business relationship with the SAP.

### Support various releases

Regardless of the product support (ABAP Cloud Developer Trial, SAP ERP, SAP S/4HANA, industry solution) and the software components generally available with it, you should also think about the release support, the release status and patch level of these software components that you want to support minimally. It is unlikely that external developers will use the exact release level of your development system. The more you support, the easier it is to participate, but the more difficult it is to develop because you have to do without new features and APIs.

For example, [abapGit](https://github.com/abapGit/abapGit) and [abap2UI5](https://github.com/abap2UI5/abap2UI5) both still support the ABAP release 7.02. Technically, you use two different approaches for this:

abapGit is limited to the syntax and available APIs from ABAP 7.02. Continuous integration with [abaplint](https://github.com/abaplint/abaplint), which can check for release-specific syntax, ensures that no one accidentally uses newer syntax. If a API is technically required and is not available in the supported release, the call is implemented dynamically.

abap2UI5 uses a different approach. The syntax used is checked for compatibility with ABAP 7.50 using abaplint. The syntax is also automatically downloaded using abaplint via a [CI-Pipeline](https://github.com/abap2UI5/abap2UI5/blob/main/.github/workflows/ABAP_702.yaml) and committed to a separate branch. Details about this approach can also be found in this [article](https://www.linkedin.com/pulse/running-abap2ui5-older-r3-releases-downport-compatibility-abaplint-mjkle/) from the maintainer.

### Support various ABAP language versions

Another complexity is the support of multiple ABAP language versions. For example, it may be that you are limited to ABAP release 7.50 and a SAP-API is already available there and also included in the ABAP Cloud developer trial. However, it is not approved for use in ABAP Cloud. In this case, you would normally create a wrapper in the Clean Core Level Concept. Of course, this is no longer available in Level A and therefore cannot be delivered in public Cloud systems. Maybe there is a newer API released in ABAP Cloud. However, this is not available in ABAP 7.50. If you would like to support this scenario, you have various options:

- __Branching__  
  You can use a separate branch in git per release or ABAP language version distinction. This offers the advantage that you can use specific APIs and features normally and statically tested. Installation is also comparatively easy for the user of your component, as they simply select the specific branch. However, maintaining this setup is very time-consuming as you have to continuously port all new features and bug fixes to different branches.
- __Standard ABAP as a dependency in a separate repository__  
  You can implement the primary coding of your application with language version ABAP for Cloud development and offload any specific release/product or language version dependent calls into separate repositories, which then have to be installed as a dependency in the respective system.
- __Dynamische API-Verwendung__  
  You can both dynamically call the APIs, which can only be used in standard ABAP and only in ABAP Cloud, and use the ABAP-Cloud-API as a fallback. In this case you largely lose syntax checking. However, you gain an easier installation and a simpler repository setup. Examples of such calls can be found at [steampunkification](https://github.com/heliconialabs/steampunkification).

abapGit also offers further options for handling the ABAP language version. You can find these under [abapGit Docs - ABAP Language Version](https://docs.abapgit.org/user-guide/reference/abap-language-version.html).

### Continuous integration without SAP system

The next difficulty is tooling support for static and dynamic source code analysis for quality assurance. The ABAP Test Cockpit (ATC) would normally be used here. However, this is not available integrated in open source development because there is no original system for development. The single source of truth is the Git repository. You can of course use ATC in your development system, but the external developers do not benefit from this and you do not see any direct feedback in pull requests. Connecting your development system to the Git provider such as GitHub is technically unproblematic, but is not covered by the license. The solution is to use source code analysis tools outside of the SAP system.

[abaplint](https://abaplint.org/) can be integrated natively into continuous integration environments such as GitHub Actions and offers a comparable range of functions to standard ATC tests or Code Pal for ABAP for static source code analysis. In addition, it is possible to run unit tests outside the system using the built-in transpiler, thereby fully supporting the development process. Syntax checking across multiple repositories is also possible.
