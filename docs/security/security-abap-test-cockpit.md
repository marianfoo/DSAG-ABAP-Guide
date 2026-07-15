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

SAP recommends a central ATC system; this system should be kept fairly “lean,” meaning only an ABAP NetWeaver system with the corresponding database and the SAP_BASIS software component. SAP states: “You only need to install and configure a central ATC test system: the pure SAP Basis system (SAP_BASIS >=7.51) within your SAP system landscape.” It follows that: You only need an AS-ABAP system with the SAP_BASIS software component

However: The central ATC system should be the most up-to-date system in the entire system landscape in terms of software, which has the advantage that the latest checks are available there and remote checks run more smoothly. Therefore, if you are having trouble keeping your ATC test system up to date, you should consider the SAP BTP ABAP Environment as an option.

SAP delivers all checks via the SAP_BASIS component; therefore, it is recommended to use the latest version so that you are working with and testing using the most current checks. Another advantage of the “lightweight” system is that the ATC system can be updated quite “easily” as needed (Support Package Update). In general, you should update the ATC system once or twice a year (the “application” and the database).

Once the checks are integrated into the “Code Inspector”—a feature within the SAP development environment and SAP ADT (ABAP Development Tools—Eclipse extension)—they can be triggered via the “Check => ABAP Test Cockpit” function. It is also possible to run all RFC-capable checks (almost all checks are RFC-capable) as a periodic background job to verify the entire code and generate a “list” of findings.

The checks are complemented by integration into the SAP CTS “Correction and Transport System” for system changes and developments. Here, you can configure the system so that it checks against the ATC checks every time a transport is released. If issues are detected, you can configure the system to prevent the transport from being released. This ensures that only flawless code is transported into the SAP systems. This function can also be extended with an “exemption workflow”.

## Central ATC

![Schema Central ATC]({{ site.baseurl }}/security/img/image7.png)

Schema Central ATC
{: .img-caption}

On the left is the central ATC system. In its standard configuration, it consists of the ATC (ABAP Test Cockpit) and the ACI (ABAP Code Inspector) components. With a separate license, the CVA (SAP Custom Code Vulnerability Analyzer) can be activated and used. The CVA checks the code you have written against SAP recommendations for “secure programming.” Details about the CVA and the checks will be explained in more detail later.

 Note:

 The ATC system can be extended using the open-source component abapGIT (not to be confused with SAP’s gCTS) (see the recommendations in the “Open Source” chapter). The individual components are explained below.

## abapGit

[abapGit](https://abapgit.org/) is an open-source Git client developed in ABAP. It requires SAP_BASIS release 7.02 or higher.

abapGit is a tool for importing and exporting code between ABAP systems. If a developer has a developer key for the system, they can already perform these actions. abapGit enables the developer to perform bulk exports, changes, and imports, but no more than what is already possible manually.

abapGit makes it relatively easy to transport objects across system boundaries using Git. This is particularly helpful during dual-maintenance phases. abapGit is also a prerequisite for [abapOpenChecks](https://docs.google.com/document/d/1--6biTn5OvRM4r8CO_19FLBKCQ3_bf1cIttiBDJJeRg/edit#heading=h.2xcytpi), so it should be installed in the relevant systems.

abapGIT is made available “simply” as a single ABAP report via the Git repository. This ABAP report is then implemented in the ATC system and also in the connected development systems.

The process is described in the [abapGit installation documentation](https://docs.abapgit.org/user-guide/getting-started/install.html), which also explains how to install updates and new versions in an ABAP system.

![abapGit GUI Client]({{ site.baseurl }}/security/img/image8.png)

abapGit GUI Client
{: .img-caption}


## Checks - ABAP Checks

SAP already provides a large number of checks through the ATC, which are used directly by the Code Inspector and the ATC.

SAP delivers the following subareas:

![SCI test variant]({{ site.baseurl }}/security/img/image9.png)

SCI test variant
{: .img-caption}

The ABAP checks should be coordinated between the ABAP development team and the security team (which checks are appropriate?); then, those deemed “appropriate” should be enabled for background checks as well as for online checks as part of the transport release process.

### S/4 Readiness-Checks

The “S/4HANA Readiness” checks are special checks provided by SAP. These checks are used to verify that the customer’s own code is compatible with S/4HANA.

The following tests are delivered in detail:

![S/4HANA Readiness test variant]({{ site.baseurl }}/security/img/image10.png)

S/4HANA Readiness test variant
{: .img-caption}

Typically, as part of a Custom Code Lifecycle project, all of the customer’s code is checked in the background for S/4HANA compatibility; the results are then migrated or converted to S/4HANA using appropriate tools, often in an automated process.

Example:

![S/4HANA Readiness results]({{ site.baseurl }}/security/img/image11.png)

S/4HANA Readiness results
{: .img-caption}

The S/4HANA readiness checks should be enabled for background checks and also for the online check as part of transport approvals as long as you are still developing code for ECC. Once the system has been converted to S/4HANA, you can then disable the checks.

### abapOpenChecks

[abapOpenChecks](https://docs.abapopenchecks.org/) provides SAP Community checks for ATC and Code Inspector and is installed using abapGit. It adds more than 100 checks to those delivered by SAP; the current set is listed in the [abapOpenChecks documentation](https://docs.abapopenchecks.org/checks/). Enable these checks for background runs and online checks during transport release.

### Code Pal for ABAP

This tool provides checks that support compliance with the [Clean ABAP Style Guide](https://github.com/SAP/styleguides/blob/main/clean-abap/CleanABAP.md). Static analysis cannot verify every recommendation, and strict adherence may not be appropriate in every situation, but the tool provides robust automated support for a useful subset. SAP publishes Code Pal for ABAP on GitHub, and it is installed using abapGit. See the [installation instructions](https://github.com/SAP/code-pal-for-abap/blob/master/pages/how-to-install.md) and [current check documentation](https://github.com/SAP/code-pal-for-abap/blob/master/docs/check_documentation.md).

The Code Pal checks should be reviewed with the development team to determine which checks are meaningful and relevant. The selected checks should then be activated for both background checks and online checks during transport release procedures.

A useful complement to Code Pal Checks is ABAP Cleaner, an Eclipse extension. It enables developers to verify compliance with Clean ABAP principles during code creation, i.e., while entering code.

### Code Pal for ABAP Cloud

A version of [Code Pal for ABAP Cloud](https://github.com/SAP/code-pal-for-abap-cloud/) (BTP) environments has been available since mid-September 2023. Basically (according to the documentation) "code pal for cloud checks" seems to work the same as the "normal" "code pal". SAP delivers new checks via the GitHub, which can be imported with "abapgit". The checks are stored in their own name area /CC4A/CODE_PAL. Details are described by SAP in the following blog: "[Clean code checks for ABAP – Cloud Edition](https://blogs.sap.com/2023/09/11/clean-code-checks-for-abap-cloud-edition/)". The checks are also available in the Eclipse development platform, so that Clean code can be checked during the development process if you develop Cloud with ABAP.

## Checks – Security

### Standard security checks

As part of the standard delivery, SAP provides the following security checks:

![CVA exams]({{ site.baseurl }}/security/img/image14.png)

CVA exams
{: .img-caption}

The SAP standard security checks should be activated for both background checks and online checks during transport release procedures. In coordination with the development team, it may also be beneficial to define additional critical statements or commands that should be checked.

### CVA - Code Vulnerability Analyzer

The [Code Vulnerability Analyzer (CVA) is an SAP product](https://me.sap.com/notes/1855773) that requires an additional license. It significantly expands the available security checks and uses the same checks that SAP applies to the ABAP code delivered in its systems. The checks are extended with each SAP NetWeaver AS ABAP update.

The CVA performs static analysis of the ABAP source code and reports possible security risks. You can find an excerpt of the tests in note [1921820](https://me.sap.com/notes/1921820). For security reasons, SAP has stored the CVA check in 2 test variants, so that you can “only” check CVA completely, i.e. individual checks cannot be switched off.

![Complete exams]({{ site.baseurl }}/security/img/image17.png)

Complete exams
{: .img-caption}

BSP checks are provided separately for technical reasons and apply to Business Server Pages. The CVA checks should be activated for both background checks and online checks during transport release procedures.

### CVA – Code Vulnerability Analyzer (Cloud)

In addition to the licensed on-premise version, a cloud-based variant is available through the ABAP Environment. To use it, you only need to provision and connect the system, after which the checks can be used directly. In this scenario, no additional licensing costs are incurred for the CVA checks.
