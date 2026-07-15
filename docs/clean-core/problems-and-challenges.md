---
layout: page
title: Problem areas and challenges
permalink: /clean-core/problems-and-challenges/
parent: Clean Core
nav_order: 3
---

{: .no_toc}
# Key Issues and Challenges

1. TOC
{:toc}


For established brownfield customers or SAP add-on vendors (partners) that rely on legacy technologies, the consistent implementation of a clean-core concept is not feasible without a redesign of the processes.

## Customer Code

Most of the customer code that has accumulated over decades needs to be rewritten. The reason for this is that existing development is often based on non-released APIs or development components from the SAP standard. As a first step, you should analyze whether you want to make your system cloud-ready. In doing so, you should also check which solutions may already be using outdated technologies, such as BOPF, complex variant configuration settings, or the traditional classical reports.

In addition to customer-specific extensions to the standard SAP system, every SAP system involves custom SAP applications—in-house developments that run in parallel with the standard SAP system. Replacing such applications requires large-scale projects of their own and must continue to be managed by process experts.
 
The discrepancy between SAP’s view of the Clean Core and that of its long-standing customer base lies in the application of Clean Core principles and concepts.

Standard transactions, standard BAdIs, and standard Fiori apps are often no longer sufficient to meet business process requirements. Traditional extensions and RICEFW objects have delivered value that must now be recreated in S/4HANA—the Clean Core. To leverage new technologies, such as SAP Build, particularly on the BTP, investments in organization, technology, and processes are required.
 
## Technologies

From negotiating licenses, setting up the infrastructure, training SAP Basis staff and developers on new technologies, to purchasing consulting services and reviewing and evaluating alternatives, everything must be defined in the evaluation of the development landscape.

There is a particular need for alternative technologies that can be used with existing ABAP developers, as existing customer enhancements and RICEFW objects must continue to be maintained.
 
## Organization

The classic consultant and developer develops through the new technologies into a full-time developer with broad development knowledge; massive change management is required here. You can find out more about this in [Organization chapter]({{ site.baseurl }}/organization/).

Thanks to no-code and low-code options—particularly SAP Build, but also Key User Extensibility—non-developers can contribute to fusion teams. This approach benefits from agile practices.

## (Business) Processes
 
Organizational processes can be significantly streamlined, for example in reporting. When standard CDS views and standard APIs are used, the authorization checks are handled within the CDS view. This allows you to offer data products, and business department colleagues can generate reports without involving IT. A potential issue: This carries the risk that underperforming CDS views (keyword: compatibility views) could significantly impact system load.

Standard processes are supported by SAP, and even non-developers can easily customize standard Fiori apps in the UI. Customers with a long history of using SAP often have business process requirements that go far beyond the standard apps. Another potential issue involves SAP SEGW project-based apps: Once the standard Fiori app is built on SAP SEGW projects and then migrated to the RAP model in the backend following a system upgrade, the custom development must first be recreated in the new RAP model.

## Add-ons

Clean Core continues to affect add-ons that can be used in the ABAP system. To enable partners to support their customers’ Clean Core strategy in the future, SAP has changed the requirements for obtaining add-on certification. Consequently, it is no longer possible to obtain certification for an add-on if the implementation of the extension does not comply with Clean Core requirements (created in ABAP Cloud or the BTP).

For add-ons without SAP certification in SAP S/4HANA (On-Premise) or SAP S/4HANA Cloud Private Edition, we therefore recommend that you check with the add-on partner well in advance to confirm whether they have developed their product in accordance with Clean Core, or that a compatible add-on will be delivered in time for an upcoming upgrade.
