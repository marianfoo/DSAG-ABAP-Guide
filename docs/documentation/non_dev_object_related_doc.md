---
layout: page
title: Documentation across development objects
permalink: /documentation/non_dev_object_related_doc/
parent: Documentation
nav_order: 3
---

{: .no_toc}
# Cross-Object Documentation

1. TOC
{:toc}

In addition to describing the many development objects that perform specific functions within the ABAP system, there is also a need to illustrate the broader context within a module and across modules. This includes, for example, answers to questions such as:

* What dependencies exist between the modules?
* Which applications are used in which business processes?
* Which background jobs run at what times of the day/month/year, and which development objects are affected by them?

In our opinion, there is no suitable storage medium within the SAP development environment that effectively integrates graphics to answer these questions. We therefore recommend using other media to document these cross-functional relationships. Examples of this are:

* SAP Solution Manager / SAP Cloud ALM
* SAP LeanIX for Enterprise Architecture Management
* SAP Signavio for business process management
* Interne (product) wikis
* Documents in maintained public directories (portal storage, SharePoint, file share, etc.)

Experience shows that the main challenge in this area lies primarily in maintaining discipline. No tool can solve this challenge; only the development team and its management can.

To document the system and software architecture, including design decisions, it is advisable to use a template, such as the arc42 template. This can prevent essential aspects from being omitted from the documentation and—when a template is used across multiple projects—speeds up the search for specific information. Additionally, establishing templates facilitates the creation of documentation in parallel with development and ensures adherence to an appropriate level of abstraction.

Document templates such as the arc42 template do not always need to be completely “filled out”; rather, relevant sections should be identified based on the nature and scope of the development project, and the rest deleted.

Additionally, outdated documentation can be misleading. Therefore, all documents should include a status and versioning information to enable an assessment of their currency.

{: .recommendation }
> It should be clarified within the company how software should be documented.
> A uniform platform should be used, either a structured storage, ticket system or a process document with continued documentation (versioned)
> The structure of the documents should always be the same, even from externally purchased software, which enables the support organization to be able to help there too

Within an SAP system landscape, SAP Solution Manager, for example, provides tools for project documentation.

The following links provide further information on this topic.

{: .note }
> 1. The arc42 template for architectural documentation, [Arc42-Template](https://arc42.org/download) (accessed on: September 19, 2024)
> 2. Stefan Zörner: Documenting and communicating software architectures. Carl Hanser Verlag GmbH Co KG, 2021. ISBN: 978-3446469280
> 3. [Master Guide SAP Solution Manager - Solution Documentation](https://help.sap.com/docs/SAP_Solution_Manager/c3c5ec585ee248228ddb6c3f08073ea9/2cb3e75e134249a2bd091a40fe2f6d61.html?locale=en-US) (accessed on: 26.01.2025)
> 4. [ABAP Development Tools: User Guide - Documentation of Development Objects](https://help.sap.com/docs/ABAP_PLATFORM_NEW/c238d694b825421f940829321ffa326a/52546a60ba3f436d8f5b54b83044d0b7.html?locale=en-US&q=documentation) (accessed on: 26.01.2025)

## Version Control Documentation

### Transport Request

It is often helpful to document the following for the transport request:

* Ticket number and title
* Key development objects in the transport
* Dependencies on other transports (if any)
* Brief description of changes in the transport

You can enter documentation for each task and each request during request processing in the “Documentation” tab of the Transport Request Editor. You can continue to add to the documentation until the request is released. Note that once the request has been released, you can no longer edit it.

This documentation on the “Documentation” tab can be created for every transport request that goes to the production system. Avoid redundant documentation and do not document transports of copies. Ultimately, only the transports that are intended to go to the production system or have already gone there are relevant.

{: .note }
> * [SAP Help: Change and Transport System - Request Editor - Writing Documentation](https://help.sap.com/docs/ABAP_PLATFORM_NEW/4a368c163b08418890a406d413933ba7/d636153aab4a0c0ee10000000a114084.html?locale=en-US) (accessed on: 26.01.2025)

### Git Client

Using a Git client such as abapGit or gCTS automatically logs code changes with every commit. In addition, metadata is saved with each commit, including a brief description (known as a commit message), the author, and the date. The resulting commit history makes it possible to see past commits and track code changes. If a ticket system, such as Jira or Azure DevOps, is used to track requirements, each development requirement has a unique ID. Many teams have a policy or internal agreement to include this ID in the commit messages so that commits can be assigned to tasks. If this is done consistently, a free-text search in the commit messages can identify all commits belonging to a specific task. This significantly simplifies the process of locating and reviewing the implementation in the event of bugs. At the same time, it allows similar tasks to be implemented quickly because developers can find and follow the example that already works.

{: .important }
> Improve the traceability and transparency of changes to development objects by documenting the changes in the transport request or Git client—ideally with a reference to the triggering event in the ticket system.
