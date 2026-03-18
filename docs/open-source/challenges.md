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

ABAP has a particularly difficult time gaining a foothold in the open source environment due to certain conditions.

## Source code in the database

The source code of source code-based development objects is stored in the `REPOSRC` table of the primary database of the SAP system. Metadata and non-source code-based development objects are reflected in a relational model in the database. This is unusual from the perspective of other programming languages. Standard tooling used in open source development expects the source code to be managed in a file system using files and folders and is therefore initially incompatible with the ABAP development.

{: .solution }
[abapGit](https://abapgit.org/) allows you to serialize the database table contents and relational model into files and folders. In addition, files and folders can be returned to the SAP system model via deserialization. Thus, abapGit provides an interface between the formats and enabled the use of file system-based tools. Alternatively or in addition, another approach is available with the [Git-Enabled Change and Transport System (gCTS)](https://help.sap.com/docs/ABAP_PLATFORM_NEW/4a368c163b08418890a406d413933ba7/f319b168e87e42149e25e13c08d002b9.html?locale=en-US). So see [Version Management](ABAP-Leitfaden/version-management).

## Unsuitable Built-in Version Management

The central linchpin in open source development is the version management system. It enables the procurement and exchange of source code and thus collaborative work on the project without a central development system. The version management built into the ABAP platform is unsuitable in this context. Your focus is on the audit-proof tracking of changes, not on the exchange beyond the system. Transportation, with its proprietary binary exchange format, is also unsuitable.

{: .solution }
With [abapGit](https://abapgit.org/), development objects can be versioned and exchanged in all ABAP runtime environments with the defacto standard version management [git](https://git-scm.com/). A wide range of object types [supports](https://docs.abapgit.org/user-guide/reference/supported.html). In a corporate context, abapGit can be used in addition to the built-in version management and classic transport systems and can be rolled out piece by piece or per team/project. So see [Version Management](ABAP-Leitfaden/version-management).

## Proprietary programming language

ABAP is proprietary. There is no available programming language specification. This limits the development of tooling that is required in the open source environment. Because without a specification and without a compiler outside of a SAP system, it is difficult to integrate continuous integration measures into development. SAP systems are difficult to integrate into the process because it is difficult to license the use of a system by unknown users. In open source development, that is exactly the goal: to enable everyone to participate in the development of the software.

{: .solution }
Despite little information from SAP, developers in the open source community have made the effort to develop tooling. [abaplint](https://abaplint.org/) deserves special mention here. The tool is able to carry out syntactic correctness and various code style and CI checks - without any SAP system! Furthermore, it can even execute ABAP coding by transpiling it to Javascript. This means that unit tests can be carried out in a CI environment based on pull requests without having access to a SAP system.  
You can use the [ABAP Feature Matrix](https://software-heroes.com/en/abap-feature-matrix) to find out which features are available in which release. This is important in the open source context because releases that are lower than the release of the system being developed on are often required to be supported. abaplint also offers the option of automatically checking for compatibility with lower releases or even carrying out automatic downports. This means that different systems do not have to be maintained.

## Monolithic Architecture

Applications developed classically in ABAP are often not self-contained and do not have defined interfaces. Especially in customer-specific extensions, it is often not taken into account which software components contain third-party objects or what the dependencies of your own objects and packages look like. Open source projects should minimize their dependencies and document existing dependencies including versions so that as many people as possible can use them. This is particularly important to take into account when developing open source projects.
ABAP is technologically not categorically unsuitable for developing encapsulated reusable components. However, it is not directly enforced by the technology and is often not necessary in everyday development to implement requirements. Therefore, an examination of the topic may be necessary.
When using such reusable components, the issue arises that problems can directly affect all applications that use them, since they do not each use their own installation of the component but rather the central one installed in the system. The problem also arises when delivering your own software, open source or not, because the component must be available in the appropriate version in the target system.

For architectural considerations and support for multiple releases and products, see use case [Open source software development](/ABAP-Leitfaden/open-source/developing-open-source-software/). For solutions regarding installing multiple versions of a component in the system, see [Delivery of open source dependencies in your own products](/ABAP-Leitfaden/open-source/using-open-source-software/#auslieferung-von-open-source-abhängigkeiten-in-eigenen-produkten).
{: .solution }

## Namespaces

The namespace concept is generally unsuitable for cross-company participation in development projects without risking name conflicts in the customer namespace. Dependencies cannot be installed multiple times in the system in different required versions.

To solve the problem, there is tooling in the form of automatic name conflict checking on [dotabap.org](https://dotabap.org), automatic copying of dependencies to other namespaces / prefixes with abaplint and the ABAP open source namespaces. For details see [Namespaces](/ABAP-Leitfaden/open-source/developing-open-source-software/#namensräume) and [Delivery of open source dependencies in your own products](/ABAP-Leitfaden/open-source/using-open-source-software/#auslieferung-von-open-source-abhängigkeiten-in-eigenen-produkten).
{: .solution }
