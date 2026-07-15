---
layout: page
title: Challenges
permalink: /open-source/challenges/
parent: Open Source
nav_order: 6
---

# Challenges
{: .no_toc}

1. TOC
{:toc}

ABAP faces several challenges when it comes to establishing itself in the open-source ecosystem due to a number of underlying conditions.

## Source Code Stored in the Database

The source code of source-based development objects is stored in the `REPOSRC` table of the SAP system's primary database. Metadata and non-source-based development objects are represented in a relational model within the database. From the perspective of other programming languages, this is unusual. Standard tooling used in open-source development expects source code to be managed in a file system using files and folders and is therefore initially incompatible with ABAP development.

{: .solution }
[abapGit](https://abapgit.org/) serializes database content and relational development objects into files and folders. Through deserialization, it can also return those files and folders to the SAP system’s object model. abapGit therefore bridges the two formats and enables the use of file-system-based tools. The [Git-Enabled Change and Transport System (gCTS)](https://help.sap.com/docs/ABAP_PLATFORM_NEW/4a368c163b08418890a406d413933ba7/f319b168e87e42149e25e13c08d002b9.html?locale=en-US) provides an alternative or complementary approach. See [Version Management]({{ site.baseurl }}/version-management).

## Unsuitable Built-In Version Management

A version control system is the central cornerstone of open-source development. It enables the distribution and exchange of source code and thus collaborative work on a project without requiring a central development system. The version control functionality built into the ABAP platform is not suitable in this context. Its primary focus is the audit-proof tracking of changes rather than the exchange of source code beyond the boundaries of the system. The transport system, with its proprietary binary exchange format, is likewise unsuitable.

{: .solution }
With [abapGit](https://abapgit.org/), development objects can be versioned and exchanged across ABAP runtime environments using the de facto standard version-control system [Git](https://git-scm.com/). abapGit [supports a wide range of object types](https://docs.abapgit.org/user-guide/reference/supported.html). In a corporate environment, it can complement built-in version management and traditional transport systems and can be introduced incrementally by team or project. See [Version Management]({{ site.baseurl }}/version-management).

## Proprietary Programming Language

ABAP is proprietary. There is no freely available specification of the programming language. This limits the development of tooling required in the open-source ecosystem. Without a language specification and without a compiler available outside an SAP system, it is difficult to integrate continuous integration measures into the development process. SAP systems are also difficult to incorporate into such processes because, from a licensing perspective, allowing unknown users to access a system is difficult to realize. However, this is precisely the goal of open-source development: to enable anyone to participate in the development of the software.

{: .solution }
Despite the limited information available from SAP, developers in the open-source community have created their own tooling. [abaplint](https://abaplint.org/) deserves special mention: it can check syntax, code style, and CI rules without an SAP system. It can even execute ABAP code by transpiling it to JavaScript, allowing unit tests to run in a pull-request-based CI environment without access to an SAP system.  
You can use the [ABAP Feature Matrix](https://software-heroes.com/en/abap-feature-matrix) to find out which features are available in which release. This is important in the open source context because releases that are lower than the release of the system being developed on are often required to be supported. abaplint also offers the option of automatically checking for compatibility with lower releases or even carrying out automatic downports. This means that different systems do not have to be maintained.

## Monolithic Architecture

Applications developed traditionally in ABAP are often not self-contained and are not equipped with clearly defined interfaces. Particularly in custom enhancements, insufficient attention is often paid to the software components in which external objects reside or to the dependencies of the organization's own objects and packages. Open-source projects should minimize their dependencies and document existing dependencies, including their versions, so that as many users as possible can adopt them. This must be taken into account when developing open-source projects.
From a technological perspective, ABAP is not inherently unsuitable for developing encapsulated, reusable components. However, neither is this approach directly enforced by the technology, and in day-to-day development it is often not required to fulfill business requirements. As a result, additional consideration of this topic may be necessary.
When using such reusable components, another challenge arises: issues within the component can directly affect all consuming applications, since these applications do not each use their own installation of the component but instead rely on the centrally installed version within the system. The same issue also arises when delivering your own software, whether open source or proprietary, because the target system must contain the component in the appropriate version.

For architectural considerations and support for multiple releases and products, see use case [Open source software development]({{ site.baseurl }}/open-source/developing-open-source-software/). For solutions regarding installing multiple versions of a component in the system, see [Delivery of open source dependencies in your own products]({{ site.baseurl }}/open-source/using-open-source-software/#delivery-of-open-source-dependencies-in-your-own-products).
{: .solution }

## Namespaces

The namespace concept is generally unsuitable for cross-company participation in development projects because of the risk of naming conflicts within the customer namespace. In addition, dependencies cannot be installed multiple times in different required versions within the same system.

To solve the problem, there is tooling in the form of automatic name conflict checking on [dotabap.org](https://dotabap.org), automatic copying of dependencies to other namespaces / prefixes with abaplint and the ABAP open source namespaces. For details see [Namespaces]({{ site.baseurl }}/open-source/developing-open-source-software/#namespaces) and [Delivery of open source dependencies in your own products]({{ site.baseurl }}/open-source/using-open-source-software/#delivery-of-open-source-dependencies-in-your-own-products).
{: .solution }
