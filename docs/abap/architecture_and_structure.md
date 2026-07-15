---
layout: page
title: Architecture and structuring in the ABAP development
permalink: /abap/architecture_and_design/
has_children: true
parent: Modern ABAP Development
nav_order: 1
---

{: .no_toc}
# Architecture and Structuring in ABAP Development

1. Toc
{:toc}

## Structural Challenges in SAP Applications

Many SAP ERP systems contain numerous and extensive in-house developments that have been created over the course of the system’s lifecycle and continuously expanded. The more complex a system is, the more important it is that the applications and components it contains are organized in a well-defined structure that follows common software architecture principles.
In SAP ERP systems, this is not always the case when it comes to in-house developments. This has, among other things, the following reasons:

- **Development classes**
      Development began before the SAP package concept existed, when its predecessor—development classes—was still in use. These classes only allowed for a flat structure, so the organization followed fairly broad criteria, such as by development team or module. This principle was retained and continued after the package concept was introduced.

- **Knowledge**
      Knowledge of the package concept and the application of software architecture principles is often lacking in the ABAP environment.

- **Modification and extension of existing software**
      Many developments involve the enhancement of existing features. A redesign and the associated restructuring of packages are rarely planned or carried out.

- **Time and deadline pressures**
    Ultimately, most development work is carried out under time pressure. The question of how an application can be structured effectively into packages is often not asked or is overlooked, as the priority is on delivering the functionality.  

As a result of the structural shortcomings in in-house development arising from the reasons mentioned above, the following problems may arise:

- **Lack of transparency and clarity**
    Neither the functions and responsibilities of individual artifacts nor their interdependencies are apparent from the structure of the packages.

- **Significant effort required for adaptation**
    Making changes to existing software is a time-consuming process, due to the extensive analysis required to identify the artifacts that need to be modified and to implement the changes correctly. Since it is difficult to predict whether changes will be correct, this results in significant testing and bug-fixing efforts.

- **Side effects and errors when modifying existing applications**
    Changes can lead to unforeseen side effects in production and, as a result, to increased development and debugging costs.

- **Problems with the distribution and import of changes**
    Problems may arise during transport if not all necessary objects are transported correctly or if not all dependencies have been taken into account (e.g. RC8).

## Architecture and Structure as the Foundation and Framework of a Good SAP Application

The complexity of software is often underestimated, and only those who give careful thought to good software architecture from the very beginning and continuously improve the application both technically and structurally will be less likely to face the issues described above.  
Good, modern software development begins first and foremost with considering what functions and responsibilities an application to be created should have, how responsibilities are organized, and how this ultimately reflects in the package structure.  
With the SAP package concept, you have the tool to translate these considerations into visible structures and thus lay the foundation for a clean and future-proof application architecture.

## Structuring Software into Packages

### The SAP Package Concept and the Role of Packages

As in other programming languages such as Java, ABAP provides a package concept that allows software to be structured at multiple levels. Before packages were introduced, development objects were organized in a flat structure using development classes.  
Applying the package concept to in-house developments opens up significantly expanded possibilities for software structuring. While these changes may not directly impact functionality at first glance, they offer clear advantages—at the latest—during the maintenance, support, and expansion of the in-house development. Since SAP provides detailed and easy-to-understand documentation of the package concept, we will not go into the package concept in detail here, but rather provide a practical overview and recommendations on how to proceed when creating in-house developments—hereinafter referred to as “software”—in order to use packages in ABAP in a meaningful and beneficial way.  
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

## Package Structures and Hierarchies  

We recommend organizing packages based on functional aspects. Use main packages to represent standalone solutions that are also intended to be transportable on their own. Structure the various functional aspects of this solution—such as business logic, available interfaces, user interfaces, and central elements of the solution that are shared by other components within the main package—into subpackages (development packages). In a traditional environment, the main package is the transportable unit.  
In the ABAP Cloud context, a technically required structure package can then be created via this main package, which is subsequently used for the software component. In the cloud context, the transportable unit is represented by the software component.  
Structuring based on organizational, responsibility, or project structures is not recommended, as these attributes change over time and are only partially dependent on functionality. These attributes are better documented in documentation associated with the main package.  

## Managing Dependencies

Enabling package encapsulation allows you to control dependencies within packages.  
In the package interfaces, you define the visibility of objects when package encapsulation is enabled, and you use the usage declaration to document dependencies on other packages via their package interfaces.
The package check is the tool used to identify and monitor the use of invisible objects or missing usage declarations.  
How you specifically use these elements is explained in the [detailed section]({{ site.baseurl }}/abap/package_details/#package-check) on the package concept. You can also find information about this in the SAP documentation.

## Benefits and Added Value from Implementing the Package Concept

### Clearly Defined Dependencies

Applying the package concept makes dependencies between functionalities transparent. Either a dependency is listed in the usage declaration—in which case it is a deliberately defined dependency—or the dependency becomes apparent through an error message during package validation—in the case of invisible objects or a missing usage declaration. The information obtained from this can be used for documentation and description. Before a package is imported into a system, it is thus possible to check whether the system meets the prerequisites for importing the package without errors, or whether other packages are required.

### Transparency and Understandability

In complex and large-scale development projects, proper structuring helps developers locate relevant objects more quickly. The structure itself can be considered part of the documentation.

When corrections, enhancements, or additions to an in-house development are required, a well-structured package helps the developer navigate the application more easily and implement enhancements more quickly.  

If software is to be transported across systems, we recommend creating transports at the main package level. The main package represents a self-contained business function or an extension of a standard function or a defined area.  
If all objects of a main package (structured into subpackages) are included in a transport and the declared prerequisites/dependencies are met in the target system, the transport can be transported and imported across system lines. Import errors (RC8) should then generally no longer occur.

### Flexibility

When a software component is well structured, additions, changes, extensions, and corrections can be made more easily than when an application consists of loosely assembled objects in a large, unorganized package that contains other objects for other functions. This means that good structuring also results in increased flexibility. In particular, if functionalities grow over the course of the life cycle and the scope increases, it may be necessary to adapt the structure and, if necessary, to outsource functionalities into central or generally available packages in order to achieve reusability or, in the opposite case, to combine several smaller applications into a main package.

### Future viability

In addition to the obvious advantages, creating software in well-structured packages also includes other advantages that do not take effect immediately, but can become relevant as part of the software life cycle.  
If the in-house developments in the system are already organized into packages, important requirements have already been met in order to use modern version management systems such as abapGit or gCTS, which require packages. This means that transports using Git-based methods into other systems or even into the Cloud are possible, see chapter [Version Management]({{ site.baseurl }}/application-lifecycle-management/version-management/).
If the package concept, including an explanation of usage relationships, has already been implemented within the company and there is thus already awareness regarding usable objects, good conditions are in place to understand and apply the concepts in ABAP Cloud with the software components.

## Measures for Implementing the Package Concept in Development

### Definition and Implementation of the Package Strategy

The benefits mentioned above can only be realized if the package concept is implemented comprehensively and consistently throughout the company in the form of a package strategy. It is therefore important that you clearly define your package strategy and establish how packages are created and documented.  
Ensure that the individuals responsible for development understand and can implement the guidelines for the package concept. Therefore, it is important to provide developers with sufficient training on the package concept to be implemented and to verify compliance and proper implementation. Particularly when external developers are used, it is important to ensure that appropriate onboarding takes place. The task of defining the packages, structuring them, and classifying them within the package landscape should be carried out by the software architect or the person responsible for software development, such as the SAP Lead Developer, to ensure consistency across packages.

### Avoiding Large/Non-Specific Collection Packages

We recommend not allowing the creation of large collector packages (e.g. at the base module level), as this can lead to issues with readability and unwanted dependencies, and violates the Single Responsibility Principle.  
There is a high risk that, for various reasons, numerous diverse classes and functions will end up in such packages instead of being based on sound architectural considerations, which can undermine efforts to maintain a well-organized system architecture.  

However, it can certainly make sense to create small, well-defined, and domain-specific helper packages that centrally provide basic and frequently used helper functions.

## Further Considerations Regarding the Implementation of the Package Concept

In addition to the recommendations regarding the package concept described here, there are other issues that cannot be addressed in detail here, as doing so would exceed the scope of this guide. However, these should be taken into account and defined in the guidelines and manuals. These include the following aspects:  

- Avoiding static dependencies – packages should be defined in such a way that they are independent of other packages
- Definition of the procedure when dependencies are unavoidable or desirable. There are various possible solutions here, such as:
  - by defining BAdIs - which are then implemented locally and used to establish the package connection
  - Calling a function from another package via dynamic function module calls
- Package size – architectural boundaries – demarcation – costs (Clean Architecture)
- Package refactoring – splitting – combining individual packages – continuous package maintenance during changes and extensions

## The Package Concept in ABAP Cloud – Software Components

In the context of ABAP Cloud, the package concept described here is no longer directly applicable, as package interfaces are no longer supported in the cloud.  
With the introduction of the ABAP Environment for development in the cloud and with ABAP Cloud, the “Software Component” (SWC) property—which has long existed but was generally not used for structuring—takes on a central role in the structuring of ABAP software. When developed with ABAP Cloud, the software component becomes a central part of the software structure and complements the package concept.
The packages within the software component serve to structure the various parts of an application.
Package interfaces are no longer used here, as dependency relationships are no longer maintained at the package level. However, the principles are comparable. For software components, usage is controlled via release contracts (C1). This means that objects in software components can be used system-wide, provided they are assigned a release contract.  
If the software components are to be used only by objects of defined software components, this can be done through so-called software component relationships. The software components declared here are granted permission to use all objects of the SWC. It is not possible to restrict access to specific objects within one’s own SWC. Detailed information can be found in the [SAP Documentation for SWC](https://help.sap.com/docs/abap-cloud/abap-development-tools-user-guide/software-component?locale=en-US)  

Even though some elements of the package concept are no longer present in the cloud, the implementation and application of the concepts described above still make sense in current on-premise and private cloud SAP systems, as they structure developments and declare dependencies and visibility, thereby helping to create well-structured applications.  

## From architecture to design

After the statements mentioned here have created the prerequisites for a good architecture, which is reflected in the package structure, the application architecture must now be defined/designed in the specific form of classes in the individual sub-packages. You can find the information on this in section: [Design and design of modern SAP applications]({{ site.baseurl }}/abap/oo-design/).
