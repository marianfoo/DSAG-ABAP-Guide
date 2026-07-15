---
layout: page
title: Solution approach
permalink: /clean-core/solution-approach/
parent: Clean Core
nav_order: 5
---

{: .no_toc}
# Solution approach

1. TOC
{:toc}

## Define Your Transformation Path
Every company must decide internally how to implement new technologies. And a rational decision is based on economic factors—added value for the departments, customer satisfaction, direct costs (license fees, operating costs), and indirect costs (hiring, training, and the loss of existing expertise).

A comprehensive analysis also requires considering alternatives to SAP products. For example, developers can create cloud-native applications on platforms other than SAP BTP. Other cloud providers must be taken into account for a comprehensive evaluation.

Similarly, the tools for API management must also be defined and selected. The organizational aspects of “fusion teams” should be incorporated into the evaluation; so-called citizen developers can sometimes take on IT tasks such as front-end design. In addition to SAP and non-SAP products, there are also open-source projects that address various use cases, particularly in reporting.

Implementing the Clean Core concept requires a strategic approach and careful planning. Organizations can use the following approach to effectively leverage SAP’s Clean Core concept.
 
1. **API-First approach**: Adopt an API-First approach to development by exposing core functionalities as reusable APIs that can be utilized by both internal and external applications. This promotes agility, scalability, and innovation while ensuring security and governance. Keyword: SOA – Service-Oriented Architecture or Microservices.
    * New interfaces are only created with the standard APIs and SAP.
    * Or customer's own REST APIs are created internally.
2. **Modularization and standardization**: Break down monolithic systems into modular components and standardize data structures and interfaces wherever possible. This enables greater flexibility, reusability, and interoperability across the entire organization.
    * Decide where to store the customer-specific data. If you need additional data for your business processes, it is best integrated into a standard data product, avoid parallel data models to standard tables.
    * Harmonize your business processes and launch projects to integrate Z-Transactions into standard Fiori apps. To do this, you should find or extend the functionalities of Z transactions in standard Fiori apps.
    * Decide which custom extensions should remain. 
3. **Evaluation and rationalization**: Conduct a thorough assessment of existing SAP environments to identify areas of complexity and redundancy. Streamline systems and processes to align them with the principles of Clean Core and set priorities for simplification measures.
    * Conduct fit-gap workshops and initiate cleanup projects of underperforming, unsafe, or unused code.
    * Train your architects to consciously use new technologies based on guidelines.

## Decision-Making Aids

Here are some references and resources to help you make a decision:
* A methodology for enterprise architects [SAP Application Extension Methodology - SAP AEM](https://help.sap.com/docs/architecture_guidance/2f804cb5e53d4279879009100a2b2082/cd963582f46d421c9abfd28dc25ea7e3.html)
* SAP's complete guide on how customers can do Clean Core extensions [Extend SAP S/4HANA in the cloud and on premise with ABAP based extensions](https://www.sap.com/documents/2022/10/52e0cd9b-497e-0010-bca6-c68f7e60039b.html)
* Also look at examples with the [Extensibility Scenarios Explorer](https://extensibilityexplorer.cfapps.eu10.hana.ondemand.com/ExtensibilityExplorer/#/ExtensibilityGuide)
* What is the shared successor development object? [Cloudification Repository Viewer](https://sap.github.io/abap-atc-cr-cv-s4hc/)
* Further considerations can also be found in the chapter: [Integration](/integration)

## ABAP Cloud

ABAP Cloud is the new development model for all system landscapes, whether SAP BTP ABAP Environment, S/4HANA Cloud Public Edition and Private Edition or S/4HANA On-Premise, you can use the same model for the development of Clean Core and Use Cloud Ready applications. The use is described in more detail in [Extensibility Guide for S/4HANA](https://www.sap.com/documents/2022/10/52e0cd9b-497e-0010-bca6-c68f7e60039b.html). In the following sections you will get some details. ABAP Cloud is fundamental part if you want to achieve Clean Core.

![ABAP Cloud]({{ site.baseurl }}/clean-core/img/image-07.png)

ABAP Cloud - Availability
{: .img-caption}

### Released APIs

The use of released APIs (development objects with a C1 release status) is a central component of ABAP Cloud. SAP provides customers with the assurance that these APIs are stable and can be used for your own development projects. This means that only SAP objects that SAP has explicitly released can be used in ABAP Cloud.

### Level Concept

The Clean Core Level Concept was delivered in August 2025 and replaces the previous 3-TIER model. The Level Concept is about classifying your customer's own development into four different levels (Level A-D). Level A is equivalent to ABAP Cloud and is therefore automatically Clean Core and Cloud Ready. Levels B-D were reclassified and classified using the ABAP Test Cockpit.

* Level B - Classified as Clean Core and this includes classic technologies such as IDOC or the ALV Grid. There is a list of technologies that are described and detailed in note [3578329](https://me.sap.com/notes/3578329). In addition to the note, the Cloudification Repository is used to classify the objects mapped as "[Classic API](https://sap.github.io/abap-atc-cr-cv-s4hc/?version=objectClassifications_3TierModel.json&states=classicAPI)".
* Level C - This level is described as "SAP Intern" and is "Conditional Clean Core". The APIs and objects are not explicitly released or prohibited, but SAP keeps the option open to change or delete the objects.
* Level D - All objects marked here as "[No API](https://sap.github.io/abap-atc-cr-cv-s4hc/?version=objectClassifications_3TierModel.json&states=noAPI)" fall under the category no Clean Core. You should no longer use objects that have been classified via the Cloudification Repository in your development.

![Level Concept]({{ site.baseurl }}/clean-core/img/image-10.png)

Clean Core Level Concept
{: .img-caption}

{: .recommendation }
Even if classic technologies have now been defined as Clean Core, you should rely on software components and ABAP Cloud when developing new ones. With such new implementations, you should also think about whether you want to carry them out on-stack or side-by-side.

If an API is not currently released, you can create a wrapper that encapsulates the SAP functionality and release the wrapper for Level A development. You should also submit an influence request to SAP to request approval or an alternative API. Further information about creating wrappers and determining which objects are suitable is available in the SAP guide [ABAP Cloud API Enablement](https://www.sap.com/documents/2023/05/b0bd8ae6-747e-0010-bca6-c68f7e60039b.html).

{: .note }
> [Clean Core Extensibility (White Paper)](https://www.sap.com/documents/2024/09/20aece06-d87e-0010-bca6-c68f7e60039b.html)
>
> [Extensibility Guide (Current version)](https://www.sap.com/documents/2022/10/52e0cd9b-497e-0010-bca6-c68f7e60039b.html)

### Migration of Reports

Reports and programs are now a central component for executing logic in an SAP system, whether in interactive mode or in the background via batch jobs. However, during migration, you should note that reports are no longer part of ABAP Cloud.

Currently there are the following successors:
* Fiori App - Creation of an application based on SAP Fiori with the ABAP RESTful Programming Model, RAP for short. For more information about RAP, see the Development chapter. The app is the entry point for the user.
* Application Job - This new type of job is developed based on a class that is started by a central routine in the system. The start takes place via a Fiori application. Jobs are particularly suitable for automated background activities.

### New Concepts

With the introduction of ABAP Cloud, various development concepts have been revised and replaced with new ones. You should therefore be aware that some of the old concepts are no longer valid. Here are a few examples:

| Area              | Old (Level B-D)    | New (Level A)                       |
|-------------------|--------------------|-------------------------------------|
| Application Log   | SLG0, SLG1         | CL_BALI_OBJECT_HANDLER, ABAP API    |
| Job               | SM36, SM37, Report | Application Job                     |
| E-Mail            | CL_BCS             | CL_BCS_MAIL_MESSAGE                 |
| E-Mail            | SOST               | Monitor Email Transmissions (F5442) |
| Programming model | BOPF               | RAP                                 |
| Table maintenance | SM30               | Business Configuration              |
| translation       | SE63               | Maintain Translations (F4950)       |

The full list can be found [here](https://software-heroes.com/abap-cloud-api).
