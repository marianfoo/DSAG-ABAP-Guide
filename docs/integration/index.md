---
layout: page
title: Integration
permalink: /integration/
nav_order: 12
---

{: .no_toc}

# Integration

1. TOC
{:toc}

The integration of SAP systems, and also non-SAP systems, would itself go beyond the scope of this guide. Therefore, here you will primarily find technologies currently in use and an approximate direction as to which technologies will exist in the next few years. You should always keep in mind that middleware also plays an important role in distributing data and monitoring. See also section [Chapter Clean Core]({{ site.baseurl }}/clean-core//what-is-clean-core/) 

Additionally, you should note that with the increasing migration of SAP systems to the Cloud, non-functional requirements (NFRs) such as availability, security, scalability and observability must be taken into account from the outset. These aspects are often self-evident in on-premise environments, but must be rethought and actively integrated in the Cloud. Inadequate planning can lead to high costs for improvements, especially if a system only shows its limits when the number of users increases or in an emergency. [See article "The Seven Reasons Your SAP Tech Initiatives Are Failing"](https://secondphase.com.au/seven-reasons-sap-tech-failing/)

### Business Accelerator Hub

The [Business Accelerator Hub](https://api.sap.com/) from SAP provides standardized documentation for all types of interfaces. If you would like to find out more about the available standard interfaces for your SAP product, you should first check the options here. Searching by product, technology and module makes it easier to find the right interfaces.

## Technologie

This section is about various interface technologies and gives you a rough overview of the common technologies.

### IDoc

Intermediate Document, IDoc for short, is a data exchange format from SAP to integrate different systems with each other. The data can be loaded into the system or exported from it. Most IDocs are created on a position basis, which means the entire data record is on one line and the format for the data is derived via identification (usually the first part of the line). In more current systems there are also IDocs in XML format.

### RFC

Remote Function Call, RFC for short, is the use of classic function blocks for communication across system boundaries. So-called destionations can be used to call a function module in another system.

It is also possible to call function blocks from non-SAP systems; there are adapters for the various programming languages, which are usually provided by SAP. You can find some examples here:

- [JCo](https://support.sap.com/en/product/connectors/jco.html) (Java)
- [SAP Connector for Microsoft .NET](https://support.sap.com/en/product/connectors/msnet.html)
- [SAP Cloud SDK](https://sap.github.io/cloud-sdk/docs/java/features/bapi-and-rfc/overview) (Java)
- [@sap/cds-rfc](https://www.npmjs.com/package/@sap/cds-rfc) (Node.js for CAP)

### SOAP

Simple Object Access Protocol, SOAP for short, is a standardized interface format for exchanging XML messages between different systems. The technology is also used for interfaces outside the SAP world. The format of the payload is not limited to XML, but CSV or BASE64 data can also be used (still needs to be checked).

### OData

The Open Data Protocol, OData for short, is a standardized protocol for HTTP communication. This describes standards, how requests and responses are provided by interfaces and what integration into the HTTP protocol looks like. Communication can take place in XML, but also JSON format. OData is now the standard for building UI and API interfaces in the SAP system. The currently available version is "OData v4" and offers additional options for integrating applications compared to "OData v2".

### HTTP

In principle, all interfaces that have Hypertext Transfer Protocol, or HTTP for short, can also be consumed via SAP and via HTTP Client. However, the implementation is usually limited to individual development and you should check beforehand whether there are standard exchange formats such as OData or SOAP.

### Event

You can create the current integration with events. An event is generated at defined times in the standard or customer process, which is made available in a queue (e.g. via SAP Event Mesh). Interested applications and processes can register on the queue, which will then be notified of new events. An event is usually a simple message with the triggering event, the key of the object and a payload.

## Clean Core

Which technologies are actually still relevant when switching to Clean Core and which ones should you best avoid today? In this section, you will learn about the recommended technologies when building or migrating to Clean Core. You will find information about this in the SAP guide “[Supporting Business Transformation with a Cloud ERP Clean Core Strategy](https://www.sap.com/germany/index.html)”.

![Clean Integration](./img/image-01.png)

Recommendation for Clean Core integration
{: .img-caption}

Here you will find an overview of the technologies mentioned above, divided into the areas to continue and to avoid. The distribution results from the recommendations in the guide.

| Verwenden   | Vermeiden |
| ----------- | --------- |
| OData       | RFC       |
| SOAP        | IDoc      |
| Events      |                                            |
| HTTP (REST) |                                            |

## Recommendations for borderline cases

When integrating SAP systems, there are borderline cases in which not all standardized SAP integration types can be used optimally. In such scenarios, it is essential to carefully differentiate from other SAP and non-SAP tools.

### Consideration of future developments

SAP continuously develops its integration solutions. Therefore, it should always be checked which technologies will become more important in the future and which may be replaced by newer solutions. Future-oriented planning helps to avoid technological dead ends and to make the integration stable and sustainable in the long term. 

### Bestand alter Technologien

Although SAP continues to provide new integration solutions, some older technologies remain valuable and cannot yet be fully replaced. It is therefore important not to decommission existing solutions too quickly, but rather to assess their relevance in the respective corporate context. For example, **IDoc** and **RFC** are deeply rooted in many legacy systems and continue to provide reliable communication options.

### Sustainable architecture and Clean-Core strategy

The design of sustainable architecture should be done taking into account the **Clean-Core strategy**. The Public Cloud often serves as a model for sample integrations that are characterized by high standardization and ease of maintenance. The aim is to keep the amount of individual code low and to give preference to standard solutions.

### Important decision factors in borderline cases

- **Costs:** The financial effort for development (resources), operation, licenses and maintenance must be weighed against the benefits.
- **Features:** Check whether existing integration solutions cover all required functions or whether adjustments are required.
- **Vendor Lock-In:** Dependencies on certain SAP or third-party technologies should be viewed critically.
- **Monitoring:** Effective monitoring of the integration is essential to identify and resolve problems at an early stage. Reprocessing scenarios must be provided in the event of system failures.


### Example: mass data transfer 

#### EDI (Electronic Data Interchange) in S/4HANA

(Web) APIs based on REST or SOAP have their limitations. Other technologies should be used for this. For example, SAP EDI is designed to process large amounts of electronic data for 100,000+ messages per day - and is done with numerous B2B partners using standardized formats such as EDIFACT.

In a direct comparison, it quickly becomes clear why IDocs are the better choice for SAP EDI: They are asynchronous, designed for mass data and offer predefined validations as well as robust monitoring and reprocessing mechanisms. APIs, on the other hand, are **mostly** synchronous, process messages individually and require additional effort for error handling and mappings. Therefore, in high-load scenarios, a API-based EDI integration can cause significant performance issues and high operating costs.

#### Additional solutions for mass data transfer

- [SAP Landscape Transformation Replication Server](https://www.sap.com/germany/products/technology-platform/landscape-replication-server.html), ABAP and NetWeaver based 
- [SAP HANA Smart Data Integration (SDI)](https://help.sap.com/docs/SUPPORT_CONTENT/hanasdi/4740563873.html?mt=de-DE), SAP HANA Datenbank basiert
- [Master Data Governance (MDG)](https://www.sap.com/documents/2015/07/3a2f4c59-5b7c-0010-82c7-eda71af511fa.html), based on the Data Replication Framework in ERP

## Cloud Connector

If you are using the Business Technology Platform (BTP), you also need a Cloud connector in your infrastructure in order to be able to establish a connection from the Cloud to on-premise. The Cloud Connector acts as a gateway and proxy and routes network traffic from the Internet to the correct systems in your landscape behind the firewall.

### Aufbau

When setting up your Cloud connector landscape, you should pay attention to the separation of the system rails, as the stricter rules for access to resources usually apply in production. In this case, at least two instances are suggested, one for DEV/TEST and one for PROD. Depending on the ongoing processes and their importance, you should think about a corresponding fail-safe structure (high availability).

### Protokolle

There are currently two protocols that are used in most use cases and accesses.

- HTTP - The leading protocol is OData and SOAP, but plain HTTP is also possible to address data and systems on-premise.
- RFC - RFC-capable function blocks can also be consumed, even if they are no longer the strategic goal of the SAP, so many functions of the system are available without violating Clean Core.

The resources are released in the respective configured systems in the Cloud Connector. With HTTP, the corresponding paths/URLs are released, with RFC the corresponding function modules. In production, we recommend explicitly releasing resources and avoiding wildcards (*).

### Erweiterungen

If you create extensions in the BTP, you usually do so using CAP (Cloud Application Programming Model) or RAP (ABAP RESTful Application Programming Model). So that you can then access data, you need a configured Cloud connector on the sub-account. The configuration is not part of this guide as it is mostly carried out by your SAP base. 

In most cases, you will configure the connection to the on-premise system in the BTP Destination Service. If you use the SAP BTP ABAP Environment to create your extensions, you can also map these in the system as Communication Arrangements and Communication Systems and do not need the configuration in the Destination Service. However, if you want to expand standard Fiori applications, you need access via the sub-account to gain access to your systems.

### Zugriffsrichtung

So far you have mainly read about access from the Internet or the BTP towards on-premise. The Cloud Connector can also be used as a proxy to route from an on-premise system to a Cloud system and avoid the direct connection of the Cloud system. The ABAP Test Cockpit on the ABAP Environment is one such case.
