---
layout: page
title: The ABAP RESTful Application Programming Model (RAP)
permalink: /abap/restful_abap/
parent: Moderne ABAP Entwicklung
nav_order: 5
---

{: .no_toc}
# ABAP RESTful Application Programming Model (RAP)

1. TOC
{:toc}

The [ABAP RESTful Application Programming Model](https://help.sap.com/docs/ABAP_PLATFORM_NEW/fc4c71aa50014fd1b43721701471913d/289477a81eec4d4e84c0302fb6835035.html?locale=en-US), _RAP_ for short, was first introduced by the SAP in 2018 and has been usable since the S/4HANA release in 1909. Conceptually it has many parallels to [ABAP-Programming Model for SAP Fiori](https://help.sap.com/docs/ABAP_PLATFORM/cc0c305d2fab47bd808adcad3ca7ee9d/3b77569ca8ee4226bdab4fcebd6f6ea6.html?mt=de-DE) and can therefore be seen as its spiritual successor.  

Both programming models specify the necessary development objects and their interaction in order to build applications and interfaces with their own data storage in a S/4HANA system. The further development to RAP has made development much easier and does not require any SAP GUI transactions or SEGW services. In RAP, too, the entire application logic revolves around a so-called business object, which defines data storage and existing business logic and offers it to consumers. The first choice should be RAP if transactional Fiori Elements applications are to be developed (List Report & Object Page). But read-only APIs, SAPUI5 freestyle apps or non-SAP UI technologies can also be implemented with RAP by using the resulting OData services.

RAP represents the complete E2E scenario from the database layer to the published OData service. The business object (BO) is defined on the one hand by the virtual data model (VDM) and on the other hand by the (optional) available behavior. In the VDM, by creating CDS views, the fields are selected from the database and defined via relationships between the CDS views of the BO Composition Tree. This always consists of a root entity (root, for example a trip with corresponding possible instances) and any number of child entities (e.g. one or more instances of flight bookings below the trip). This composition tree can be built to any depth. Each child entity can only exist together with its direct parent and its key is part of its own.  

{: .recommendation }
> * RAP should be used productively [at the earliest from Release 2021](https://pages.community.sap.com/topics/abap/rap). If necessary, deal in detail with the limited range of functions in the 1909 and 2020 releases (such as the lack of validations, determinations, draft, ...)!  
> * As a rule, you should use the integrated draft concept for new developments and only forgo it if there are good reasons.
> * Since RAP is a relatively new technology, there are sometimes striking differences depending on the S/4HANA release. Familiarize yourself with the limitations of your system in advance!  
> * Whenever possible, new applications should be implemented with Fiori Elements. SAPUI5 freestyle apps often tempt you to allow yourself to be lured into increased complexity through additional freedom and usually lead to significant additional effort.
> * Don't forget to share your developments with RAP for extensibility to other consumers if desired.


## Managed developments with RAP
By definition, the RAP framework separates the individual development objects anyway and thus already specifies the software architecture and a clean separation. The actual application logic is strictly separated from the data storage. These strict requirements of the framework make it easier for developers to orientate and implement applications and relieve a lot of work in this regard. The picture below shows the rough interaction of the sub-elements in RAP programming.  

![RAP Big Picture, © SAP](./img/RAP.png)
  
RAP Big Picture, © SAP
{: .img-caption}

### Database level
For new developments, the managed scenario should always be used in order to use as many functions as possible (CRUD handling, draft, ...) automatically from the framework and to reduce manual development effort. Some differences in the [Unmanaged scenario](#unmanaged-szenario) can be found in the relevant section below. At the lowest level, the data model for the RAP business object is created classically via DDIC tables or, on newer systems, with CDS table entities. Each node that is later to be published as its own EntitySet via RAP receives its own data storage. Care must be taken to use UUIDs as keys and to include the UUID key of all hierarchically higher nodes.

### Virtual data model
Based on the tables, the virtual data model (VDM) is now built via CDS Views - more information about this development object can be found in chapter [Core Data Services](../core-data-services/index.md). According to the SAP recommendations, several levels or layers should be set up for this (from bottom to top):
* **DB-Tabelle**
* **I_** Basic Interface View (renaming of fields, ... may not be necessary when using CDS Table Entities)  
* **R_** Restricted Base View (Reuse Layer, Composition Tree for RAP with app specifics)
* **I_** (optional) Composite Interface View, Released API for expansion based on the R_View
* **C_** Projection View (Consumption Layer, projection with app-specific UI annotations)  

In order to signal in the CDS view that your CDS views are used for RAP, you can use the suffix _TP in the name. The SAP recommends this - but in our opinion it can be dispensed with.  

There is a maximum of one restricted layer per business object, for which the BO behavior is also defined. However, if this BO uses several, separate applications, you have the option of later creating several consumption layers and adding app-specific virtual fields in the CDS at this point or removing unnecessary fields for the respective use case from the selection. However, if virtual fields are relevant and valid for the entire RAP BO, they should be introduced deeper into the reuse layer. The same applies to the linking of input help or language-specific texts that are to be used globally in the BO.

### Behavior Definition & Pool
Building on the Root Reuse CDS View, a central behavior definition is created in the next RAP layer. This defines the available transactional behavior for the business object and contains central configurations for it. It is unique and multiple behavior definitions cannot exist for a given CDS composition tree. Each node of the tree is listed individually in the behavior definition and can be given an alias and can then be addressed under this via [EML](#entity-manipulation-language-eml).

### Behavior Projection
The previously mentioned behavior definition exists uniquely and centrally for each business object (composition tree) and determines which behavior this BO basically provides. However, the BO can now be used in several (or no) Fiori applications and here the specific requirements usually differ. For example, the app should only allow certain users to delete existing instances - but creating new instances will be less relevant for other users. The projection layer therefore makes it possible to limit the available behavior of the RAP BO for each individual app or API. However, validations and determinations are always applied automatically for the BO. Actions, for example, can be ignored in Behavior Projection by not releasing them for use. Similarly, the fields to be displayed are restricted in the CDS projection layer. The Behavior Projection refers to a Root Consumption CDS View and this is later used for the service definition.

### OData release
The actual OData service is no longer published in the RAP framework via transaction SEGW as was previously the case. Rather, the framework handles the generation and provision automatically and with just a few configurations on your part.  

First you need to create a **Service Definition** based on your Root Consumption CDS View. This lists all Consumption CDS Views to be published and allows you to assign an alias per source. Under this alias, the entity is later available in the OData service as an EntitySet. Other linked CDS views, for example as master data sources, do not have to be explicitly included; these automatically become part of the service when referenced from published CDS views.

Based on the service definition, a **service binding** is created in the next step. Here you can specify whether the OData service is intended for the use of Fiori interfaces, for analytical scenarios or simply as a web API. You also choose OData V2 or V4. After pulishing, you can directly call the Fiori preview for UI services or, alternatively, consume the OData service and test the delivered data via /IWFND/GW_CLIENT. Before S/4HANA 2025, the use of transaction /IWFND/V4_ADMIN is required for V4 activations on-premise.

## Advanced RAP functionalities

### RAP Unit Testing
Of course, the RAP framework also supports the creation of unit tests to support high application quality as a priority in the development cycle. For this purpose, local test classes are defined in the behavior pool of the business object in order, for example, to check the correct functioning of a RAP validation or to ensure that running an action leads to the desired result. These then directly call the ABAP methods of the `class_under_test` and can be run through and evaluated in the ATC. Alternatively, a separate test class can be defined that tests the RAP BO via EML; Here too, used master data can be mocked and used via CDS test doubles - the reference to the BO is established by a ABAP doc comment `"! @testing BDEF:<rap_bo_name>`. Further information and concrete examples are available in this [RAP Workshop](https://github.com/SAP-samples/abap-platform-rap-workshops/tree/main/rap4xx/rap400#readme), others among.

### Extensibility
Since the S/4 Release 2022 it has been possible to expand RAP Business Objects. If the creator of a BO (e.g. SAP, partner, customer) has approved it for expandability, there are extensive opportunities to expand the BO's delivered functionality and adapt it to business requirements. Scenarios include adding new fields using [Data Model Extensions](https://help.sap.com/docs/abap-cloud/abap-rap/develop-data-model-extensions), adding behavior using [Behavior Extensions](https://help.sap.com/docs/abap-cloud/abap-rap/develop-behavior-extensions) or completely new nodes in the BO composition tree using so-called [Node Extensions](https://help.sap.com/docs/abap-cloud/abap-rap/develop-node-extensions). In your own developments, please make sure to release all development objects for the extension if this is desired. A practical hands-on is available in the [RAP-Kurs 630](https://github.com/SAP-samples/abap-platform-rap630).

### Unmanaged scenario
If you cannot develop your application on a greenfield site, the `unmanaged` scenario offers the possibility of also publishing existing legacy coding via a RAP BO. Unfortunately, you don't have the convenient features of CRUD out-of-the-box. Instead, you have to implement both the interaction phase and the saving sequence completely yourself. The local class `cl_abap_behavior_saver` is used to program how the changes from the interaction phase are persisted via your existing legacy coding (such as BAPIs) and how changes, deletions or new creations are recorded. However, you also have the option of manually implementing `unmanaged save` or `additional save` in the `managed` scenario if required. You can find a hands-on [here](https://github.com/SAP-samples/abap-platform-rap-opensap/blob/main/week4/unit3.md).

### Entity Manipulation Language (EML)
The Entity Manipulation Language was added to the ABAP kernel specifically for the RAP framework and allows the use and interaction with RAP business objects from ABAP code. In this way, you can also call up your BOs or those released by the SAP in individual developments. There are, among other things, options for creating new instances, calling actions, editing field values ​​and the like. All nodes of the composition tree can be used using the appropriate syntax. For more information, the [EML Cheat Sheet](https://github.com/SAP-samples/abap-cheat-sheets/blob/main/08_EML_ABAP_for_RAP.md) is a further source.

### RAP Feature Showcase App
The SAP provides a central repository that can be installed as an example application in your S/4 system. This [RAP Feature Showcase App](https://github.com/SAP-samples/abap-platform-fiori-feature-showcase) shows you interactively which functionalities can generally be implemented with RAP and Fiori Elements and helps you to understand the necessary developments directly in the system. Once installed, you can run the app on your S/4 system and explore all available options. The app also provides specific information on how certain functions can be implemented.

### Migration of CDS generated BOPF
You have the option of migrating existing BOPF applications to the more modern RAP framework if they were not generated from CDS using the BOBX transaction but rather via @ObjectModel annotations. For more information on how to do this, see the official [Migration Guide Migrating from CDS generated BOPF to RAP](https://help.sap.com/docs/SAP_S4HANA_ON-PREMISE/0a54d0c8a2be4136a8b5d41a367dd537/2e48e205756c4dafb02ef0e2ff14b1bc.html?locale=en-US).  

## Feature availability overview
As mentioned above, the RAP framework made big leaps from S/4 version to S/4 version, especially immediately after release. Which features you can use depends largely on your system version. In most cases, use is not recommended before the 2021 release. The following list is intended to give you an initial orientation as to which features will be supported and when and what can be expected in the future.

**1909**
+ First release of RAP, EML in ABAP syntax
+ Only support queries (read-only) and unmanaged transactional apps with legacy coding.
+ Nur OData v2

**2020**
+ Virtual elements in the CDS view for the RAP-BO (see transient fields in the BOPF)
+ Managed Scenario, Unmanaged/Additional Save (Custom Save Handler), Unmanaged Lock
+ Draft Scenario (total eTag)
+ OData v4
+ Type & Control MappingOData Navigation across more than two BO hierarchy levels
+ Documentation via Knowledge Transfer Document for Behavior Definition, Service Binding
+ Actions/Functions allow other entities/structures as result return parameters
+ Control structure for Create provides information about which fields were not filled by the client
+ Dynamisches Operation/Feature Control
+ Introduction of the DVM (Determination Validation Machine) with trigger operations + fields

**2021**
+ Additional implementation for Draft Actions
+ Simulation mode for COMMIT ENTITIES (EML)
+ Singleton root instance for multi-line editing of several main entities (Customizing entries, etc.)
+ Additional actions, functions in behavior projection
+ InA service for CDS analytical queries

**2022**
+ Extensibility of RAP business objects
+ Business Events (Define & Raise)
+ Abstraktions-Ebene via Business Object Interface
+ Large Objects (binary files, file upload)
+ ADT Wizard: Generate ABAP Repository Objects (RAP generation based on a database table)
+ Instance Factory Actions for creating entities
+ Read access logging for RAP BOs

**2023**
+ Side effects to trigger field updates
+ Extensibility of service definitions
+ Initial release of the Background Processing Framework
+ Migration tool for existing BOPF BOs (see below)
+ Consumption of business events

**2025**
+ Exclusively CDS-based data model (CDS Table Entities as persistence, CDS Simple Types, CDS Exact Cardinalities, CDS Scalar Functions, CDS Aspects - but without draft and simple ENUMs)
+ RAP modeling of hierarchies
+ Collaborative draft (parallel collaboration on a BO instance)
+ Fiori Elements tables for displaying and modifying RAP hierarchies
  
{: .note }
> + [RAP Cloud Documentation](https://help.sap.com/docs/ABAP_PLATFORM_NEW/fc4c71aa50014fd1b43721701471913d/289477a81eec4d4e84c0302fb6835035.html?locale=en-US)
> + [EML Cheat Sheet](https://github.com/SAP-samples/abap-cheat-sheets/blob/main/08_EML_ABAP_for_RAP.md)
> + [RAP Feature Matrix of Software Heroes](https://software-heroes.com/en/abap-feature-matrix)
> + [RAP Feature Cheat Sheet](https://www.brandeis.de/blog/cheat-sheet-sap-rap-basics-de)
> + [Migrating CDS generated BOPF to RAP via Migration Guide](https://help.sap.com/docs/SAP_S4HANA_ON-PREMISE/0a54d0c8a2be4136a8b5d41a367dd537/2e48e205756c4dafb02ef0e2ff14b1bc.html?locale=en-US)  
> + [RAP Feature Showcase App](https://github.com/SAP-samples/abap-platform-fiori-feature-showcase)  
> + [SAP Samples: RAP Repositories](https://github.com/orgs/SAP-samples/repositories?q=rap)
> + [SAP Learning Course: Building Apps with RAP](https://learning.sap.com/courses/building-apps-with-the-abap-restful-application-programming-model)
> + [SAP Learning Journey: Creating a Fiori Elements App with RAP OData V4](https://learning.sap.com/learning-journeys/getting-started-with-creating-an-sap-fiori-elements-app-based-on-an-odata-v4-rap-service)
> + [SAP Technology Blog: Getting Started with RAP](https://community.sap.com/t5/technology-blog-posts-by-sap/getting-started-with-the-abap-restful-application-programming-model-rap/ba-p/13420829)
