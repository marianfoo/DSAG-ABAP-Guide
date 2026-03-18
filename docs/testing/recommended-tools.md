---
layout: page
title: More testing tools
permalink: /testing/recommended-tools/
parent: Software test with ABAP Unit
nav_order: 4
---

{: .no_toc}
# Testing tool recommendations

1. TOC
{:toc}

In addition to the information about the ABAP Unit, we would like to show you other testing tools that can be used in the context of testing in SAP. These serve to support testing of the applications in the business process context. These tools are not ABAP-specific, but are generally seen as part of (SAP) software development.  
This means that ABAP development does not have to take any special precautions regarding the tools.  
However, ABAP Unit is the basis and testing support is a prerequisite to avoid and discover fundamental errors in the development phase and to ensure appropriate software quality. If ABAP Unit is in extensive use, you can concentrate on errors that arise from the integration and interaction of the applications when testing the applications with the tools mentioned here. The tests are no longer interrupted by errors in deeper software layers and the number of test cycles and thus the test effort are significantly reduced.

The selection in this guide is limited to the products preferred by SAP and some of which are already included in the license scope. There are also many other test management solutions on the market that can be used to support ABAP development.

## Testing tools in SAP Solution Manager
The [SAP Solution Manager](https://support.sap.com/en/alm/solution-manager.html) is a sophisticated and proven system for the [Application Lifecycle Management]({{ site.baseurl }}/application-lifecycle-management), which includes, among other things, various test tools.

### Test-Suite
The [SAP Solution Manager test suite](https://help.sap.com/docs/SUPPORT_CONTENT/sm/3530264795.html?mt=de-DE) essentially consists of the test plan management for preparing the tests and a tester app with which the users, i.e. the testers, carry out the prepared and released test cases. Furthermore, various functions for evaluation and analysis are available to the test manager.

Test plans are created and managed in test plan management. The heart of the matter is the selection of test cases, which are stored as such in the structure of the [Solution documentation](https://help.sap.com/docs/SAP_Solution_Manager/c3c5ec585ee248228ddb6c3f08073ea9/2cb3e75e134249a2bd091a40fe2f6d61.html?mt=de-DE) (Solution Documentation, “SolDoc” for short). These can then be divided into smaller units, the so-called test packages, and assigned to the corresponding testers or tester groups. In this way, tailor-made test plans can be created, for example for functional tests, integration tests, regression tests, unit tests or user acceptance tests.

![Presentation: Test management in the SAP Solution Manager](./img/darstellung_solman_testmanagement_neu.png)

Schematic representation: Test plan with test packages and test cases from SolDoc (source: own representation)
{: .img-caption}

Manual test cases are often described in **test documents** (using Microsoft Word, Microsoft Excel, etc.) that detail the test steps to be performed. It is also possible to store **URLs** that lead to test cases that are located at a different location. The third test case type in the standard SAP Solution Manager are so-called **test configurations**, which control automated test cases that were created, for example, using [CBTA (komponentenbasierte Testautomatisierung)](#komponentenbasierte-testautomatisierung), eCATT (extended Computer Aided Test Tool) or with [Tricentis Test Automation](#tricentis-test-automation) (see [Chapter on the test cases in the SAP Help Portal](https://help.sap.com/docs/SAP_Solution_Manager/fbc7b5ecf5094fe0b6a2eb966160008f/df49e0555937e263e10000000a44538d.html?locale=de-DE)). 
SAP introduced [Testschritte (engl. "Test Steps")](#testschritt-designer) as a further variant for manual test cases, but these are only available after installing the “Focused Build” add-on.

The testers who execute the test cases provided and released by the test manager have them listed in the “My Tasks / Tester Worklist” app with all the information relevant to them. The test cases can be processed there. In the event of an error, this can be reported as a so-called test defect, which is then forwarded to the respective support team and - after the error has been corrected - is available for testing again.

The analysis functions of the Test Suite consist of various reports that prepare the testers' activities in a variety of ways and sometimes display them graphically. The test manager has an overview of the status and progress of the tests at all times.

### Testschritt-Designer
From the Solution Manager Add-on ["Focused Build"](https://support.sap.com/en/alm/focused-build.html) (software component ST-OST), which was designed by SAP primarily for agile software development and has been made available free of charge since 2020, the [Testschritt-Designer](https://help.sap.com/docs/Focused_Build_Focused_Insights/53cb8e90c8504f31bb44d4f0029b4b98/84bc67026ded45e58c7f29296a5d3f35.html?mt=de-DE) is particularly worth highlighting in test management, which can also be used in combination with document-based test cases, so that both classic test documents and test steps can be contained in one test package at the same time. Test steps are a modern, elegant way to map manual test cases, which, in contrast to conventional test documents, require a little more preparatory work to create. On the other hand, test step designer test cases can be generated from well-documented processes with detailed process steps with just a few clicks. 

Focused Build ships another tester app called My Test Executions, which is optimized for test step designer test cases and is very easy to use. This app is limited to the functions that are absolutely necessary for the tester. It can also be used for purely document-based test cases or for test packages with mixed test cases and makes test case execution very pleasant.
The “classic” app “My Tasks / Tester Worklist” is a little more powerful, but also more difficult to use. It can also be used for both test case types, although when you call up a test step designer test case you jump to "My test executions", which can be confusing at first.

![Presentation: Possibilities of the SAP Solution Manager Test Suite and the addition from Focused Build](./img/solman_test_suite_focused_build.png)

Possibilities of the SAP Solution Manager Test Suite (below) and the supplement from Focused Build (above) [(Quelle: SAP)](https://support.sap.com/content/dam/support/en_us/library/ssp/alm/sap-solution-manager/focused-solutions/Focused_Build/sp15/FB_TestManagement_L2.pdf)
{: .img-caption}

{: .note }
> If your users use a SAP Fiori launchpad as an entry point into the SAP world, embed the “My Test Executions” tile as an iFrame that displays the number of open test packages assigned to the respective user.

### Komponentenbasierte Testautomatisierung
The [komponentenbasierte Testautomatisierung](https://help.sap.com/docs/SAP_Solution_Manager/fbc7b5ecf5094fe0b6a2eb966160008f/00e90f0489994e76ad5999a63bbf4f30.html?locale=de-DE) (Component-Based Test Automation, CBTA for short) is the on-board tool of the SAP Solution Manager for automating test cases and is included in the standard scope of delivery.

With CBTA, test cases can be automated for different technologies such as SAP GUI, SAP CRM Web Client, Web Dynpro ABAP, Business Server Pages (BSP), SAP UI5/FIORI and many more.
It is created using a test recorder that generates a test script with the steps to be carried out. The individual modular components (the "C" in CBTA) created when recording a test script can be reused and used as [zusammengesetzte Testskripte](https://help.sap.com/docs/SAP_Solution_Manager/fbc7b5ecf5094fe0b6a2eb966160008f/77f3f335ba9c4f0b8ec79924991d7748.html?locale=de-DE) for end-to-end testing.

The test scripts are packed into so-called test configurations and can be stored in the solution documentation - alongside manual test cases and URLs.

{: .note }
> With the end of maintenance of the SAP Solution Manager, the end of CBTA is also getting closer. It is therefore advisable to consider whether a future-proof third-party solution such as Tricentis Test Automation (see below) for test automation might be a better alternative now.

## Test tools in SAP Cloud ALM
As a successful product to the SAP Solution Manager, whose mainstream maintenance end date from SAP is dated at the end of 2027, [SAP Cloud ALM](https://support.sap.com/en/alm/sap-cloud-alm.html) was developed for the implementation of the [Application Lifecycle Management]({{ site.baseurl }}/application-lifecycle-management). The Cloud product - like the Solution Manager - includes, among other things, integrated test management that can be used both independently (for manual test cases) and in conjunction with a test automation solution such as [Tricentis Test Automation](#tricentis-test-automation). SAP Cloud ALM and thus also its test management functions are continuously developed by SAP.

Similar to the SAP Solution Manager, the [test management is divided into SAP Cloud ALM](https://support.sap.com/en/alm/sap-cloud-alm/implementation/sap-cloud-alm-implementation-expert-portal/testmanagement.html?anchorId=section_1012737862
) into an app for **test preparation** of manual and automated test cases, an app for managing **test plans**, one for **test execution**, an analytics app for **test execution analysis** and one for an overview of test case errors, here called **Defects**.

A function still missing (as of May 2025) in SAP Cloud ALM, which is used intensively by many users in the Solution Manager, is the grouping of test cases within a test plan into test packages, with the option of precisely assigning tester groups including reuse, as shown in section [Test-Suite](#test-suite).

SAP delivers a large number of standard processes including process flow diagrams and associated test activities, which can be easily used in SAP Cloud ALM and customized if necessary, similar to the [Testschritt-Designer](#testschritt-designer) from the Focused Build package.

A test automation tool for S/4HANA Cloud Public Edition is integrated into SAP S/4HANA Cloud and supports automated testing of standard and customer-specific business processes. There are over 300 pre-built test scripts based on SAP best practices. These scripts cover standard business processes and can be executed directly.
 
For more extensive scenarios, third-party testing tools can be integrated via the APIs of [SAP Cloud ALM Test Automation API](https://api.sap.com/api/CALM_TEST_AUTOMATION/overview) provided by SAP. This allows flexibility in managing complex test environments.

![Illustration: Testing with SAP Cloud ALM](./img/sap_test_automation_api.jpg)

Testing with SAP Cloud ALM (Source: SAP)
{: .img-caption}

## Tricentis Test Automation
Tricentis is an independent company that is not part of SAP, but is [very well integrated into the SAP world through a strategic partnership](https://support.sap.com/en/alm/partners/test-automation.html) and therefore the recommended test automation solution in the SAP context.

An interface between the SAP Solution Manager and Tricentis Tosca has existed since 2017. In 2020, the strategic partnership between SAP and Tricentis was further deepened. Since then, the automation functionality of Tricentis Tosca has been integrated into the SAP Solution Manager and now also into the SAP Cloud ALM. All SAP customers with a SAP Enterprise Support contract are entitled to use Tricentis Test Automation for SAP ("TTA for SAP") as a term license. In addition, the Tricentis platform is sold through SAP distribution under the [SAP Solution Extensions](https://www.sap.com/products/solution-extensions.html).

[TTA for SAP](https://support.sap.com/en/alm/partners/test-automation.html) is a subset of Tricentis Tosca. It uses the same automated test case concepts as Tosca itself, but is limited to SAP applications. There are also functionalities from Tosca that are not present in "TTA for SAP", such as the test case design functions or requirements and problem management.

TTA for SAP is intended for use with the SAP Solution Manager Test Suite. The Test Suite serves as a test management tool (for testing, planning, reporting and more) and TTA as an automation tool. To do this, a test configuration is created in the test suite, which serves as a shell for the automatic test. The automatic test case can be called directly from the test suite. After the test case has expired, the status is then reported back to the test suite. This applies analogously to the interaction of the Solution Manager with the independent automation tool Tricentis Tosca. This is offered by SAP as “SAP Enterprise Continuous Testing by Tricentis” (ECT).
 
There is also an integrated test automation solution for SAP Cloud ALM. "[Tricentis Test Automation for SAP with SAP-Cloud-ALM integration](https://help.sap.com/docs/cloud-alm/tricentis-test-automation-for-sap/overview?locale=de-de)" is a joint cloud-based offering from SAP and Tricentis. It combines the application lifecycle management capabilities of SAP Cloud ALM with the test automation capabilities of Tricentis. This enables automated, functional and consistent software testing for all browser-based SAP products and applications. Tricentis also provides options for test orchestration, execution monitoring and test reporting. To use this functionality, a Tricentis tenant must be set up and connected to SAP Cloud ALM. However, as with TTA, there are restrictions regarding users and storage. For full functionality, an independent Tricentis tool must be purchased, the "[SAP Test Automation by Tricentis](https://www.sap.com/germany/products/technology-platform/test-automation.html)".
 
SAP Cloud ALM offers an interface to third-party tools with the "[SAP Cloud ALM Test Automation API](https://api.sap.com/api/CALM_TEST_AUTOMATION/overview)". In addition to products from other providers, the comprehensive Tricentis test automation tool "SAP Test Automation by Tricentis" can be connected via this interface. This enables integrated testing with SAP applications and third-party applications. This product from Tricentis can also be purchased through SAP sales.

![Illustration: Integration of the SAP ALM tools with the test automation tools from Tricentis](./img/tricentis_test_automation_uebersicht.jpg)

Integration of the SAP ALM tools with the test automation tools from Tricentis (Source: SAP)

{: .img-caption}



