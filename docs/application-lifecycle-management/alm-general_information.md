---
layout: page
title: ALM background knowledge and tool support
permalink: /application-lifecycle-management/alm-general_information/
parent: ALM
nav_order: 2
---

{: .no_toc}
# ALM background knowledge and tool support

1. TOC
{:toc}

## ALM support from SAP

The SAP supports the ALM subject area by extensively providing various tools, best practices and services (see [SAP Support - ALM](https://support.sap.com/en/alm.html)). This became particularly clear with the introduction of the SAP Solution Manager 7.0 in 2008 and the functional extensions contained in release 7.1 (2011). Since then, the Solution Manager has been used by many SAP customers as a central component of the SAP ALM strategy for on-premise systems of the SAP Business Suite 7 components. The SAP Solution Manager follows the maintenance strategy of the SAP Business Suite 7 and will (as of May 2025) be maintained by the SAP until the end of 2027 (with extended maintenance support until 2030).

The successful product to the SAP Solution Manager is called SAP Cloud ALM and is - as the name suggests - a pure Cloud solution that runs on the SAP Business Technology Platform (BTP). SAP Cloud ALM has been under construction for several years and is continuously being developed further in close coordination with DSAG and user companies. The scope of functions is currently still limited compared to the SAP Solution Manager and is currently (as of May 2025) more suitable for smaller companies without ALM that has grown over the years and for cloud-centric system landscapes.

Other SAP products from the ALM family are SAP Focused Run as an independent on-premise system for the monitoring area, as well as the SAP Solution Manager addons Focused Build for e.g. agile projects and Focused Insights for dashboards of all kinds.

In summary, the products mentioned above cover the following range of functions:

**Anforderungsmanagement**

- Capturing, documenting and tracking business requirements
- Support in aligning IT and business goals

**Change and request management**

- Controlling changes to SAP systems
- Planning and execution of releases and transports
- Minimizing downtime and risks through structured processes

**Test management**

- Planning, carrying out and documenting tests
- Integration of manual and automated tests
- Quality assurance before go-lives

{: .note }
> [Test management](/ABAP-Leitfaden/testing/index)

**IT-Service-Management (ITSM)**

- Support with disruption management, incident and problem handling
- Integration with ITIL-compliant processes

**Project and Portfolio Management (PPM)**

- Planning, management and control of IT projects
- Resource management and budget tracking

**Custom Code Management**

- Analysis and optimization of custom ABAP code
- Assessment of system load and maintainability

**Application Operations / System Monitoring**

- Real-time monitoring of SAP systems
- Proactive error detection and performance optimization

**Business Process Monitoring and Optimization**

- Monitoring and analysis of business processes
- Identification of optimization potential

**Documentation and knowledge management**

- Central storage of technical and functional documentation
- Reusability of information and know-how backup

{: .note }
> - [SAP Support - Application Lifecycle Management (ALM)](https://support.sap.com/en/alm.html)
> - [E3-Special SAP Solution Manager](https://e3mag.com/wp-content/uploads/2018/03/1205-E-3_Extra.pdf)

## Benefits of ALM

The added value of a consistent ALM approach lies in the structured recording, documentation and traceability of all activities across the entire life cycle of an application. Internal and external actors benefit equally from this.

The ALM - correctly implemented and strictly applied - can meet the auditors' requirements for legal regulations, such as the complete documentation of all changes to systems that affect finance-relevant processes (Section 239 Paragraph 2 HGB, Section 257 HGB). This affects requirements management, traceable test and transport management, and complete documentation including all changes, to highlight only the most important aspects.

From the perspective of the SAP development, the Change Request Management (ChaRM) is primarily worth highlighting, as it perfectly combines the processes and applications of requirements and transport management and can be expanded to include various consistency and quality checks.

With regard to documentation, there is, among other things, the option of automatically reading development objects from the connected SAP systems and then assigning them (manually) to the corresponding processes, which can simplify changes to processes by the developer.