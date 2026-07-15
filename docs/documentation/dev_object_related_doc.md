---
layout: page
title: Documentation of development objects
permalink: /documentation/dev_object_related_doc/
parent: Documentation
nav_order: 2
---

{: .no_toc}
# Documentation of development objects

1. TOC
{:toc}

In addition to methods, function modules, and reports—which may contain source code—there are other development objects in the ABAP system that do not have source code and must therefore be documented in other ways. Examples of these include:

* DDIC objects
* Transactions

Since the Workbench documentation is also linked to the transport system, it is available in all individual systems within a system landscape. Furthermore, this documentation can be viewed by all users and is automatically integrated into the user interface for reports by the ABAP system. Another advantage is that the documentation can be maintained in multiple languages. On SAP systems with SAP_BASIS >= 7.40, ABAP Doc comments can be used in the source code. This can serve as an alternative to documentation in the ABAP Workbench. However, the full functionality of ABAP Doc comments can currently only be utilized with the ABAP Development Tools for Eclipse. When using Core Data Services to define DDIC objects, significantly more development objects can be documented in the source code, eliminating the need for external documentation.

Starting with SAP NetWeaver 7.50, ABAP Doc comments for classes and interfaces can be exported as HTML files. Starting with ABAP Platform 7.55, SAP is expanding its repertoire to include an additional technology for documenting ABAP development objects. The Knowledge Transfer Document focuses on the new object types that primarily originate from the ABAP RESTful Application Programming Model (RAP) context. This includes, among other things: CDS views, behavior definitions, service definitions, service bindings, annotation definitions, and packages.

## Short Descriptions

Short descriptions can be created for many objects, such as a description for a data element or a method.

## Knowledge Transfer Documents (KTD)

The Knowledge Transfer Document (KTD) has been available since ABAP Platform 7.55. With KTD, documentation can be created individually for each element of an object. It is based on Markdown, which uses a simple text formatting syntax.

KTDs must be in the same package as the development object. They are not automatically transported with the development object, but if the development object is deleted, the associated KTD is also deleted.

{: .recommendation }
> We recommend using the documentation function of the ABAP workbench for all development objects and regardless of the source code. The documentation function should be used in the following order, depending on which type of documentation object is available for which object: 1. Knowledge Transfer Documents 2. abapDoc 3. Short texts Only the current status should be documented, if necessary enriched with short references to the change documentation (transport documentation, defect numbers).

# Documentation in the Source Code

## Documentation Language

These days, development teams mostly collaborate on an international level. Even if you’re currently developing exclusively in German, your project may become internationalized over time. The effort required to address coordination issues or even to translate the code later on is disproportionate to the potentially greater effort involved in creating English documentation. It has also been shown that the readability of source code and comments is improved by using English-language comments. This is because the ABAP commands themselves are in English and structured like sentences. Therefore, when working with English documentation, the reader of the source code does not have to constantly switch languages.

{: .recommendation }
> The company should determine what language to use for comments. We recommend using English for comments.

## Documentation of Changes

Once a program goes live, care should be taken to ensure that changes to the program are properly documented. Finding the right balance is essential here: A complete version history of all changes and commented-out source code reduce the readability of the source code. Despite this drawback, some development teams deliberately document all changes in the source code to simplify debugging on production or test systems where the version history is not available.

{: .important }
> Subsequent changes to the source code should only be documented directly in the source code in exceptional cases.

## Comments in the Source Code

Comments in the source code are intended to help developers understand the source code when this cannot be achieved through clever design alone (modularization, naming of methods and variables).

Comments are intended for other developers and, as time passes, also for the original developer.

Asterisk comments should only be used in the program header or for temporarily commenting out old source code.

For all other comments, SAP recommends using inline comments. These should precede the source code they document and be indented exactly like that source code. The latter is correctly handled (only) for inline comments by the pretty printer as well.

{: .recommendation }
> You should answer the question of “why” something was programmed, not “what.” The latter is evident from the source code anyway, whereas the reasons behind it are often not immediately apparent. Yet it is precisely these reasons that are essential for understanding. The guiding principle here is: as few comments as possible, as many comments as necessary.

OTHER SOURCES

1. Horst Keller, Wolf Hagen Thümmel: ABAP programming guidelines. SAP Press, 2009. ISBN: 978-3-8362-1286-1
2. Klaus Haeuptle, Florian Hoffmann, Rodrigo Jordão, Michel Martin, Anagha Ravinarayan, Kai Westerholz: Clean ABAP. SAP PRESS, 2022. ISBN: 978-3-8362-8659-6

## ABAP Doc

ABAP Doc allows you to document classes, interfaces, and function modules. The comments consist of one or more commented lines.  
- ABAP Doc begins with the prefix `"!.`.  
- ABAP Doc can be used to document basic information about a class, method, or interface directly within the source code. In addition, you can use ABAP Doc to provide detailed documentation for each parameter of a method. These ABAP Doc comments are placed directly before declarative statements.  
- In ABAP Doc, HTML tags can also be used for formatting, which improves the readability and structure of the documentation.  
- With the recommended use of ADT, the creation of ABAP Doc is very easy and efficient by using Quickfix [DSAG AG ADT Guide: What are ABAP Doc](https://1dsag.github.io/ADT-Leitfaden/working-with-adt/features/abap-doc/#was-sind-abap-doc)

The advantage of using ABAP Doc is that these comments are displayed in the following ADT functions, providing developers with valuable information directly as they write code.

* ABAP Element Info View
* Element Information Pop-up
* Code Completion List.

These ABAP Doc comments can be extracted from ADT into an HTML file and thus used for other purposes outside the code, such as on internal web pages. If the code and the associated ABAP Doc documentation are maintained simultaneously and ABAP Doc is extracted after every change, the external documentation remains up-to-date without any additional effort.
If the ABAP Doc documentation is created in a structured manner, it can also be used with supporting generative AI to create further documentation (see [Chapter Artificial Intelligence]({{ site.baseurl }}/artificial-intelligence/#ai-as-a-tool-for-documentation-creation)).
