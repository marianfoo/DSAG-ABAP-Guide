---
layout: page
title: Open Source
permalink: /open-source/
has_children: true
nav_order: 11
---

{: .no_toc}
# Open Source

1. TOC
{:toc}

Open source has a particularly difficult time gaining a foothold in ABAP development. There are still objections that the use of available software in the business-critical SAP systems is not possible or justifiable with the company data. There are solutions for many of the legitimate objections to minimize the _risks_ and to be able to use the [_Chancen_](#motivation-und-chancen), which offers open source software. In other programming languages, the opportunities have long outweighed the remaining risks and processes and tools have been created to effectively integrate open source components into your own development process. This chapter is intended to give you an overview of the current status of open source in ABAP development and introduce processes and tools to...

1. ...to integrate open source projects into your own solutions ([Use of open source software](using-open-source-software))
2. ...an Open-Source-Projekten mitzuwirken ([Beteiligung an Open-Source-Software](contributing-to-open-source-software))
3. ...provide your own solutions as an open source project ([Open source software development](developing-open-source-software)).

{: .recommendation }
Every company has to develop an _open source strategy_ for itself. Here you will find a working basis and experience reports.

## What is Open Source?

Open source software (OSS) is software that is provided under a [_Open-Source-Lizenz_](licenses). In all three use cases mentioned above, the license is decisive for the use, modification and further distribution of the provided coding. In addition, this must be _freely available_, i.e. not only made available to a certain group of people. This allows you, for example, to check the source code of an application before use and generate the binaries for execution yourself, instead of trusting that the files provided correspond exactly to the checked version of the source code. If in doubt, you can fix bugs yourself instead of having to wait for the software provider or rely on support. You can develop additional functionality and integrations yourself and also make them available to other users of the software. You can check promised features such as end-to-end encryption and disabled telemetry yourself.

You can find a comprehensive definition of open source at the open source initiative on the following website: [The Open Source Definition](https://opensource.org/osd).

{: .note }
SAP S/4HANA is not "open source" just because you as a developer can read the source code written by the SAP. Open source is much more than simply making the coding available to the customer and involves free use, modification and redistribution, _without being in a customer relationship_ with the software provider.

## Motivation and opportunities

Why should you consider open source in ABAP development? The number of scenarios in which you encounter open source, and _also_ open source ABAP, in everyday life is slowly but steadily increasing. The number of ABAP projects available in the open source community is growing - over 300 projects are listed on [dotabap.org](https://dotabap.org). SAP itself publishes software as open source projects, such as [Code Pal for ABAP](https://github.com/SAP/code-pal-for-abap-cloud) or [RAP Generator](https://github.com/SAP-samples/cloud-abap-rap) and various tutorials or learning content, such as [RAP100](https://github.com/SAP-samples/abap-platform-rap100) or [Fiori Elements Feature Showcase for RAP](https://github.com/SAP-samples/abap-platform-fiori-feature-showcase). Categorically closing yourself off to this increasingly leads to missed __opportunities...__

### ...in optimizing your own development processes

1. With tools like [ABAP Cleaner](https://github.com/SAP/abap-cleaner), [Code Pal for ABAP](https://github.com/SAP/code-pal-for-abap-cloud) and [abapOpenChecks](https://github.com/larshp/abapOpenChecks) you can relieve developers of the burden of implementing development guidelines and best practices by partially implementing them automatically and statically checking them in other parts and actively pointing out findings to developers. And this far exceeds the scope of the options provided in the SAP standard.  
2. With [abapGit](https://abapgit.org/) you have the opportunity to harmonize your development processes _across technologies_ with uniform tooling and to manage your entire company codebase in a single source of truth, instead of viewing ABAP as a special snowflake with special rules. You can conduct code reviews with dedicated tooling. You can automatically undo changes that have been made if the department no longer wants them after development time, without major manual dismantling effort. And all of this even on systems from ABAP release 7.02.
3. With the help of [abaplint](https://abaplint.org/) you can check, develop ABAP coding outside of a SAP system and even [carry out](https://transpiler.abaplint.org/) with the transpiler. This allows you to set up continuous integration pipelines without having to operate your own SAP systems at high cost and to carry out static code analyzes and unit tests (with limitations compared to execution in ABAP systems).  
4. You can generate boilerplate coding using generators like the [RAP Generator](https://github.com/SAP-samples/cloud-abap-rap) or [ABAP OpenAPI Generator](https://github.com/abap-openapi/abap-openapi) and then just have to adapt it. In this way, development costs can be saved and, in particular, prototypes can be set up quickly.

### ...in the implementation of business requirements

1. With [abap2xlsx](https://github.com/abap2xlsx/abap2xlsx) you can implement the creative requirements of the departments for creating, reading and modifying Excel files. And that already from ABAP release 7.31. You don't have to adapt your processes because the OLE-based SAP-API for Excel folders does not support background jobs and expects the user to have Microsoft Office installed. In particular, you do not have to invest the development effort to implement and maintain a codebase that deals with conversion and handling of Excel files. And you don't have to reject the requirement as not proportionally feasible given the implementation effort; you can build on the work that others have already done.
2. The situation is similar with other technical problems for which there are already established open source solutions. For example, [ABAP Logger](https://github.com/ABAP-Logger/ABAP-Logger) instead of separate wrapper classes around the function modules of the Business Application Log. Or [ajson](https://github.com/sbcgua/ajson) as a JSON library for ABAP release 7.02.

### ...in external representation

1. You can evaluate whether reusable components of your ABAP-based solutions would also make sense as an open source project. Coding that does not implement your business model in competition, but rather serves to optimize the development process or overarching topics such as user experience, revision security or operations, could also be used by other companies. If you publish these components as available software, you enable external participation in the development from which you can benefit.  
In addition, this can serve as a flagship when recruiting new developers. They can see directly that you develop in a modern way and are not afraid to show the source code to the outside world.  
Examples: [IBM](https://github.com/IBM?q=&type=all&language=abap&sort=), [Microsoft](https://github.com/microsoft?q=&type=all&language=abap&sort=), [rku.it](https://github.com/rku-it-GmbH?q=&type=all&language=abap&sort=), [Schwarz IT](https://github.com/SchwarzIT?q=&type=all&language=abap&sort=)
2. If your company provides services that are implemented through interfaces with partners/customers who also implement them in your SAP systems using ABAP, you can provide an open source SDK that implements your API. Users of the SDK have the opportunity to open issues or suggest additional features themselves via pull requests and reduce your implementation effort or offer more functionality in your software. You can deploy the SDK internally yourself or use it for integration testing.  
Examples: [ABAP SDK for Azure](https://github.com/microsoft/ABAP-SDK-for-Azure), [ABAP SDK for Google Cloud](https://cloud.google.com/solutions/sap/docs/abap-sdk/overview), [AWS SDK for SAP ABAP](https://aws.amazon.com/sdk-for-sap-abap/), [Microsoft AI SDK for ABAP](https://github.com/microsoft/aisdkforsapabap), [ABAP SDK for IBM watsonx](https://github.com/IBM/abap-sdk-nwas-x)

### ...in upskilling developers

1. By exploring external libraries and implementing them, you can expand your knowledge of object-oriented design and software architecture. You can become familiar with new technologies or approaches directly with productive source code, instead of demo examples. This effect increases particularly when you participate in your own features or bug fixes and code reviews.

{: .recommendation }
As you can see, there are many places where open source can provide significant added value, including in ABAP development. It is therefore always worth considering the topic, even if only some of the points mentioned above are specifically relevant to you.

## Ausbaustufen

A possible approach to the topic is to see the different use cases as building on one another:

1. You can first deal with the topic of how you can __integrate open source tools into your development process__ and thus immediately achieve added value. Initially, it's not about open source software components that are in your coding, but simply about tools that are part of your development process and therefore only in your development system landscape. This is often the easiest case to look at and a good entry point into the topic.  
This expansion stage is described in [Use of open source software](using-open-source-software).
    1. This level can optionally be expanded with the __use of open source projects in your developed software solutions__. In this case, the open source components also reach your productive system or are delivered as part of your software.

2. Next, you can consider __participation in open source projects__. You expand or modify an open source project and make these adjustments available to the community so that other companies can also benefit from them. In order for developers to be able to participate in this way, your company must have a guideline on how this can be specifically designed.  
This stage is covered in [Beteiligung an Open-Source-Software](contributing-to-open-source-software).

3. The final stage is __developing your own software as open source software__. In this case, you offer selected components of your own software solutions as open source software, thereby enabling others to use them and also participate in them.  
This stage is discussed in [Open source software development](developing-open-source-software).

The individual levels offer different opportunities, but also come with different risks and expenses. These are taken up in the subchapters mentioned.
