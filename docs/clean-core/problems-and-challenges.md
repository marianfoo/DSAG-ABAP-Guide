---
layout: page
title: Problem areas and challenges
permalink: /clean-core/problems-and-challenges/
parent: Clean Core
nav_order: 3
---

{: .no_toc}
# Problem areas and challenges

1. TOC
{:toc}


For established brownfield customers or SAP add-on manufacturers (partners) who are based on legacy technologies, the consistent implementation of a Clean Core concept is not possible without a redesign of the processes. 

## Custom code

Most of the customer code that has grown over decades needs to be reworked. The reason for this is that existing developments are often based on unreleased APIs or development components from the SAP standard. The first step should be to analyze whether you want to make your system Cloud-Ready. You should also check which solutions may already use outdated technologies, such as BOPF, the complex variant configuration settings or the classic report.

In addition to the customer extensions in the SAP standard, there is the issue of custom SAP applications in every SAP system, which are in-house developments that run parallel to the SAP standard. Replacing such applications requires major projects of its own and must continue to be supported by process experts. 
 
The dissonance between the SAP view of the Clean Core and the long-standing customer base is the application of the Clean Core principles/concepts. 

The standard transactions, standard BADIs and standard Fiori apps are often no longer sufficient to cover the business process requirements. The classic extensions / RICEFW objects have created added value that first has to be found in S/4HANA - the Clean Core. In order to use the new technologies, for example SAP Build, especially on the BTP, it requires investments in organization, technologies and processes.
 
## Technologies

From negotiating the licenses, setting up the infrastructure, training the SAP base and training the developers of the new technologies to purchasing consulting services, considering and evaluating alternatives, everything must be defined in the evaluation of the development landscape.

Above all, alternative technologies that can be used with existing ABAP developers are needed, as existing customer extensions/RICEFW objects still need to be maintained.
 
## Organization

The classic consultant and developer develops through the new technologies into a full-time developer with broad development knowledge; massive change management is required here. You can find out more about this in [Organization chapter]({{ site.baseurl }}/organization/).

Thanks to the no-code and low-code options, especially with SAP Build, but also key-user extensibility, non-developers can work in Fusion teams. This also requires a modern way of working, which should be agile in nature.
 
## (Business) processes
 
Organizational processes can be enormously streamlined, for example in reporting. If standard CDS views and standard APIs are taken, then the authorization checks in the CDS view. This means you can offer data products and your department colleagues can do reporting without IT. A possible problem: This brings the risk that un-performing CDS views (keyword: compatibility views) will have an enormous impact on the system load.

Standard processes are supported by the SAP and standard Fiori apps can also be easily adapted in the UI by a non-developer. Customers with a long SAP history often have business process requirements that go far beyond the standard apps. The SAP SEGW project-based apps are also a possible topic: if the standard Fiori app is first built on the SAP SEGW projects and then, after a system upgrade, this app moves to the RAP model in the backend, the in-house development must first be recreated in the new RAP model.

## Add-Ons

Clean Core continues to impact add-ons that can be used in the ABAP system. So that a partner can support your customers' Clean Core strategy in the future, SAP has changed the conditions for obtaining certification of add-ons. It is therefore no longer possible to obtain certification of an add-on if the implementation of the extension does not comply with the specifications of Clean Core (created in ABAP Cloud or the BTP).

For add-ons without SAP certification in SAP S/4HANA (on premise) or SAP S/4HANA Cloud, private edition, we therefore recommend checking with the add-on partner in good time whether they have developed their product according to Clean Core, or that a compatible add-on is available in time for an upcoming upgrade be delivered.
