---
layout: page
title: Architecture and structuring in the ABAP development
permalink: /abap/architecture_and_design/
has_children: true
parent: Moderne ABAP Entwicklung
nav_order: 1
---

{: .no_toc}
# Architecture and structuring in ABAP development

1. Toc
{:toc}

## Structural challenges in SAP applications

Many SAP ERP systems contain numerous and extensive in-house developments that were created and continually expanded over the life of the system. The more complex a system is, the more important it is that the applications and components it contains are organized in a well-defined structure that follows common software architecture principles.
In SAP ERP systems, this is not always the case in the area of ​​in-house developments. This has, among other things, the following reasons:

- **Entwicklungsklassen**  
The developments were started when the SAP package concept did not yet exist and its predecessors, the development classes, were used. These only enabled a flat structure and therefore the structure followed very rough criteria, e.g. per development team or module. This principle was retained and continued after the introduction of the package concept.

- **Wissen**  
The knowledge about the package concept and the application of software architecture principles is often not sufficiently available in the ABAP environment.

- **Changes and extensions to existing software**
Many developments concern the further development of existing functionalities. A redesign and the associated package structuring is rarely planned and carried out.

- **Time and deadline pressure**  
Ultimately, most developments take place under time pressure. The question of how an application can be meaningfully structured in packages is often not asked or neglected because the focus is on delivering the functionality.  

As a result of the structural deficits in in-house developments resulting from the reasons mentioned, the following problems can arise:

- **Lack of transparency and comprehensibility:**  
The tasks and their responsibilities of individual artifacts as well as their dependencies on each other are not clear from the structure of the packages.

- **High adjustment effort**  
Changes to existing software require a lot of effort caused by complex analysis, finding the artifacts that need to be changed and implementing the change correctly. Since the correctness of changes is difficult to predict, high testing and error correction costs arise.

- **Side effects and errors when changing existing applications:**
Changes can lead to unforeseeable side effects in production and thus to increased development and error correction efforts.

- **Problems with distribution and import of changes**
Problems can arise with transports if not all necessary objects were transported correctly or not all dependencies were taken into account (e.g. RC8).

## Architecture and structure as the foundation and framework of a good SAP application

The complexity of software is often underestimated and only those who think about good software architecture right from the start and continuously improve the application technically and structurally will be less confronted with the problems described above.  
Good and modern software development begins first and foremost with consideration of what functions and responsibilities an application to be created should have, how the responsibilities are regulated and how this is ultimately reflected in the package structure.  
With the SAP package concept you have the tool to translate these considerations into visible structures and thus lay the foundations for a clean and future-proof application architecture.

## Structuring software in packages

### The SAP package concept and the posting of packages

As is common in other programming languages ​​such as Java, the SAP has also implemented a package concept in the ABAP, with which it is possible to structure the software at different levels. Before the availability of the package concept, development objects were organized into development classes as a flat structure.  
The use of the package concept in in-house developments results in significantly expanded possibilities for software structuring, which, although on the face of it do not have a direct effect on the functionality itself, bring significant advantages with them at the latest when it comes to servicing, maintaining and expanding the in-house development. Since SAP provides detailed and easy-to-understand documentation of the package concept, we will not go into the package concept in detail here, but rather give a practical overview and recommendations on how to proceed when creating in-house developments, after referred to as "software", in order to use packages in ABAP sensibly and beneficially.  
[SAP Documentation ABAP Workbench - Package Builder](https://help.sap.com/docs/ABAP_PLATFORM_NEW/bd833c8355f34e96a6e83096b38bf192/af40bd38652c8c42e10000009b38f8cf.html?locale=de-DE).


{: .recommendation}
>- ***Use the package concept:***
>- Turn on packet checking on your SAP systems.
>- Create main packages for your own developments that are based on architectural requirements (single responsibility).
>- Enable packet encapsulation per packet.
>- Group and structure the package with sub-packages based on responsibilities rather than object type.
>- Do regular package checks during the development process to identify dependencies.
>- For non-visible objects, check alternatives (e.g. comparable object with visibility from another package, own definition in the package, ...).
>- Include desired dependencies in the declaration of use.
>- Avoid creating very large packages or "bundle packages" that bundle numerous independent functions.
>- Train your developers on package definition, software structuring and maintenance of package interfaces and usage declarations  

## Package structures and hierarchies  

We recommend designing the packages according to functional aspects. You create independent solutions that should also be able to be transported independently using main packages. The various functional aspects of this solution, such as business logic, usable interfaces, user interfaces and central elements of the solution that are shared by the other components within the main package, are structured in sub-packages (development packages). In the classic environment, the main package is the transportable unit.  
In the ABAP-Cloud context, a technically required structure package can then be created via this main package, which is then used for the software component. In the Cloud context, the transportable unit is represented by the software component.  
Structuring based on organizational, responsibility or project structures is not recommended, as these attributes change over time and are only partially dependent on functionality. These attributes are better contained in documentation that is part of the main package.  

## Dependency control

Enabling package encapsulation enables control over dependencies in packages.  
In the package interfaces you define the visibility of objects when package encapsulation is switched on and you use the usage declaration to document dependencies on other packages via their package interfaces.
Package inspection is the tool to make visible and monitor the use of invisible objects or missing usage declarations.  
How you specifically use these elements is explained in the [detailed section]({{ site.baseurl }}/abap/package_details/#paketpr%C3%BCfung) on the package concept. You can also find information about this in the SAP documentation.

## Advantages and added value by using the package concept

### Clearly declared dependencies

By using the package concept, dependencies on functionalities become transparent. Either a dependency is listed in the usage declaration, which means it is a deliberately defined dependency, or the dependency is visible through an error message in the package check, in the case of invisible objects or if a usage declaration is missing. The information obtained from this can be used for documentation and description. Before a package is imported into a system, it can be checked whether the system meets the requirements to import the package without errors or whether other packages are required.

### Better overview and explainability

In complex and extensive developments, structuring helps to find relevant objects more quickly. The structure can already be considered part of the documentation. If corrections, extensions or additions to an in-house development are required, a good package structure helps the developer to find his way around the application more easily and to implement extensions more quickly.  

If software is to be transported across systems, we recommend creating the transports at the main package level. The main package represents a functioning business function or an extension of a standard function or a defined area.  
If all objects of a main package (structured in sub-packages) are included in a transport and the declared requirements/dependencies are met in the target system, the transport can be transported and imported across system lines. Import errors (RC8) should then generally no longer occur.

### Flexibility

When a software component is well structured, additions, changes, extensions, and corrections can be made more easily than when an application consists of loosely assembled objects in a large, unorganized package that contains other objects for other functions. This means that good structuring also results in increased flexibility. In particular, if functionalities grow over the course of the life cycle and the scope increases, it may be necessary to adapt the structure and, if necessary, to outsource functionalities into central or generally available packages in order to achieve reusability or, in the opposite case, to combine several smaller applications into a main package.

### Future viability

In addition to the obvious advantages, creating software in well-structured packages also includes other advantages that do not take effect immediately, but can become relevant as part of the software life cycle.  
If the in-house developments in the system are already organized into packages, important requirements have already been met in order to use modern version management systems such as abapGit or gCTS, which require packages. This means that transports using Git-based methods into other systems or even into the Cloud are possible, see chapter [Version Management]({{ site.baseurl }}/application-lifecycle-management/version-management/).
If the package concept with an explanation of the usage relationships has already been practiced in the company and there is already awareness of usable objects, good conditions are created for understanding and applying the concepts in ABAP Cloud with the software components.

## Measures to implement the package concept in development

### Definition and implementation of the package strategy

The above-mentioned advantages only arise if the package concept is implemented comprehensively and consistently within the company in the form of a package strategy. It is therefore important that you clearly define your package strategy and determine how packages are created and documented.  
Make sure that the people responsible for development understand and can implement the specifications for the package concept. It is therefore important to adequately train the developers regarding the package concept to be implemented and to check compliance and proper implementation. Particularly when external developers are used, it is important to ensure that appropriate onboarding takes place. The task of defining the packages and their structuring, as well as their classification in the package landscape, should be carried out by the software architect or software development manager such as the SAP Lead Developer in order to ensure consistency across packages.

### Avoiding large/unspecific collector packs

We recommend not allowing the creation of large collector packages (e.g. based on module level), as this can lead to problems with clarity and unwanted dependencies and violates the principle of single responsibility.  
There is a great risk that, for various reasons, numerous different classes and functions end up in such packages instead of solid architectural considerations, which can counteract the effort to maintain an orderly system architecture.  

However, it can definitely make sense to create small, well-defined and domain-specific help packages that provide basic and often needed help functions centrally.

## Further questions when implementing the package concept

In addition to the recommendations for the package concept described here, there are further questions that cannot be discussed further here, as a detailed treatment would exceed the scope of the guide. However, these should be taken into account and defined in the guidelines and manuals. These are the following aspects:  

- Avoiding static dependencies - Packages should be defined in such a way that they are independent of other packages
- Definition of the procedure when dependencies are unavoidable or desirable. There are various possible solutions here, such as:
  - by defining BAdIs - which are then implemented locally and used to establish the package connection
  - Calling a function from another package via dynamic function module calls
- Size of packages - Architectural boundaries - Boundaries - Costs (Clean Architecture)
- Package refactoring - Splitting - Combination of individual packages - Continuous package maintenance for changes and extensions

## The package concept in ABAP Cloud - software components

In the context of ABAP Cloud, the package concept described here is no longer applicable 1:1, as package interfaces are no longer supported in the Cloud.  
With the introduction of the ABAP environment for development on the Cloud and with ABAP Cloud, the “software component” (SWC) property, which has been around for a long time but is generally not used for structuring, is becoming increasingly important in the structuring of ABAP software. When developed with ABAP Cloud, the software component becomes a central part of the software structure and complements the package concept.
The packages below the software component are used to structure the various components of an application.
The package interfaces are no longer required because the usage relationships are no longer maintained at the package level. But the principles are comparable. The use of the software components is controlled via the release contracts (C1). This means that objects in software components can be used system-wide as long as they are provided with a release contract.  
If only software components defined by objects are to be used, this can be done in so-called software component relationships (SWC). The software components declared here receive permission to use all SWC objects. A restriction to specific objects of your own SWC is not possible. Detailed information can be found in the [SAP Documentation for SWC](https://help.sap.com/docs/abap-cloud/abap-development-tools-user-guide/software-component?locale=en-US)  

Even if some elements of the package concept are no longer found in the Cloud, the implementation and application of the concepts described above still makes sense in current on-premise and private Cloud SAP systems because it structures developments, declares dependencies and visibility and thus helps to create well-structured applications.  

## From architecture to design

After the statements mentioned here have created the prerequisites for a good architecture, which is reflected in the package structure, the application architecture must now be defined/designed in the specific form of classes in the individual sub-packages. You can find the information on this in section: [Design and design of modern SAP applications]({{ site.baseurl }}/abap/oo-design/).
