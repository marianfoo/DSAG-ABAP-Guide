---
layout: page
title: Documentation across development objects
permalink: /documentation/non_dev_object_related_doc/
parent: Documentation
nav_order: 3
---

{: .no_toc}
# Cross-development object documentation

1. TOC
{:toc}

In addition to describing the many development objects that take on individual, very specific functions in the ABAP system, there is also a need to show the larger connections within a module and across modules. These include, for example, answers to questions such as:

* What dependencies are there between the modules?
* Which applications are used in which business processes?
* Which background jobs run when during the day / month / year and which development objects are affected by them?

In our opinion, there is no suitable storage medium within the SAP development environment to answer these questions, which in particular integrates graphics well. We therefore recommend using other media to document these overarching connections. Examples of this are:

* SAP Solution Manager / SAP Cloud ALM
* SAP LeanIX for Enterprise Architecture Management
* SAP Signavio for business process management
* Interne (Produkt-)Wikis
* Documents in maintained public directories (portal storage, SharePoint, file share…)

Experience shows that the challenge in this area lies primarily in the question of discipline. No tool can solve this challenge, only the development team and the associated development management.

To document the system and software architecture, including design decisions, it is advisable to use a template, such as the arc42 template. This can prevent essential aspects of the documentation from being forgotten and - when using a template across multiple projects - speeds up the search for specific information. In addition, defining templates makes it easier to create documentation parallel to development and to maintain an appropriate level of abstraction.

Document templates such as the arc42 template do not always have to be completely “filled out”, but relevant parts should be identified depending on the type and scope of the development project and the rest deleted.

Additionally, outdated documentation can be misleading. Therefore, the status and versioning should be included in all documents in order to be able to assess whether they are up to date.

{: .recommendation }
> It should be clarified within the company how software should be documented.
> A uniform platform should be used, either a structured storage, ticket system or a process document with continued documentation (versioned)
> The structure of the documents should always be the same, even from externally purchased software, which enables the support organization to be able to help there too

Within a SAP system landscape, for example, the SAP Solution Manager offers options for project documentation.

The links below provide further information.

{: .note }
> 1. The arc42 template for architectural documentation, [Arc42-Template](https://arc42.org/download) (accessed on: September 19, 2024)
> 2. Stefan Zörner: Documenting and communicating software architectures. Carl Hanser Verlag GmbH Co KG, 2021. ISBN: 978-3446469280
> 3. [Master Guide SAP Solution Manager - Solution Documentation](https://help.sap.com/docs/SAP_Solution_Manager/c3c5ec585ee248228ddb6c3f08073ea9/2cb3e75e134249a2bd091a40fe2f6d61.html?locale=en-US) (accessed on: 26.01.2025)
> 4. [ABAP Development Tools: User Guide - Documentation of Development Objects](https://help.sap.com/docs/ABAP_PLATFORM_NEW/c238d694b825421f940829321ffa326a/52546a60ba3f436d8f5b54b83044d0b7.html?locale=en-US&q=documentation) (accessed on: 26.01.2025)

## Documentation for Version Management

### Transport request

It often helps to document the transport order

* Ticket number and title of the ticket
* Most important development objects in transport
* Dependencies on other transports (if any)
* Short description of changes in transport

The documentation for each task and each order can be recorded during order processing within the Transport Request Editor in the “Documentation” tab. The documentation can be continuously expanded until it is released. Please note that once the order has been released, processing is no longer possible.

This documentation on the "Documentation" tab can be created for every transport order that goes into the production system. Avoid redundant documentation and do not document the transport of copies. Ultimately, only the transports that are supposed to go into the productive system or have already gone are of interest.

{: .note }
> * [SAP Help: Change and Transport System - Request Editor - Writing Documentation](https://help.sap.com/docs/ABAP_PLATFORM_NEW/4a368c163b08418890a406d413933ba7/d636153aab4a0c0ee10000000a114084.html?locale=en-US) (accessed on: 26.01.2025)

### Git-Client

Using a Git client like abapGit or gCTS automatically logs code changes with every commit. In addition, metadata is stored with the commit, which contains a short description, the so-called commit message, the author and the date. The resulting commit history makes it possible to see past commits and track code changes. If a ticket system, such as Jira or Azure DevOps, is used to capture requirements, each development requirement has a unique ID. Many teams have the requirement or internal agreement to include this ID in the commit messages so that the commits can be assigned to the tasks. If this is done consistently, all commits that belong to a specific task can be identified using a free text search in the commit messages. This makes it much easier to find and check the implementation in the event of bugs. At the same time, similar tasks can be implemented very quickly because the developers can find and follow the already working example.

{: .important }
> Increase the traceability and transparency of changes to development objects by documenting the changes in the transport order or Git client - ideally with reference to the triggering process in the ticket system.
