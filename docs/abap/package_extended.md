---
layout: page
title: Basics of the package concept
permalink: /abap/package_details/
parent: Architecture and structuring in the ABAP development
grand_parent: Modern ABAP Development
nav_order: 1
---

1. TOC
{:toc}

{: .no_toc}
# Basics of the package concept

For a better understanding of the recommendations mentioned in the guide, the basics are explained in detail below. We also recommend using the official SAP documentation.

## Explanations of terms for the package concept

A **package** is used to structure software. A package combines software artifacts that are responsible for a specific purpose. Packages can (and should) be encapsulated. This means that an object from one package cannot use an object from another package or cannot be used by an object from another package unless they are made public via a package interface and declared to the user in the where-used list.  
In order to make our recommendation practical for you, a few basics are mentioned below and then the benefits and advantages are explained.

In the SAP package concept there is the **main package**, which contains sub-packages but no development objects. The main package usually represents a standalone solution. Other cases are described below.  

A **sub-package** is defined by the fact that it is not marked as a main package and is assigned to a main package. The subpackages are used to internally structure the artifacts of the main package.  
The main package defines the external structure and represents the various applications. The sub-packages define the internal structure of an application.  

The **package interfaces** are defined per package and define the external visibility of the objects contained in the package interface.

The last term to be explained here is the **Usage Declaration**, which is maintained in a package. Package interfaces whose objects are used by the current package are included in the usage declaration of that package.  
If a package A uses an artifact from a package B, the corresponding package interface B is included in the usage declaration of package A. This makes it immediately clear at the package level which dependencies package A has (namely to package B). The usage declaration can also be evaluated in the where-used list. This makes it possible to find out how the usage relationships are designed.

Above the main packages are **structure packages**, which combine main packages at the highest level. These make sense especially for large software projects where there are a large number of main packages.
To reduce complexity, structure packages will not be discussed further in this guide. Details can be found in the SAP documentation.  
Using structure packages makes sense if the package concept is already widely used in the company with main and sub-packages, allowing a higher-level structure to be meaningfully mapped. SAP uses structure packages to ensure technically secure decoupling of packages; these should not be defined at the main package level [SAP Documentation: From packages to structure packages](https://help.sap.com/docs/ABAP_PLATFORM_NEW/bd833c8355f34e96a6e83096b38bf192/4aa197adacd5007fe10000000a42189c.html?locale=de-DE).  
Package interfaces of structure packages cannot contain development objects but rather define relationships to other structure packages. This reduces the declaration and maintenance of usage relationships and ensures the technical decoupling of applications (e.g., SAP_APPL and SAP_HR).  
In the ABAP Cloud context, structure packages are required as root packages of software components and are therefore necessary.

## Definition of the main package

In the following information we describe the aspects of the package concept for the creation of a larger in-house development. Other cases will be discussed later.
When implementing in-house developments, it must be clearly defined which function the software fulfills and which application area it affects. The name of the in-house development is thus defined as a component. Company development guidelines, including naming conventions and prefixes, must be observed.
Naming is crucial and should be carefully considered, taking other components into account. The name should clearly indicate the SAP object type (e.g., document type, form) and the function the component fulfills. Since custom developments are usually related to SAP functions, this connection should be recognizable via the name. Names often need to be shortened sensibly due to character limits imposed by namespaces and prefixes.  
For example, if implementing a separate, reusable extension in the EWM area for handling unit processing, the name should reflect the EWM area, the HU object, and the task. The name could, for example, be composed as follows: *Z_EWM_HU_PROCESSING*.  
This package can then contain several EWM functions affecting HUs.

This is the name of the main package, which can now be created in SAP and is set as both main package and encapsulated. When creating the package, the SAP application component is now assigned; the same component should be used that is also assigned to the associated SAP standard component. This can be found in the package of associated SAP objects that are related to the in-house development.

Within this main package, create sub-packages whose names are based on the main package, with postfixes expressing the sub-package's function. A sub-package to the EWM-HU package that concerns packaging could, for example, be derived as follows: *Z_EWM_HU_PRC_PACKING*.

## Creation of sub-packages - division according to the function of the included objects

Main packages should not be divided into sub-packages by object type (e.g., DDIC, Forms, Classes) but rather by logical function. Depending on the software type, the following sub-packages can be created:  

- **.._CORE** or **..._ENG** (for engine) basic package
  This package contains objects used by other sub-packages, holding core functionality such as business process logic and shared functions.  
- **.._UI** - All application interface artifacts.
- **.._API** or **..IF** - E.g., for OData services, classes, or RAP BO interfaces usable by other packages, propagated in the package interface.
- **.._DATA** - Objects encapsulating database queries or obtaining data (e.g., CDS artifacts).
- **.._TEST** - Objects for unit tests, test helpers, mock objects, and other test infrastructure.
- **.._HLP** or **..SHARED** - Sub-packages for helper objects or functions used in multiple sub-packages (e.g., message classes or logging).

## Use of packages when implementing BAdIs and small extensions

The structure described above is useful for larger developments with numerous objects, creating order and overview. The same approach in a reduced form also makes sense for small extensions, such as BAdI implementations.
Create a main package corresponding to the SAP enhancement spot package, following naming conventions and assigning the same application component.  
The sub-packages can be structured here according to the sub-areas of the individual BADIs, depending on the scope of the individual BADIs of the enhancement spot.
For functions reused in multiple BAdIs, create objects in Helper and Core sub-packages as described and call them accordingly.

For very small developments like auxiliary reports or individual classes providing functions distributed across packages, separate main packages with sub-packages would be oversized.  
In this case, we recommend creating main packages that provide common functions in a function-oriented manner (e.g. 'Area'**_UTILS**). Sub-packages can further structure individual task areas, with central functions collected in the Core sub-package.

Ideally, propagate externally visible functions in package interfaces so users can declare them in the where-used list.

## Package interfaces

The measures described above require architectural considerations to be taken into account early in implementation, reflecting the application structure in packages.  
However, significant advantages and improvements in software management only arise through the use of the package interfaces.

If a package is self-contained and its objects are not intended for use by other packages, a package interface is not required. If a package is intended to expose functionality to other packages, package interfaces are required.  
Objects intended for use by other packages are explicitly included in the interface. Package interfaces follow the same hierarchical structure as the packages themselves. For details on the structure of package interfaces and how objects from subpackages are propagated via the main package, refer to the SAP documentation.

A well-designed package should include an interface subpackage containing interfaces, classes (particularly facade classes), and other artifacts intended for use by other packages.  
This interface package hides the implementation details (information hiding) and thus the complexity of the application. By exposing these objects via the package interface, they are explicitly declared for external use. This allows internal changes to be made freely as long as the external interface remains stable.  
If incompatible changes are necessary, new interfaces should be created, added to the package interface, and released as a new version.

## Usage Declaration

At the package level, in addition to the interfaces exposed to the outside world, there is the usage declaration. This lists which package interfaces a package uses. The usage declaration allows you to verify whether dependencies on other packages are intentional. These dependencies are thus technically documented and can be evaluated.  
This applies to SAP packages as well. If SAP objects are declared in package interfaces, they can be automatically included in the where-used list via the package check and suggestion function. However, SAP does not provide package interfaces for customer communication regarding object release.
The usage declaration helps provide an overview of visible objects (via the usage declaration) and invisible objects (identified by errors in the package check).

## Package Check

Package checking plays a central role in implementing the package concept for in-house developments. It can be performed in the ABAP Development Tools (ADT), in the ABAP Test Cockpit (ATC), or in transaction SE80.  
To perform a package check, packages must be encapsulated. The package check must also be configured at the system level as described in the documentation.  
Two error scenarios may occur during package checking, providing information about existing dependencies:  

- **Invisible Object**: If you use an object from another package that is not included in a shared package interface, the package checker reports an error indicating the object is not visible.
You can react in different ways:
Avoid using the object; instead, use an alternative or create your own object within the package to provide the function.  
If you wish to use the object, contact the package manager of the other package to have it included in their package interface.

- **Missing Usage Declaration**: If you use an object from another package that is exposed via a package interface, you must declare this interface in your usage declaration to avoid package check errors. This declaration can be generated automatically from the package check message, considering the entire hierarchy. This is helpful and time-saving for complex SAP packages.

The package manager is responsible for determining which objects in their package are made available to other packages and adding them to the package interface accordingly to avoid package check errors. Users must then include this package interface in their usage declaration, enabling a technical evaluation of dependencies.

## Package Encapsulation and Interfaces of Subpackages

Encapsulating main packages helps document dependencies via package checking. Encapsulation is also useful for subpackages. Create a package interface for each subpackage and include objects used by other subpackages in it. Maintain the usage declaration accordingly. Although this involves administrative effort, it documents subpackage dependencies and allows for targeted control and monitoring. Define clear usage relationships per main package and avoid mixed reuse within subpackages.  
For large collection packages, it may be beneficial to split them into smaller, independent components if the size warrants it. Clear and orderly usage relationships are helpful in this context.

## Package Hierarchies

Using the methods and tools described above, a robust software architecture can be represented in SAP through packages and their dependencies. Good package design considerations lead to good application architecture when clean architecture principles are followed. Information on modern software architecture principles can be found in specialist literature, such as "Clean Architecture" by Robert C. Martin.  
When designing packages, consider developments across packages. When creating new packages or expanding existing ones, evaluate how well they fit together and determine whether your own functional developments should be separated into distinct packages. In complex system landscapes, it may be beneficial to define framework packages for basic functions, followed by function packages representing business logic, and optional add-on packages for different interface technologies or functionality versions. This creates a hierarchy of main packages whose dependencies can be easily mapped and documented via package interfaces.
Ensure that dependencies are defined in only one direction.

Another use case is providing the same functionality for different releases, with the core function implemented in a central package and release-specific differentiations in separate main packages.
