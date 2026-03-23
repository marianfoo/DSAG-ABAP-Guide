---
layout: page
title: Version Management
permalink: /application-lifecycle-management/version-management/
parent: ALM
nav_order: 3
---

{: .no_toc}
# Version management in SAP

1. TOC
{:toc}

The documents that must be retained in accordance with HGB, AO and GoBS also include the repository objects in ABAP. For a long time, this was achieved through the integrated version management within the ABAP workbench (SE80). In recent years, however, ABAP has developed further, be it through the use of an external development environment (ABAP Development Tools), the use of Git version management or the development of additional repository objects that cannot be developed in the ABAP workbench. Therefore, the central question that arises for every ABAP developer is:

* Which version management should I use and when?

This chapter is therefore intended to provide an overview and comparison of version management solutions within the SAP universe for ABAP developers.

## Git Basics

Git is a distributed versioning system that is available as open source. It was developed in 2005 by Linux inventor Linus Torvalds. In the programming area it is used to:

* monitor your own changes
* Undo changes
* Make changes available to others
* Obtain updates from others

This results in the following advantages:

* it can be developed at the same time, e.g. B. for various features
* Versioning prevents work that has already been done from being lost or overwritten
* If necessary, you can go back to previous versions or work on different versions simultaneously

### Key Terms

* **Repository**: All files, including previous versions, are located in a repository or repo. This means that all changes that have been transferred from a file to the repo are always available and it can be traced who made which changes and when.
* **Branches**: When using Git, branches are used to create a separate branch of work. This can then also be seen as a new context in which work takes place. For example, a feature can be programmed in its own branch, which is incorporated back into the main branch upon completion and after testing.
* **Versioning**: During versioning, all changes made are logged in the Git. Using “Commit” the changes can be added to the repository, and a new version of the file(s) will then be in the repo. Different versions can then be compared, changes can be undone or a previous version can be reverted to.

## Use of Git based solutions in ABAP development

In many programming languages, management of program code in a Git repository is standard. Through the efforts of Lars Hvam Petersen, who made it possible to bring ABAP code into a Git repository through his free open source solution abapGit, Git-based solutions are taking on an increasingly important role in the ABAP world. The use of Git-based solutions in ABAP development has the following technological advantages:

* **Standard versioning features**: By using Git, standard features can be used, such as rollback not just for one object, but for all objects at the same time.
* **Collaboration of multiple developers on different requirements at the same time**: With the help of Git it is possible for multiple developers to work on different requirements at the same time using branches.
* **Enabling external tools**: It is now possible to not only use SAP products for the development workflow, but you can also use external tools to check your code for example. In addition, CI pipelines can be built, which is not possible with the standard transport mechanism.
* **Versioning**: Previously it was only possible to know a version of an object. It is now possible to version a series of objects using tags. This has the advantage that the application can now have a release character.
* **Code is central**: The code is in a central location and all changes to the application are brought there. In addition to the ABAP code, other components of the application such as Fiori or .NET developments can also be saved in the Git repository. The documentation can also be saved in the Git.

In addition to the technological advantages, there are also organizational advantages

* **Git is standard solution**: It is easier to get other people excited about SAP development if they already know tools or technologies from other programming languages. Git is the standard solution for other programming languages ​​and no new know-how needs to be developed. Especially students who already know Git can then become more enthusiastic about ABAP.
* **Uniform format for programming languages**: Not only SAP developments can be stored in the Git repository, but other development teams can also centrally deposit their code there.
* **Format**: The format can be read by anyone. It is not encrypted and all changes can be traced. This means that an auditor can also see all changes, when they were made and by whom.

## Version control systems in the SAP environment

The following version control systems exist in the SAP environment:

### Server-based Version Management

Server-based version management is active for all editable objects in the ABAP Workbench.
Version management can be done via

* SE80 - Object Navigator
* SE09 - Transport Organizer
* the display and maintenance transactions for repository objects

be called.

The corresponding objects are versioned every time the transport is released.

### Local version management in ABAP Development Tools

The ABAP Development Tools, based on the Eclipse IDE, offers built-in version management for development resources, which can be executed using the ABAP Compare Editor and offers extensive comparison options:

* **client-based local versioning:** - The standard feature under Eclipse provides standard versioning. Every time an object, such as a ABAP class, is edited and saved, Eclipse saves the version according to your personal preferences. This is useful if you want to track changes that occurred before a transport release.

* **Server-based revision history:** - This is equivalent to local version management and displays versions based on the current status and released transports. Compared to the GUI-based version, changes here, especially in classes, are much clearer and easier to understand. It is also possible to use other systems that are integrated into Eclipse as ABAP projects for version comparison (e.g. central development system line and Q system of the production line). No RFC connections between the systems are required; the comparison takes place locally.

Details can be found in [ADT guidelines from DSAG](https://1dsag.github.io/ADT-Leitfaden/working-with-adt/features/vcs-and-compare/#versionsverwaltung-und-vergleichen/)

### abapGit

abapGit is a Git client developed in ABAP. It was developed by Lars Hvam Petersen and is an open source project. With abapGit, developers have the opportunity to connect a Git version control to the SAP application server and create ABAP development objects in a Git repository.

### gCTS

In contrast to abapGit, gCTS (Git-enabled Change and Transport System) is an extension to CTS provided by SAP. It supports the integration of Git into the existing CTS to enable modern version control functions.

### Version management in SAP BAS

With SAP Business Application Studio, companies have a tool for developing their applications and extensions related to SAP solutions. The provider provides the development environment in the form of a Cloud-based service. Integration with Git is planned for easier version management. However, versioning is also possible with other systems.

## Comparison of the different version control systems

### SAP system and availability

In the following SAP systems, the version control system is available.

| **Tool**                                         | **SAP-System**            | **System availability**   |
|:-------------------------------------------------|:--------------------------|:--------------------------|
| **SE80 (Local version management)**             | SAP OnPrem                | Since at least 2007       |
| **ABAP Development Tools (Version Management)**  | SAP OnPrem/SAP Cloud      | Since 2012                |
| **abapGit to SAP GUI**                           | SAP OnPrem                | SAP BASIS version 702     |
| **abapGit to ADT**                               | SAP Cloud/SAP OnPre       | Since 2018                |
| **abapGit in the Cloud**                         | SAP Cloud                 | Since 2018                |
| **gCTS in the Cloud**                            | SAP Cloud                 | S/4HANA EM 1909 FPS00     |
| **gCTS OnPrem**                                  | SAP OnPrem                | S/4HANA EM 1909 FPS00     |
| **SAP BAS**                                      | SAP Cloud/SAP OnPrem      | Since 2020                |

### Functional Scope

The scope of functions of the respective version management can be found in the following documentation

| **Tool**                                         | **Functional Scope**          |
|:-------------------------------------------------|:------------------------------|
| **SE80 (Local version management)**             | [SAP Version Management](https://help.sap.com/docs/SAP_NETWEAVER_AS_ABAP_752/2b28ffa716c24348903f8ffbfeb81df8/e52a2c8d53f8400bb8a309cffe417275.html)|
| **ABAP Development Tools (Version Management)**  | [ADT User Guide ](https://help.sap.com/docs/abap-cloud/abap-development-tools-user-guide/comparing-source-code)              |
| **abapGit to SAP GUI**                           | [abapGit User Guide](https://docs.abapgit.org/user-guide/)                                                                   |
| **abapGit to ADT**                               | [BTP Working with abapgit](https://help.sap.com/docs/btp/sap-business-technology-platform/working-with-abapgit)              |
| **abapGit in the Cloud**                         | [abapGit](https://help.sap.com/docs/btp/sap-business-technology-platform/working-with-abapgit)                               |
| **gCTS in the Cloud**                            | [gCTS](https://help.sap.com/docs/ABAP_PLATFORM_NEW/4a368c163b08418890a406d413933ba7/f319b168e87e42149e25e13c08d002b9.html)   |
| **gCTS OnPrem**                                  | [gCTS](https://help.sap.com/docs/ABAP_PLATFORM_NEW/4a368c163b08418890a406d413933ba7/f319b168e87e42149e25e13c08d002b9.html)   |
| **SAP BAS**                                      | [Documentation still missing]                                |

### Version Scope

Version management includes the following version scope

| **Tool**                                          | **Version Scope**                          |
|:--------------------------------------------------|:-------------------------------------------|
| **SE80 (Local version management)**              | Each individual object                     |
| **ABAP Development Tools (Version Management)**   | Each individual object                     |
| **abapGit to SAP GUI**                            | At the package level                             |
| **abapGit to ADT**                                | At the package level                             |
| **abapGit in the Cloud**                          |                                                                                                                                                                                |
| **gCTS in the Cloud**                             | At the transport layer level                  |
| **gCTS OnPrem**                                   | At the transport layer level                  |
| **SAP BAS**                                       |                                                                                                                                                                                |

### Trigger Point

Version management is triggered as follows.

| **Tool**                                          | **Trigger Point**                          |
|:--------------------------------------------------|:-------------------------------------------|
| **SE80 (Local version management)**              | With every transport release                |
| **ABAP Development Tools (Version Management)**   | After each save/activation                 |
| **abapGit to SAP GUI**                            | When triggered manually or automatically in the background                  |
| **abapGit to ADT**                                | When triggered manually                   |
| **abapGit in the Cloud**                          | When triggered manually                   |
| **gCTS in the Cloud**                             | Upon release for transport                      |
| **gCTS OnPrem**                                   | Upon release for transport                      |
| **SAP BAS**                                       | When triggered manually                   |

### Applications

The following applications in addition to a SAP system are required to use the version management.

|                                                                                                                                                                                                            | **Applications**                                              |
|---------------------------------------------------|---------------------------                                      |
| **SE80 (Local version management)**              | No additional system necessary                                    |
| **ABAP Development Tools (Version Management)**   | ABAP Development Tools                                         |
| **abapGit to SAP GUI**                            | Repository System as well as abapGit in the SAP system                   |
| **abapGit to ADT**                                | Repository System as well as abapGit in the SAP system and plugin in ADT |
| **abapGit in the Cloud**                          | Repository System as well as abapGit in the SAP system and plugin in ADT |
| **gCTS in the Cloud**                             | Repository system and gCTS configuration                        |
| **gCTS OnPrem**                                   | Repository system and gCTS configuration                        |
| **SAP BAS**                                       | Repository system and access to SAP BAS (licenses)              |

## Deployment Scenarios

### Widely Used 3-System Landscape

This deployment scenario involves pushing the code on the development system into a Git repository with a Git version control system.

![Illustration 3-system landscape]({{ site.baseurl }}/application-lifecycle-management/img/dsagleitfaden-normal.drawio.png)

### Software Supplier

This deployment scenario is used to exchange source code from a software supplier to its customer via a Git repository.
![Illustration software supplier]({{ site.baseurl }}/application-lifecycle-management/img/dsagleitfaden-softwarelieferant.drawio.png)

### Distribution in different system landscapes

This is about exchanging source code between your different system landscapes. This makes it possible to use the same source code and continue working without cross-transports.  
![Alt text]({{ site.baseurl }}/application-lifecycle-management/img/dsagleitfaden-verteilung.drawio.png)

### Recovery

This scenario describes the possibility that a previous state can be reclaimed from the Git repository.
It is not necessary to retrieve each repository object individually, but rather an old version of an entire application.
![Alt text]({{ site.baseurl }}/application-lifecycle-management/img/dsagleitfaden-RECOVERY.drawio.png)

### Parallel Work

![Alt text]({{ site.baseurl }}/application-lifecycle-management/img/dsagleitfaden-parallel.drawio.png)

### Custom Code Migration

![Alt text]({{ site.baseurl }}/application-lifecycle-management/img/dsagleitfaden-customcode.drawio.png)

## Comparison of the development process with different version management

| SAP-Standard  | git-basiert  |
|:--------------|:-------------|
| Order must be created at the beginning | Commit is performed after the change |
| Distributing code - no control over changes in other systems | Central point of contact |
| Versioning of an application is not possible | Versioning of an entire application possible via standard functionalities |
| Undoing changes to a transport is only possible manually with massive effort and limitations | Going back to the previous commit allows you to reset all changes via gCTS or abapgit |

## Approaching development processes ABAP and non-ABAP via git-based tools

SAP developers find themselves caught between traditional stability and the need for faster, more flexible development processes. DevOps practices have already been successfully implemented in many other IT departments, while the SAP team is still struggling with longer release cycles and more complex transport mechanisms. DevOps is a combination of “Development” and “Operations” and aims to interlink development and operational processes so that software is delivered faster, more reliably and with higher quality. By using version management, an agile and efficient development environment can also be created in the SAP world. 

## Integration with Other Components

SAP versioning is the starting point for working with ABAP code outside of a SAP system

### Azure Pipelines

Azure DevOps streamlines the deployment process by providing pipelines that you can run.
Source: 
https://community.sap.com/t5/technology-blog-posts-by-members/sap-change-management-with-azure-devops-transforming-enterprise-operations/ba-p/14130760

### Apache Jenkins

Jenkins is one of the standard tools for continuous integration. To easily apply Continuous Integration or Daily/Nightly Build components to a ABAP development system, the starting point can be version management.

Source:
https://github.com/SAP/jenkins-library
https://community.sap.com/t5/application-development-and-automation-blog-posts/continuous-integration-and-abap-jenkins-the-missing-link/ba-p/13489906

## Security Aspekte 

### Revisionssicherheit

By precisely and completely logging all changes, version management ensures revision security. This is particularly important to meet compliance requirements and when reviewing security incidents or audits.

### Backup and restore

Version management has mechanisms for regularly backing up data. In the event of data loss or corruption, previous versions of the data can be restored. This minimizes the risk of data loss and ensures the continuity of business processes.

### Access rights management

The use of external version management systems provides functions for controlling access rights. This allows administrators to determine who is allowed to access, edit or view which data. This prevents unauthorized access and maintains the confidentiality of the data.

### Change tracking

Every change is documented, including the time and who made it. This creates transparency and makes troubleshooting easier.

### Manipulationseinsatz

With the help of external version management systems, the content and the change history can be protected from manipulation using their cryptographic hashing algorithms.


## Risiken

* Slow release cycles: Months of development phases and manual testing cause delays.
* Complex transport mechanisms: The traditional SAP transport management is not optimized for CI/CD.
* Lack of automation: Testing, deployment and code reviews are often still manual and error-prone.
* Resistance to change: Many SAP teams work according to classic waterfall methods and are skeptical about agile processes.

## Recommendation


### Definition of requirements

Choosing the right version control depends on the specific requirements and development process of the respective project or company. Define your requirements and then decide which version management you want to use. 

### Use of additional tools

Modern development practices such as CI/CD can be used with the help of version management. Think about what your pipeline should look like

{: .note }
> [Git and SAP / Rheinwerk Verlag](https://www.rheinwerk-verlag.de/git-und-sap/?srsltid=AfmBOooMbM45uQOGPLDAiaKz5hHazrf45BIEVjmOIe8mz9HjpdHjgzZq)
