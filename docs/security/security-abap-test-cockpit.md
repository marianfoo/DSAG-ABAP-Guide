---
layout: page
title: ABAP Test Cockpit
permalink: /security/abap-test-cockpit/
parent: Security
nav_order: 7
---

{: .no_toc}

# ABAP Test Cockpit

1. TOC
{:toc}


## Overview

The ABAP Test Cockpit (ATC) is a tool for performing static and dynamic quality checks on ABAP source code and associated repository objects.

The SAP recommendation is a central ATC system, this system should be kept quite “narrow”, i.e. only a ABAP Netweaver system with a corresponding database and the software component SAP_BASIS. SAP speaks of “All you have to do is install and configure a central ATC testing system: the pure SAP basic system (SAP_BASIS >=7.51) within your SAP system landscape”. It follows that you actually only need an AS ABAP system with the software component SAP_BASIS

But: The central ATC system should be the latest software system in the entire system landscape. This has the advantage that the latest checks are available there and the remote checks are carried out more easily. If you have problems keeping your ATC test system up to date, you should look at the SAP BTP ABAP Environment as an option.

SAP delivers all checks via the SAP_BASIS component, so it is recommended to use the latest version so that you can work/check with the most current checks. Another advantage with the “narrow” system is that the ATC system can be updated quite “easily” (support package update) if necessary. In principle, you should update the ATC system (the “application” and the database) 1-2 times a year.

The checks/tests are once integrated into the “Code Inspector”, which is a function within the SAP development environment and the SAP ADT (ABAP Development Tools – Eclipse extension). The checks are triggered using the “Check => ABAP Test Cockpit” function. It is also possible to run all RFC-enabled checks (mostly all checks are RFC-enabled) as a periodic job in the background and check the entire code and create a “directory” of the findings.

The tests are rounded off with integration into the SAP CTS “correction and transport system” for system changes/developments. Here you can set the system so that every transport release is checked against the ATC checks. If findings are found, it can be set so that they prevent release for transport. This ensures that only flawless code is transported into the SAP systems. This function can also be expanded with a “liberation workflow”.

## Zentrales ATC

![Schema Central ATC](./img/image7.png)

Schema Central ATC
{: .img-caption}

The central ATC system can be seen on the left. As standard, this consists of the components ATC (ABAP Test Cockpit) and the ACI (ABAP Code Inspector). The CVA (SAP Custom Code Vulnerability Analyzer) can be activated and used with a separate license. The CVA checks its own created code against SAP recommendations for “safe programming”. Details about the CVA and the tests will be explained in more detail later.

Note: The ATC system can be expanded with the open source component abapGIT (not to be confused with gCTS of the SAP) (see the recommendations in the chapter “Open Source”). Individual components are explained below

## abapGIT

[abapGIT](https://abapgit.org/) is an open source GIT client for ABAP. This is developed in ABAP and requires at least a SAP BASE version 702 or higher.

abapGit is a tool for importing and exporting code between ABAP systems. If a developer has a developer key for the system, they can already perform these actions. abapGit allows the developer to perform bulk exports/modifications/imports, but no more than is already possible manually.

With abapGIT it is possible to deploy objects across system boundaries quite easily using your own GIT ABAP. In the past, this option was a great help and made work easier for the ABAP developers, especially in a double maintenance phase. In addition, abapGIT is required as a basis for the [abapOpenChecks](https://docs.google.com/document/d/1--6biTn5OvRM4r8CO_19FLBKCQ3_bf1cIttiBDJJeRg/edit#heading=h.2xcytpi). Therefore this function should be implemented again.

abapGIT is “simply” made available as a single ABAP report via the GIT repository. This ABAP report is then implemented into the ATC system and also into the connected development systems.

The installation is described here: [Installation - abapGit Docs](https://docs.abapgit.org/user-guide/getting-started/install.html) There are also detailed installation instructions in the SAP base including documentation on how to install an update/new version.

![abapGit GUI Client](./img/image8.png)

abapGit GUI Client
{: .img-caption}


## Checks - ABAP Checks

SAP already delivers a large number of checks with the ATC, which are used directly by the Code Inspector and the ATC.

SAP delivers the following subareas:

![SCI test variant](./img/image9.png)

SCI test variant
{: .img-caption}

The ABAP checks should be coordinated between ABAP development and the security team (which checks make sense), then those deemed “useful” should be activated for background checks and also for online checking as part of the transport releases

### S/4 Readiness-Checks

Special checks that SAP delivers are the so-called “S/4HANA Readiness” checks. These are tests with which the customer's own code can be checked for S/4HANA suitability.

The following tests are delivered in detail:

![S/4HANA Readiness test variant](./img/image10.png)

S/4HANA Readiness test variant
{: .img-caption}

Typically, as part of a Custom Code Livecycle project, the entire customer code is checked in the background for S/4HANA suitability and the findings are then converted or converted to S/4HANA using appropriate tools, often automated.

Example:

![S/4HANA Readiness Ergebnis](./img/image11.png)

S/4HANA Readiness Ergebnis
{: .img-caption}

The S/4HANA readiness checks should be activated for background checks and also for online checking as part of transport clearances while appropriate code is still being developed on ECC. With a system conversion to S/4HANA you can then switch off the checks.

### abapOpenChecks

[abapOpenChecks](https://docs.abapopenchecks.org/) are checks from the SAP Community for the ATC and the Code Inspector. The installation is done via abapGIT ([see previous chapters](https://docs.google.com/document/d/1--6biTn5OvRM4r8CO_19FLBKCQ3_bf1cIttiBDJJeRg/edit#heading=h.1ci93xb)). In the current version, abapOpenChecks delivers over 100 additional checks for the ATC and expands the checks delivered by SAP. A current list of exams can be viewed here: [abapOpenChecks - Checks](https://docs.abapopenchecks.org/checks/). The abapOpenChecks should be activated for background checks and also for online checks as part of transport releases.

### Code Pal for ABAP

This tool provides a range of checks to help with [Clean ABAP-Styleguides](https://github.com/SAP/styleguides/blob/main/clean-abap/CleanABAP.md) compliance. Although not all recommendations in the guide can be verified by static code analysis, and strict adherence to the guide may not be recommended in certain situations, this provides robust automated support for at least a subset of recommendations. SAP delivers the code PAL checks via GitHub, the installation is also carried out via abapGIT. The installation is described here: [SAP/code-pal-for-abap](https://github.com/SAP/code-pal-for-abap/blob/master/pages/how-to-install.md). The current list can be found here: [SAP/code-pal-for-abap](https://github.com/SAP/code-pal-for-abap/blob/master/docs/check_documentation.md)

The Code Pal checks should be coordinated with the developers (which checks make sense), then those deemed “useful” should be activated for background checks and also for online checking as part of the transport releases.

A useful addition to the Code Pal Checks is the ABAP Cleaner, an extension to Eclipse. Here you can check whether Clean ABAP adheres to the concept when creating the code (when entering the code).

### Code Pal for ABAP Cloud

A version of [Code Pal for ABAP Cloud](https://github.com/SAP/code-pal-for-abap-cloud/) (BTP) environments has been available since mid-September 2023. Basically (according to the documentation) "code pal for cloud checks" seems to work the same as the "normal" "code pal". SAP delivers new checks via the GitHub, which can be imported with "abapgit". The checks are stored in their own name area /CC4A/CODE_PAL. Details are described by SAP in the following blog: "[Clean code checks for ABAP – Cloud Edition](https://blogs.sap.com/2023/09/11/clean-code-checks-for-abap-cloud-edition/)". The checks are also available in the Eclipse development platform, so that Clean code can be checked during the development process if you develop Cloud with ABAP.

## Exams - Security

### Standard security checks

SAP delivers the following security checks as part of the standard delivery of Check:

![CVA exams](./img/image14.png)

CVA exams
{: .img-caption}

The SAP standard security checks should be activated for background checks and also for online verification as part of transport clearances. You may also be able to work with the developers to define critical instructions that you can/should check for

### CVA - Code Vulnerability Analyzer

The [CVA is a product of SAP](https://me.sap.com/notes/1855773) which you have to license additionally. As part of the framework contract extension (July 2022), this product was purchased at a very reasonable price. The product significantly expands the SAP security checks, the CVA checks are the same checks with which the SAP checks its own code (the code that is supplied with the SAP ABAP systems). These checks are expanded with every Netweaver ABAP update.

The CVA performs static analysis of the ABAP source code and reports possible security risks. You can find an excerpt of the tests in note [1921820](https://me.sap.com/notes/1921820). For security reasons, SAP has stored the CVA check in 2 test variants, so that you can “only” check CVA completely, i.e. individual checks cannot be switched off.

![Complete exams](./img/image17.png)

Complete exams
{: .img-caption}

BSP are checks for Business Server Pages, these are separate for technical reasons. The CVA checks should be activated for background checks and also for online checking as part of transport clearances.

### CVA - Code Vulnerability Analyzer (Cloud)

In addition to the paid version for on-premise systems, you can also get the Cloud version via the ABAP Environment. All you have to do is provision and connect the system and you can use the tests directly. In this scenario, there are no additional costs for licensing the CVA exams.
