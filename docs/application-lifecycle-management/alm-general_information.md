---
layout: page
title: ALM background knowledge and tool support
permalink: /application-lifecycle-management/alm-general_information/
parent: ALM
nav_order: 2
---

{: .no_toc}
# ALM Background Knowledge and Tools

1. TOC
{:toc}

## ALM Support from SAP

SAP supports the ALM domain by providing a comprehensive range of tools, best practices, and services (see [SAP Support - ALM](https://support.sap.com/en/alm.html)). This became particularly evident with the introduction of SAP Solution Manager 7.0 in 2008 and the functional enhancements included in Release 7.1 (2011). Since then, Solution Manager has been used by many SAP customers as a central component of their SAP ALM strategy for on-premise systems based on SAP Business Suite 7 and, as of May 2025, will continue to be maintained by SAP until the end of 2027, with extended maintenance support available until 2030.

The successor product to SAP Solution Manager is SAP Cloud ALM. As the name suggests, it is a cloud-only solution that runs on the SAP Business Technology Platform (BTP). SAP Cloud ALM has been under development for several years and continues to be enhanced in close collaboration with the DSAG and customer organizations. Compared to SAP Solution Manager, its functional scope is currently still more limited and, as of May 2025, is primarily suited for smaller organizations without a mature ALM landscape that has evolved over many years, as well as for cloud-centric system landscapes.

Other SAP products in the ALM family include SAP Focused Run, a standalone on-premise system for monitoring, as well as the SAP Solution Manager add-ons Focused Build (for agile projects, for example) and Focused Insights (for dashboards of all kinds).

In summary, the products mentioned above cover the following range of functions:

**Requirements Management**

- Capture, documentation, and tracking of business requirements
- Support for aligning IT and business objectives

**Change and Request Management**

- Control of changes to SAP systems
- Planning and execution of releases and transports
- Minimization of downtime and risks through structured processes

**Test Management**

- Planning, execution, and documentation of tests
- Integration of manual and automated tests
- Quality assurance prior to production deployment

{: .note }
> [Test management]({{ site.baseurl }}/testing/index)

**IT Service Management (ITSM)**

- Support for fault management, incident, and problem handling
- Integration with ITIL-compliant processes

**Project and Portfolio Management (PPM)**

- Planning, steering and monitoring of IT projects
- Resource management and budget tracking

**Custom Code Management**

- Analysis and optimization of customer-specific ABAP code
- Assessment of system load and maintainability

**Application Operations / System Monitoring**

- Real-time monitoring of SAP systems
- Proactive error detection and performance optimization

**Business Process Monitoring and Optimization**

- Monitoring and analysis of business processes
- Identification of opportunities for optimization

**Documentation and Knowledge Management**

- Centralized storage of technical and functional documentation
- Reusability of information and preservation of know-how

{: .note }
> - [SAP Support - Application Lifecycle Management (ALM)](https://support.sap.com/en/alm.html)
> - [E3-Special SAP Solution Manager](https://e3mag.com/wp-content/uploads/2018/03/1205-E-3_Extra.pdf)

## Benefits of ALM

The added value of a comprehensive ALM approach lies in the structured recording, documentation, and traceability of all activities throughout the entire lifecycle of an application. Both internal and external stakeholders benefit equally from this.

Thus, when correctly implemented and rigorously applied, ALM enables compliance with auditors’ requirements regarding legal regulations – such as the complete documentation of all changes to systems affecting finance-related processes (Section 239 para. 2 of the German Commercial Code (HGB) and Section 257 HGB). This encompasses requirements management, traceable test and transport management, and complete documentation – including all changes – to highlight only the most important aspects.

From an SAP development perspective, Change Request Management (ChaRM) is particularly noteworthy because it integrates requirements and transport-management processes and can be extended with various consistency and quality checks.

With regard to documentation, it is possible, among other things, to automatically extract development objects from the connected SAP system and then (manually) assign them to the corresponding processes, which can simplify, for example, the modification of processes by the developer.
