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

## Value from a Company’s Perspective

In this use case, you decide to publish and further develop an ABAP-based component of your software as an open-source project. This means that you make this component available to users outside your company. You choose an [open-source license]({{ site.baseurl }}/open-source/licenses) and thereby explicitly permit the use, modification, and redistribution of the component's source code within the scope of the applicable license terms.

At first glance, this may not seem like a particularly desirable model. In practice, however, you would not open-source the proprietary implementation of your company's business model. Instead, you would select suitable components. The following types of components are particularly well suited:

- Reusable components ("reuse services") that solve recurring technical problems (e.g., logging, maintenance dialogs, unit testability, etc.)
- SDKs for connecting your customers, for example to integrate web services that you provide
- Proofs of concept and technical demos

Developing a component as an open-source project offers the following advantages:

- **Participation by External Developers**
    External developers can test your component in other systems with different release levels or installed dependencies. They can propose features or, with your support, implement them directly in the component. As a result, your open-source component gains quality and functionality without necessarily creating development effort within your own company.

    This scenario is described from the perspective of the contributing developer in the section [Participation in Open-Source Software]({{ site.baseurl }}/open-source/contributing-to-open-source-software.md).
- **Developer Perspectives Beyond Your Own Environment**
    Through external participation, you gain new perspectives. These may arise because external users operate on a different release level, use a different runtime environment, or use a different SAP product when working with your component. They may also have different technical experiences and be familiar with alternative architectures or design patterns. You become familiar with these perspectives and can evaluate them and, where appropriate, apply them to other projects, including internal ones.
- **Development as a Standalone Component**
    In order to publish a component as an open-source project, you inevitably have to address a number of technical software architecture questions that typically do not arise in internal development. Addressing these topics can improve the quality of your software. Some of these considerations are discussed in the section [Architecture](#architecture).
- **External Visibility**
    By publishing your component as open-source software, you demonstrate as a company that you have confidence in your development capabilities and processes and that you are able to create high-quality software. This can serve as a showcase for your company and may also have a positive impact on recruiting.

## Adapting the Development Process to Accommodate External Contributors

Once you have selected a component that you would like to open source, there are several aspects to consider in order to make participation by external contributors as straightforward as possible.

### Documentation

Provide documentation describing how external contributors can participate in your project. This includes a README file containing installation instructions and details about dependencies, supported products, and supported releases. It also includes, for example, issue templates for bug reports and contribution guidelines describing naming conventions and architectural patterns used within the project. This is not specific to ABAP. Useful recommendations can be found, for example, in the [Open Source Guides](https://opensource.guide/starting-a-project/#launching-your-own-open-source-project).

### Namespaces

The namespace concept in ABAP means that participation without additional steps is only possible within the customer namespace. However, the customer namespace increases the likelihood of naming conflicts across different projects. There are two different approaches to addressing this issue:

#### Collision Check on dotABAP.org

If your project is listed on [dotabap.org](https://dotabap.org) the included objects are automatically checked for naming collisions against all other projects listed there. In addition to the namespace, the names of your development objects should include a project abbreviation, often a three-letter acronym, that is not already in use.

#### Your Own Reserved Namespace

You can use a self-reserved namespace (`/NSPC/`). However, in this case, you must provide the external developers with a development or repair key to participate. abapGit offers built-in support for this and automatically serializes/deserializes the repair license in the community version ([documentation](https://docs.abapgit.org/user-guide/reference/namespaces.html)). The SAP version of abapGit in the public Cloud systems does not provide the functionality. The intended way to install namespaces via the Maintain Namespaces app is also unsuitable because you cannot share the namespace with just any person or company ([documentation](https://help.sap.com/docs/sap-btp-abap-environment/landscape-portal/maintain-namespaces?locale=en-US)). A solution for this is the ABAP open source namespaces.

#### ABAP Open-Source Namespaces

An ABAP Open-Source Namespace is a reserved namespace whose repair license is publicly available. Such namespaces are automatically available in the Maintain Namespaces app and therefore solve the installation issue in public cloud systems. However, the level of complexity remains higher than when using the customer namespace, as authorizations for accessing the app are typically highly restricted within companies. Such a namespace can also be requested without access to the Maintain Namespaces app in SAP for Me or without business relationship with SAP. Further details can be found under [ABAP Open-Source Namespaces](https://github.com/SAP/abap-open-source-namespaces).

### Architecture

Your component should be usable by external developers outside your development system. It must therefore avoid dependencies on objects that are unavailable in the supported SAP product and release. This includes your own utility libraries: they must either be published as installable open-source dependencies or removed from the component. Consider restrictions even within the SAP standard. For example, a technical helper library should avoid unnecessary dependencies on objects in software components such as `SAP_APPL` or `S4CORE`. Such dependencies restrict participation to people with access to an SAP ERP or SAP S/4HANA system and prevent use of the [ABAP Cloud Developer Trials](https://community.sap.com/t5/technology-blog-posts-by-sap/abap-cloud-developer-trial-2023-available-now/ba-p/14057183), which are popular in the open-source community because they can run locally, are free, and do not require an active business relationship with SAP.

### Support for Different Releases

Regardless of product support (ABAP Cloud Developer Trial, SAP ERP, SAP S/4HANA, industry solutions) and the software components generally available in those products, you should also consider release support—that is, the release level and patch level of the software components that you intend to support as a minimum. It is unlikely that external developers will be using exactly the same release level as your development system. The more releases you support, the easier participation becomes. However, development also becomes more challenging because you may have to forgo newer features and APIs.

For example, [abapGit](https://github.com/abapGit/abapGit) and [abap2UI5](https://github.com/abap2UI5/abap2UI5) both still support the ABAP release 7.02. Technically, you use two different approaches for this:

abapGit is limited to the syntax and APIs available in ABAP 7.02. Continuous integration with [abaplint](https://github.com/abaplint/abaplint), which checks release-specific syntax, ensures that contributors do not accidentally use newer syntax. If an API is technically required but unavailable in the supported release, the call is implemented dynamically.

abap2UI5 uses a different approach. The syntax used is checked for compatibility with ABAP 7.50 using abaplint. The syntax is also automatically downloaded using abaplint via a [CI-Pipeline](https://github.com/abap2UI5/abap2UI5/blob/main/.github/workflows/ABAP_702.yaml) and committed to a separate branch. Details about this approach can also be found in this [article](https://www.linkedin.com/pulse/running-abap2ui5-older-r3-releases-downport-compatibility-abaplint-mjkle/) from the maintainer.

### Support for Different ABAP Language Versions

Another source of complexity is supporting multiple ABAP language versions. For example, you may restrict yourself to ABAP-Release 7.50, and a particular SAP-API may already be available there and also be included in the ABAP Cloud Developer Trial. However, it may not be released for use in ABAP Cloud. In this case, according to the Clean Core Level Concept, you would normally create a wrapper. However, this wrapper would no longer be at Level A and therefore could not be delivered to public cloud systems. At the same time, a newer API may exist in ABAP Cloud that is released for use there, but this API may not be available in ABAP 7.50. If you want to support this scenario, several options are available:

- __Branching__
  You can use a separate Git branch for each distinction based on release or ABAP language version. This has the advantage that specific APIs and features can be used normally and be checked statically. Installation is also simple for users of
    your component, since they only need to select the appropriate branch. However,
    maintaining such a setup is effort-intensive because all new features and bug fixes must continuously be ported across multiple branches.
- __Standard ABAP as a Dependency in a Separate Repository__
    You can implement the primary coding of your application using the ABAP for
    Cloud Development language version and move all release-, product-, or lan-
    guage-version-specific calls into separate repositories. These repositories can
    then be installed as dependencies in the respective systems.
- __Dynamic API Usage__  
  You can dynamically call APIs that are available only in Standard ABAP or only in ABAP Cloud and use the ABAP Cloud API as a fallback. This largely sacrifices static syntax checking but simplifies installation and repository setup. Examples of this approach are available in [steampunkification](https://github.com/heliconialabs/steampunkification).

abapGit also offers further options for handling the ABAP language version. You can find these under [abapGit Docs - ABAP Language Version](https://docs.abapgit.org/user-guide/reference/abap-language-version.html).

### Continuous Integration Without an SAP System

The next challenge is tooling for static and dynamic source-code analysis as part of quality assurance. Under normal circumstances, the ABAP Test Cockpit (ATC) would be used for this purpose. In open-source development, however, ATC is not available as an integrated solution because there is no designated original development system; the Git repository is the single source of truth. You can use ATC in your own development system, but external contributors do not benefit from it and receive no direct feedback in pull requests. Although connecting a development system to a Git provider such as GitHub is technically straightforward, this setup is generally not covered by SAP licensing. The solution is to use source-code analysis tools outside the SAP system.

[abaplint](https://abaplint.org/) can be integrated natively into continuous integration environments such as GitHub Actions and provides functionality for static source code analysis comparable to standard ATC checks or Code Pal for ABAP. In addition, its built-in transpiler makes it possible to execute unit tests outside the SAP system, thereby providing comprehensive support for the development process. Syntax validation across multiple repositories is also supported.
