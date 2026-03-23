---
layout: page
title: User Interface (UI)
permalink: /user-interface/
nav_order: 6
---

{: .no_toc}
# User Interface (UI)

1. TOC
{:toc}

This chapter provides an overview of various UI technologies used in the context of the ABAP system. Due to its relevance, the main focus is on Fiori (SAPUI5). Later, however, an overview of older and some still relevant technologies will also be given.

{: .recommendation }
> * In most cases, a Fiori-compliant surface should be used for new developments.  
> * Whenever possible, new applications should be implemented with Fiori Elements. SAPUI5 freestyle apps often tempt you to allow yourself to be lured into increased complexity through additional freedom and usually lead to significant additional effort.

## Fiori & SAPUI5

SAP Fiori describes the new user experience of current SAP solutions, which were created based on modern design principles. Fiori is the strategic surface technology of SAP and should be viewed as a set technology in most cases of new developments. However, the term **Fiori** means partly different topics:

* Fiori as a design language for modern surfaces
* Fiori recommendations for good user experience
* Fiori Elements technology for annotation-based generation of applications
* Development of Fiori apps with SAPUI5

The pure design and UX recommendations of the SAP can theoretically also be implemented with other technologies. However, so that newly designed applications can be integrated natively into the SAP environment and look and operate similarly for users, it is important to adhere to these recommendations. This should be taken into account early on in the process and, depending on the situation, also ensured with design thinking or mockup creations with SAP's [Fiori Design Stencils](https://www.sap.com/design-system/fiori-design-web/v1-96/resources/libraries/downloads?external), for example for [Figma](https://www.figma.com/de-de/design/). Both developers and technical consultants should therefore be familiar with the [Fiori Design Guidelines](https://experience.sap.com/fiori-design/).

Apart from the purely visual and interactive view of the Fiori Guidelines, Fiori also generally refers to the actual development and technology behind the Fiori apps. Here you can choose between the generated Fiori Elements apps without front-end coding and freestyle applications that are developed with SAPUI5 (i.e. Type or JavaScript). The Flexible Programming Model offers a hybrid of both. These different options are explained in more detail later in the chapter. In general, however, it can be said that Fiori applications are consumed by users as a browser website. Therefore, use is no longer restricted to devices on which the SAP GUI can be installed - a modern web browser is sufficient. This means that Fiori apps can also be used on mobile devices such as smartphones, tablets or AR headsets.

Accompanied by this separation is the stronger distinction between front and backend development than you may be familiar with from previous SAP developments. As a backend, the S/4 system provides data storage, authorization checking and most of the transaction logic for apps. This will be published externally as the OData service.  This serves as an interface for the actual frontend app (the Fiori app running in the browser) to read, write data or execute actions. This communication via OData is stateless by definition, so the backend is the single source of truth for the data status and manages the majority of the data logic. In certain scenarios, this dichotomy can complicate development. For example, this also created the need for the draft concept to enable the provision of interim data sets.

Even though it has now been archived, we would like to point out the (English-language) [DSAG UI5 Best Practice Guide](https://1dsag.github.io/UI5-Best-Practice/) at this point.  The following table compares the advantages and disadvantages of SAPUI5: 

| SAPUI5 Advantages                    | SAPUI5 Disadvantages       |
| ------------------------------------ | ------------------------- | 
| Comprehensive collection of standard UI elements that greatly simplify implementation. | JavaScript required (ABAP only in the backend). Therefore skill building is necessary. |
| Most modern look | SAP Gateway required (additional cost if installed separately) |
| Theoretically, everything that HTML5 allows in conjunction with JavaScript is possible. | In special cases there may be missing features and poorer performance compared to SAP GUI / ALV. |
| Use on tablets and smartphones. | Complex apps require more effort (stateless apps) |
| Responsive UI (automatic adaptation to the respective device) |    |
| Use of end device capabilities such as cameras |    |
| Native SAP Fiori launchpad integration |    |
| Relatively new, constantly evolving technology. Therefore optimal integration into current web browsers |    |

### Fiori Elements
The Fiori Elements Framework makes it possible to implement full-fledged Fiori business applications largely without front-end experience (JavaScript, XML). There are also some pre-built floorplans (app types) of the SAP, which are generated based on a OData service. The most common use case is the combination of [List Report](https://experience.sap.com/fiori-design-web/list-report-floorplan-sap-fiori-element/) and [Object Page](https://experience.sap.com/fiori-design-web/object-page/). These types can be used to implement transactional scenarios in which individual business data records can be listed in a searchable table and clearly created or changed in the object page. The [Analytical List Page](https://experience.sap.com/fiori-design-web/analytical-list-page/) enables a standardized display for evaluating analytical data sets.

In principle, it is sufficient for creation to enrich the OData service with UI annotations. For this purpose, the desired configurations are stored in the CDS Consumption View or Metadata Extensions. Published via the OData service, the Fiori Elements Framework evaluates the annotations at runtime and generates the Fiori app accordingly. The [ABAP RESTful Application Programming Model (RAP)](../abap/restful_abap.md) is particularly suitable for the development of transactional Fiori Elements applications. For development, reference is made to the [DSAG ADT Guide](https://1dsag.github.io/ADT-Leitfaden/), as the necessary UI annotations to generate Fiori Elements apps can only be created in the Eclipse development environment.

The UI5 ​​​​Demo Kit contains some official [Tutorials and courses](https://sapui5.hana.ondemand.com/#/topic/8b49fc198bf04b2d9800fc37fecbb218) of the SAP to get you started with the Fiori Elements development. The [Fiori Elements Feature Map](https://sapui5.hana.ondemand.com/sdk/#/topic/62d3f7c2a9424864921184fd6c7002eb) offers a good overview of the possibilities and information on how to implement individual features accordingly. In principle, development with the Cloud Application Programming Model (CAP) is also possible - but in the context of this ABAP guide, this is not the focus.

### Fiori Freestyle
If the floorplans provided by SAP are not sufficient for an application to be developed, the UI interface must be developed manually. A Fiori Freestyle development is used for this. The Fiori development is implemented using the SAPUI5 framework, which requires knowledge of JavaScript, XML views and the MVC concept.

An empty application shell with a connection to a OData service can be created using Fiori tools. However, the remaining application logic must then be implemented yourself. The representation of the actual surface is defined via XML views. For this purpose, SAP provides a wide selection of controls that save a lot of implementation effort and support a Fiori-compliant design. These can be viewed broken down by version in the [SAPUI5 API Referenz](https://sapui5.hana.ondemand.com/#/api).

SAPUI5 is also distributed under an open source license under the name [OpenUI5](https://openui5.org/). However, some components are not included in the distribution. In principle, Fiori applications can be implemented as required even without using a SAP backend.


### Flexible Programming Model
The [Flexible Programming Model (FPM)](https://ui5.sap.com/test-resources/sap/fe/core/fpmExplorer/index.html#/overview/introduction) offers a mix of generated Fiori Elements and manually developed SAPUI5 Freestyle interfaces. It is available from SAPUI5 v1.94 and only with OData V4. The FPM makes it possible to integrate freestyle elements into a Fiori Elements application via independent containers. On the other hand, Fiori Elements components can also be installed in a Freestyle app. To get an impression of the advantages of the FPM, [this CodeJam](https://github.com/SAP-samples/fiori-elements-fpm-exercises-codejam) or [Learning Journey](https://learning.sap.com/learning-journeys/developing-an-sap-fiori-elements-app-based-on-a-cap-odata-v4-service/getting-an-overview-of-the-flexible-programming-model_fc9ea1ee-20a8-4add-b3f9-c8c8e3701ae0) are ideal.
  

![Flexible Programming Model as a hybrid of Fiori Elements and Freestyle SAPUI5, © SAP]({{ site.baseurl }}/user-interface/img/FPM.png)
  
Flexible Programming Model as a hybrid of Fiori Elements and Freestyle SAPUI5, © SAP
{: .img-caption}

The flexibility enabled by FPM offers you the opportunity to enjoy more freedom in development, even in generated applications. The strict choice between SAPUI5-Freestyle or Fiori Elements is pushed into the background to some extent. Encapsulated, Fiori Elements sections can be embedded via building blocks. The [Flexible Programming Model Explorer](https://sapui5.hana.ondemand.com/test-resources/sap/fe/core/fpmExplorer/index.html) provides live testable examples of FPM implementation options via Extension Points and Building Blocks and allows sample files or entire projects to be downloaded for reference.

## Legacy Technologies
This chapter is intended to provide a brief overview of previously unmentioned surface technologies. Since these become increasingly less relevant over time, individual technologies will not be discussed in more detail here.  

| UI Technology                        | SAP Roadmap               | Comment             | Recommendation for new developments           |
| ------------------------------------ | ------------------------- | ------------------- |  ---------------------------------------- |
| Dynpro (classic) | support only | SAP advises against new developments. Lower development effort, especially for simple reports with a generated selection screen. Popular with power users. | Still useful for smaller developments in many cases, but not supported in S/4 Cloud. |
| Business Server Pages (BSP) | support only | Superseded by Web Dynpro | Not useful |
| Webclient UIF | support only | Developed and used in CRM based on BSP technology | Still relevant for classic CRM apps. SAP Hybris C4C relies on SAPUI5 / SAP Fiori |
| Web Dynpro Java | support only | Should no longer be used | Not useful |
| Web Dynpro ABAP incl. Floorplan Manager | minor extensions | In combination with Floorplan Manager, less complex than standalone. | Consider SAPUI5 instead. |
| SAP Screen Personas | minor extensions | Configuration and scripting (Java script) to make existing applications based on classic screens more attractive and easier to use. | Useful for UI revision of existing Dynpro programs. |
| CRM Web UI | n/a | Surface technology known from SAP Change Request Management. | Consider SAPUI5 instead. |




