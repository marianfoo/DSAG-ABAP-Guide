---
layout: page
title: Solution approach
permalink: /clean-core/solution-approach/
parent: Clean Core
nav_order: 5
---

{: .no_toc}
# Approach

1. TOC
{:toc}

## Define your solution path
Each company must decide internally how it will use the new technologies. And a rational decision is based on economic aspects - added value for the departments, customer satisfaction, direct (license costs, operating costs) and indirect costs (employee hiring, training, and expiry of old know-how). 

A holistic analysis also requires consideration of alternatives to SAP products. For example, Cloud, a developer cannot only create native applications on the SAP BTP. The other Cloud providers must be considered for a holistic assessment. In the same way, the tools for API management must also be defined and decided. The organizational aspects of “fusion teams” should be included in the evaluation; So-called citizen developers can sometimes take on IT tasks, such as front-end design. In addition to SAP and non-SAP products, there are also open source projects that solve various use cases, especially in reporting.

Implementing the Clean Core concept requires a strategic approach and careful planning. Organizations can adopt the following approach to effectively utilize the Clean Core concept of SAP. 
 
1. **API-First Approach**: Focus a API-first approach to development by releasing core functionality as reusable APIs that can be consumed by internal and external applications. This promotes agility, scalability and innovation while ensuring security and governance. Keyword: SOA - Service Oriented Architecture, or microservices.
    * New interfaces are only created with the standard APIs and SAP.
    * Or customer's own REST APIs are created internally.
2. **Modularization and Standardization**: Decompose monolithic systems into modular components and standardize data structures and interfaces where possible. This enables greater flexibility, reusability and interoperability across the organization.
    * Decide where to store the customer-specific data. If you need additional data for your business processes, it is best integrated into a standard data product, avoid parallel data models to standard tables.
    * Harmonize your business processes and launch projects to integrate Z-Transactions into standard Fiori apps. To do this, you should find or extend the functionalities of Z transactions in standard Fiori apps.
    * Entscheiden Sie welche Kundenerweiterung bestehen bleiben. 
3. **Assessment and Rationalization**: Conduct a thorough assessment of existing SAP landscapes to identify areas of complexity and redundancy. Streamline systems and processes to align with Clean Core principles and prioritize simplification measures.
    * Conduct fit-gap workshops and initiate cleanup projects of underperforming, unsafe, or unused code. 
    * Train your architects to consciously use new technologies based on guidelines.

## Decision aids

Here you will find a few references and possible decision-making aids: 
* A methodology for enterprise architects [SAP Application Extension Methodology - SAP AEM](https://help.sap.com/docs/architecture_guidance/2f804cb5e53d4279879009100a2b2082/cd963582f46d421c9abfd28dc25ea7e3.html)
* SAP's complete guide on how customers can do Clean Core extensions [Extend SAP S/4HANA in the cloud and on premise with ABAP based extensions](https://www.sap.com/documents/2022/10/52e0cd9b-497e-0010-bca6-c68f7e60039b.html)
* Also look at examples with the [Extensibility Scenarios Explorer](https://extensibilityexplorer.cfapps.eu10.hana.ondemand.com/ExtensibilityExplorer/#/ExtensibilityGuide)
* What is the shared successor development object? [Cloudification Repository Viewer](https://sap.github.io/abap-atc-cr-cv-s4hc/)
* Further considerations can also be found in the chapter: [Integration](/integration)

## ABAP Cloud

ABAP Cloud is the new development model for all system landscapes, whether SAP BTP ABAP Environment, S/4HANA Cloud Public Edition and Private Edition or S/4HANA On-Premise, you can use the same model for the development of Clean Core and Use Cloud Ready applications. The use is described in more detail in [Extensibility Guide for S/4HANA](https://www.sap.com/documents/2022/10/52e0cd9b-497e-0010-bca6-c68f7e60039b.html). In the following sections you will get some details. ABAP Cloud is fundamental part if you want to achieve Clean Core.

![ABAP Cloud](./img/image-07.png)

ABAP Cloud - Availability
{: .img-caption}

### Released APIs

The use of released APIs (development objects with C1 release) is a central component of ABAP Cloud. SAP gives you as a customer the assurance that this API is stable and can be used for your own developments. This means that only SAP objects that SAP has explicitly released can be used in ABAP Cloud.

### Level Concept

The Clean Core Level Concept was delivered in August 2025 and replaces the previous 3-TIER model. The Level Concept is about classifying your customer's own development into four different levels (Level A-D). Level A is equivalent to ABAP Cloud and is therefore automatically Clean Core and Cloud Ready. Levels B-D were reclassified and classified using the ABAP Test Cockpit.

* Level B - Classified as Clean Core and this includes classic technologies such as IDOC or the ALV Grid. There is a list of technologies that are described and detailed in note [3578329](https://me.sap.com/notes/3578329). In addition to the note, the Cloudification Repository is used to classify the objects mapped as "[Classic API](https://sap.github.io/abap-atc-cr-cv-s4hc/?version=objectClassifications_3TierModel.json&states=classicAPI)".
* Level C - This level is described as "SAP Intern" and is "Conditional Clean Core". The APIs and objects are not explicitly released or prohibited, but SAP keeps the option open to change or delete the objects.
* Level D - All objects marked here as "[No API](https://sap.github.io/abap-atc-cr-cv-s4hc/?version=objectClassifications_3TierModel.json&states=noAPI)" fall under the category no Clean Core. You should no longer use objects that have been classified via the Cloudification Repository in your development.

![Level Concept](./img/image-10.png)

Clean Core Level Concept
{: .img-caption}

{: .recommendation }
Even if classic technologies have now been defined as Clean Core, you should rely on software components and ABAP Cloud when developing new ones. With such new implementations, you should also think about whether you want to carry them out on-stack or side-by-side. 

If the APIs is not currently released, you can create so-called wrappers that encapsulate the SAP functionality and release it for your development in Level A. As part of this, you should create an influence request at SAP to receive approval or an alternative API. Further information on creating wrappers and which objects are suitable can be found in the SAP Guide: [ABAP Cloud API Enablement](https://www.sap.com/documents/2023/05/b0bd8ae6-747e-0010-bca6-c68f7e60039b.html).

{: .note }
> [Clean Core Extensibility (White Paper)](https://www.sap.com/documents/2024/09/20aece06-d87e-0010-bca6-c68f7e60039b.html)
>
> [Extensibility Guide (Current version)](https://www.sap.com/documents/2022/10/52e0cd9b-497e-0010-bca6-c68f7e60039b.html)

### Migration of reports

Reports/programs are now a central component for executing logic in a SAP system, whether in dialog or in the background via batch job. However, when migrating, you should note that reports are no longer part of ABAP Cloud. 

Currently there are the following successors:
* Fiori App - Creation of an application based on SAP Fiori with the ABAP RESTful Programming Model, RAP for short. For more information about RAP, see the Development chapter. The app is the entry point for the user.
* Application Job - This new type of job is developed based on a class that is started by a central routine in the system. The start takes place via a Fiori application. Jobs are particularly suitable for automated background activities.

### New concepts

With the introduction of ABAP Cloud, various development concepts were revised and successors made available. You should therefore note that some of the old concepts are no longer valid. Some examples:

| Area              | Old (Level B-D)    | New (Level A)                       |
|-------------------|--------------------|-------------------------------------|
| Application Log   | SLG0, SLG1         | CL_BALI_OBJECT_HANDLER, ABAP API    |
| Job               | SM36, SM37, Report | Application Job                     |
| E-Mail            | CL_BCS             | CL_BCS_MAIL_MESSAGE                 |
| E-Mail            | SOST               | Monitor Email Transmissions (F5442) |
| Programmiermodell | BOPF               | RAP                                 |
| Tabellenpflege    | SM30               | Business Configuration              |
| translation       | SE63               | Maintain Translations (F4950)       |

The full list can be found [here](https://software-heroes.com/abap-cloud-api).
