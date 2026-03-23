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

In addition to methods, function blocks and reports that can contain documentation in the source code, there are other development objects in the ABAP system that do not have a source code and therefore must be documented in another way. Examples of this are:

* DDIC objects
* Transactions

Since the workbench documentation is also connected to transportation, it is available in all individual systems in a system landscape. Furthermore, this documentation can be viewed by all users and is automatically integrated into the user interface for reports from the ABAP system. Another advantage can be that the documentation can be kept in multiple languages. On SAP systems with SAP_BASIS >= 7.40, ABAP doc comments can be used in the source code. This can be used as an alternative to documentation in the ABAP workbench. However, the full functionality of ABAP doc comments can currently only be exploited with the ABAP development tools for Eclipse. When using Core Data Services to define DDIC objects, significantly more development objects can be documented in the source code and the need for external documentation is eliminated.

Starting with SAP NetWeaver 7.50, the ABAP doc comments of classes and interfaces can be exported as HTML files. As of ABAP Platform 7.55, the SAP is expanding its repertoire to include another technology for documenting ABAP development objects. The Knowledge Transfer Document focuses on the new object types that primarily come from the ABAP RESTful Application Programming Model (RAP) context. This includes, among other things: CDS views, behavior definitions, service definitions, service bindings, annotation definitions and packages.

## Short texts

Short texts can be created for many objects, such as a description of a data element or a method.

## Knowledge Transfer Documents (KTD)

The Knowledge Transfer Document has been available since ABAP Platform 7.55. KTD allows documentation to be created individually for each element of an object. It is based on Markdown language with simple text formatting syntax.

KTD must be in the same package as the development object. It is not automatically transported with the development object, but when the development object is deleted, the associated KTD is also deleted.

{: .recommendation } 
> We recommend using the documentation function of the ABAP workbench for all development objects and regardless of the source code. The documentation function should be used in the following order, depending on which type of documentation object is available for which object: 1. Knowledge Transfer Documents 2. abapDoc 3. Short texts Only the current status should be documented, if necessary enriched with short references to the change documentation (transport documentation, defect numbers).

# Documentation in source code

## Documentation language

Nowadays, development teams predominantly work together internationally. Even if you are currently developing purely in German, your project can be internationalized over time. The effort that then arises from coordination problems or even subsequent translation is disproportionate to the perhaps greater effort involved in English documentation. It has also been shown that the readability of source code and comments is increased by English-language comments. Because the ABAP commands themselves are English and structured in the style of sentences. The reader of the source code does not have to constantly change the language when the documentation is in English.

{: .recommendation }
> It should be clarified within the company what the comment language is. The recommendation must be commented on in English.

## Documentation of changes

From the time a program goes live, care should be taken to ensure that changes to programs are adequately documented. The right amount is essential here: A complete version history of all changes and commented-out source code reduce the readability of the source code. Despite this disadvantage, some development teams deliberately document all changes in the source code to simplify troubleshooting on production or test systems where version history is not available.

{: .important }
> Subsequent changes to the source code should only be documented directly in the source code in exceptional cases.

## Comments in the source code

Comments in the source code are intended to make it easier for developers to understand the source code, unless this can be achieved through clever design of the source code alone (modularization, choice of names for methods and variables).

Comments are intended for other developers and, as time passes, also for the original developer.

Star comments should only be used in the program header or for temporarily commenting out old source code.

For all other comments, SAP recommends using inline comments. These should precede the source code they document and be indented in the same way as that source code. The latter is also carried out correctly by Pretty Printer (only) for inline comments.

{: .recommendation }
> You should answer the question “Why” something was programmed and not “What”. The latter emerges from the source code anyway, while the motives are often not clearly recognizable. But they in particular help significantly with understanding. The principle applies: as little comment as possible, as much comment as necessary.

OTHER SOURCES

1. Horst Keller, Wolf Hagen Thümmel: ABAP programming guidelines. SAP Press, 2009. ISBN: 978-3-8362-1286-1
2. Klaus Haeuptle, Florian Hoffmann, Rodrigo Jordão, Michel Martin, Anagha Ravinarayan, Kai Westerholz: Clean ABAP. SAP PRESS, 2022. ISBN: 978-3-8362-8659-6

## ABAP Doc

ABAP Doc makes it possible to document classes, interfaces and function blocks. The comments consist of one or more commented lines.  
- ABAP Doc begins with the prefix `"!.`.  
- ABAP Doc can be used to document basic information about the class, method or interface directly in the source code. Furthermore, the parameters of a method can be provided with detailed documentation via ABAP Doc. These ABAP Doc comments are placed directly before declarative statements.  
- In ABAP Doc, HTML tags can also be used for formatting, which increases and improves the readability and structure of the documentation.  
- With the recommended use of ADT, the creation of ABAP Doc is very easy and efficient by using Quickfix [DSAG AG ADT Guide: What are ABAP Doc](https://1dsag.github.io/ADT-Leitfaden/working-with-adt/features/abap-doc/#was-sind-abap-doc)

The advantage of using ABAP Doc is that these comments are displayed in the following functions of the ADT, providing the developer with valuable information directly when creating the code.

* ABAP Element Info view
* Element Information Popup
* Code completion list.

And these ABAP Doc comments can be extracted from ADT into an HTML file and thus used for further use outside of the code, e.g. on internal pages. If the code and the existing ABAP Doc documentation are maintained at the same time and ABAP Doc is extracted after each change, the external documentation is also up to date without any additional effort.
If the ABAP Doc documentation is created in a structured manner, it can also be used with supporting generative AI to create further documentation (see [Chapter Artificial Intelligence]({{ site.baseurl }}/artificial-intelligence/#ai-as-a-tool-for-documentation-creation)).
