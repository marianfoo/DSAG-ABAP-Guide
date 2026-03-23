---
layout: page
title: Architekturkonzepte
permalink: /clean-core/architectural-concepts/
parent: Clean Core
nav_order: 4
---

{: .no_toc}
# Architekturkonzepte

1. TOC
{:toc}


## Einstieg

This section looks at the possible architectures in the Clean Core range, learning about on-stack and side-by-side and how you can implement them in your architecture. Extensibility and its implementation is the key component for your business to achieve Clean Core. Extensibility describes all customer extensions in a SAP standard system as well as partner add-ons.


## Szenarien
Basically, you have the option of expanding your system via on-stack and/or side-by-side extensibility. Here you will find a schematic representation of the possibilities. 

![Extensibility Szenarien]({{ site.baseurl }}/clean-core/img/image-08.png)

Extensibility Szenarien
{: .img-caption}


### On-Stack

On the left you will find On-Stack Extensibility, divided into Pro Code and Low Code. In the Pro Code area you will find the classic ABAP Cloud development with the Clean Core level concept, the use of shared APIs and the extension of objects (C0 objects). You can find more about ABAP Cloud in the corresponding section of Clean Core. 

In the low code area there is primarily key user extensibility, these are some Fiori applications with which you can expand the system. The most common scenarios in this area are

* Field Extension - Create new Z fields from database to UI via application.
* User interface customization - Customize Fiori applications, rename elements or display the new Z fields. Create variants and make them available to your specialist departments.
* Own logic - Implement your own BADIs and extend the process with your own checks.
* Own Core Data Services - Create your own Core Data Services based on the shared views and make them available to the outside world as APIs.
* uvm.

The apps are primarily intended for your key users as they enable simple changes to the system. The changes are made productive via standard change management (e.g. CTS).

### Side-by-Side

On the right you will find Side-by-Side Extensibility, which is about decoupled development outside the core system. This example is the Business Technology Platform, BTP for short. Here you will find various tools and systems with which you can create applications to extend the system.

* SAP BTP ABAP Environment - Develop extensions based on ABAP in the Cloud.
* SAP Build Code - Develop extensions based on Java or JavaScript.

In addition to the Pro Code solutions, you can also find Low Code and No Code solutions from the SAP build portfolio here. Here is a brief overview of the common tools and their use.

* SAP Build Apps - Create Fiori and mobile apps here using drag'n drop and simple scripts. The apps will then be made available in the BTP.
* SAP Build Process Automation - If you need a workflow or automation, you can build it with Process Automation and connect both SAP and non-SAP systems.
* SAP Build Work Zone - If you need centralized access to all SAP applications, whether on-stack or side-by-side, then the Work Zone can be an alternative. In addition to the Standard Edition, there is also an Advanced Edition with collaborative functions.


## Strategie

Before you start working, you should think about the expansion strategy. That means which tools and environments do you want to use for the extensions. 

### Modelle
There are some company factors to consider:

* Platform - Which expansion model do you want to use in your company (CAP or RAP). Related to this, how many developers do you need in the areas.
* Know-how - Is the appropriate know-how for the environment available or does it have to be built up first? In the ABAP range these would be CDS, RAP and Fiori Elements. In the area of ​​CAP JavaScript or Java, Build Pipelines, Git and BTP.


The following detailed graphic shows the different scenarios.


![Tools and strategy]({{ site.baseurl }}/clean-core/img/image-09.png)

Tools and strategy
{: .img-caption}

The entire SAP product portfolio is available to you, although each product requires its own skills and requirements. We therefore strongly recommend developing a strategy.

### Kopplung

Coupling is about the different requirements that an application brings with it. Should the application be developed on-premise or side-by-side? In this [Artikel](https://software-heroes.com/blog/abap-cloud-clean-core-szenarien) you will find various criteria as to when which environment is worthwhile. Basically, you should understand that you can also achieve Clean Core on-premise on your own system and do not necessarily need side-by-side development.

The two coupling scenarios are:

* Tightly coupled - The application should be built on-premise.
* Loosely coupled - The application can also be developed in the Cloud.

## Make the Core clean
If you have taken the brownfield approach and migrated your system to S/4HANA and choose Clean Core, it is recommended to migrate your applications gradually. Frequently used applications are particularly worthwhile in order to quickly benefit from SAP Fiori. This allows you to examine application by application which ones you can modernize or perhaps even decommission because they are no longer needed. An initial overview with an inventory therefore makes sense.