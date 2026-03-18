---
layout: page
title: Basics of the package concept
permalink: /abap/package_details/
parent: Architecture and structuring in the ABAP development
grand_parent: Moderne ABAP Entwicklung
nav_order: 1
---

1. TOC
{:toc}

{: .no_toc}
# Basics of the package concept

For a better understanding of the recommendations mentioned in the guide, the basics are explained in detail below. We also recommend using the official SAP documentation.

## Explanations of terms for the package concept

A **package** is used to structure software. A package combines software artifacts that are responsible for a specific purpose. Packets can (and should) be encapsulated. This means that an object from one package cannot use an object from another package or cannot be used by an object from another package unless they are made public via a package interface and declared to the user in the where-used list.  
In order to make our recommendation practical for you, a few basics are mentioned below and then the benefits and advantages are explained.

In the SAP package concept there is the **main package**, which contains sub-packages but no development objects. The main package usually represents the application that can run alone. Other cases are described below.  

A **sub-package** is defined by the fact that it is not marked as a main package and is assigned to a main package. The subpackages are used to internally structure the artifacts of the main package.  
The main package defines the external structure and represents the various applications. The sub-packages define the internal structure of an application.  

The **package interfaces** are defined per package and define the external visibility of the objects contained in the package interface.

The last term to be explained here is the **Declaration of Use**, which is maintained in a package. Package interfaces whose objects are used by the current package are included in the usage declaration.  
If a package A uses an artifact from a package B, the corresponding package interface B is included in the usage declaration of package A. This means that at package level it is immediately clear which dependencies package A has (namely to package B). The declaration of use can also be evaluated in the proof of use. This makes it possible to find out how the usage relationships are designed.

Above the main packages are the **structure packages**, which combine main packages at the highest level. These make sense especially for large software projects where there are a large number of main packages.
In order to reduce complexity, however, the structural packages will not be discussed further in this guide. Details can be found in the SAP documentation.  
It can make sense to use structural packages if the package concept is already used extensively in the company with main and sub-packages and a higher-level structure can be sensibly mapped. Structure packages are used by SAP itself to ensure a technically secured decoupling of packages and this should not be defined at the main package level [SAP Documentation: From packages to structure packages](https://help.sap.com/docs/ABAP_PLATFORM_NEW/bd833c8355f34e96a6e83096b38bf192/4aa197adacd5007fe10000000a42189c.html?locale=de-DE).  
The package interfaces of the structure packages cannot contain development objects, but rather define the relationships to other structure packages. This means that the declaration and maintenance of usage relationships can be reduced and the technical decoupling of applications (as with SAP_APPL and SAP_HR) can be ensured.  
As part of Cloud, structure packages are required as root packages of the software components and are therefore necessary there.

## Definition of the main package

In the following information we describe the aspects of the package concept for the creation of a larger in-house development. Other cases will be discussed later.
At the beginning of the implementation of an in-house development, it must be clearly defined which function the software should fulfill and which application area the software affects. This means that the name of the in-house development can now be defined as a component. The requirements of the company's development guidelines such as naming conventions and prefixes must be observed.
The naming plays an important role here and should be carefully considered, taking other components into account. It should be clear in the name which SAP object it is (e.g. document type, forms ...) and which function the component fulfills. Since custom developments are usually related to SAP functions, this connection should also be recognizable through the name reference. Most of the time the name has to be shortened sensibly because the number of available characters is limited by namespaces and prefixes.  
For example, if you want to implement a separate and reusable extension or in-house development in the EWM area that deals with functions in the processing of handling units, both the EWM area, the object HU, and the task should be reflected in the name. The name could, for example, be composed as follows: *Z_EWM_HU_PROCESSING*.  
This package can then contain several functions in EWM that affect HUs.

This is the name of the main package, which can now be created in SAP and is set as both main package and encapsulated. When creating the package, the SAP application component is now assigned; the same component should be used that is also assigned to the associated SAP standard component. This can be found in the package of associated SAP objects that are related to the in-house development.

Within this main package, the sub-packages must now be created, the names of which are based on the main package, but as a postfix they express the function of the sub-package. A sub-package to the EWM-HU package that concerns packaging could, for example, be derived as follows: *Z_EWM_HU_PRC_PACKING*.

## Creation of sub-packages - division according to the function of the included objects

The main package should not be divided into sub-packages according to object type (e.g.: DDIC, Forms, Classes), but rather according to logical function. Depending on the type of software, the following sub-packages can be created:  

- **.._CORE** or **..._ENG** (for engine) basic package
  This package creates objects that are used by the other subpackages and contain core functionality such as business process logic and shared functions.  
- **.._UI** - All application interface artifacts.
- **.._API** or **..IF** - e.g.: for ODATA services, classes or RAP-BO interfaces that can be used by other packages and are propagated accordingly in the package interface.
- **.._DATA**- Objects that encapsulate database queries or otherwise obtain data (CDS artifacts).
- **.._TEST** - Objects for unit tests and test helpers as well as mock objects - everything that is part of the test infrastructure.
- **.._HLP** or **..SHARED** - Subpackage for helper objects or functions that are used in multiple subpackages, e.g. message classes or logging functions.

## Use of packages when implementing BAdIs and small extensions

The structure described above is useful for larger developments where numerous objects are created and creates order and overview. The same approach in a reduced form also makes sense for small extensions, such as BAdI implementations.
Here you create a main package that corresponds to the SAP enhancement spot package, follow the naming and assign the same application component.  
The sub-packages can be structured here according to the sub-areas of the individual BADIs, depending on the scope of the individual BADIs of the enhancement spot.
For functions that are reused in multiple BADIs, objects can be created in Helper and Core subpackages as described above and called accordingly in the BADIs.

Sometimes developments are very small objects such as auxiliary reports, or individual classes that provide functions that are distributed multiple times across packages. Providing separate main packages with sub-packages for this would be oversized.  
In this case, we recommend creating main packages that provide common functions in a function-oriented manner (e.g. 'Area'**_UTILS**). The sub-packages can then further structure the individual task areas and central functions are collected in the Core sub-package.

Ideally, the externally visible functions are propagated in the package interfaces so that users can declare these packages in the where-used list.

## Paketschnittstellen

The measures described above mean that architectural considerations must be taken into account early on in the implementation and the structure of the application is reflected in the packages.  
However, significant advantages and improvements in software management only arise through the use of the package interfaces.

If a package is self-contained and the use of objects in the package by other packages is not required or desired, the package does not require a package interface. However, if it is a package that is intended to propagate functionalities to the outside and thus be used by other packages, package interfaces are required.  
Objects intended for use by other packages are specifically included in an interface. The package interfaces follow the same hierarchical structure as the packages themselves. Details on the structure of package interfaces and how objects from sub-packages are propagated via the main package can be found in the SAP documentation.

A well-designed package should have its own API or interface subpackage that contains interfaces, classes (especially facade classes), and artifacts that are shared for use by other packages.  
This interface package with its objects specifically hides the implementation (information hiding) and thus the complexity of the application. By propagating these objects in the package interface, these artifacts are explicitly declared for external use. This means that changes can be made within the package at any time, as long as the external interface remains stable.  
If there are incompatible changes to the interface, new interfaces will be created and included in the package interface and released as a new version.

## Statement of Use

At the package level, in addition to the interfaces that the propagation declares to the outside world, there is also the usage declaration. This lists which package interfaces a package uses. In this way, it can be checked in the usage declaration whether the listed usage and thus the creation of dependencies on package xy is really desired and intended. This means that these dependencies are technically documented and can be evaluated and read.  
This applies conditionally to SAP packages. If SAP objects have been declared in package interfaces, they can also be automatically included in the where-used list using the package check and suggestion function. However, SAP does not provide the package interfaces for communication with customers regarding object release.
At least the usage declaration helps to get an overview of visible (via the usage declaration) and invisible (errors in the package check) SAP objects.

## Package inspection

Package testing plays a central role in the sensitive implementation of the package concept in in-house developments. This can be carried out in the ABAP Development Tools, in the ATC or in SE80.  
To perform packet inspection, packets must be encapsulated. The package check must also be configured at the system level according to the documentation.  
Two error situations can occur during package checking that will provide you with information about existing dependencies:  

- **Invisible Object**: When using an object from another package that is not included in a shared package interface, the package checker reports an error that the object is not visible.
There are different ways to react here:
The object should not be used and the developer must use an alternative or create their own object within the package that provides the function.  
If use is desired, the package manager of the other package must be contacted so that the object is included in the package interface.

- **Missing usage declaration**: If an object from another package is used that is located in a package interface, this interface must still be declared in the usage declaration to avoid errors in the package check. This declaration can be done automatically from the package inspection message, taking the entire hierarchy into account. This is helpful and time-saving for the complex SAP packages.

The package manager has the task of checking which objects in his package are made available to other packages and incorporating them into the package interface accordingly in order to avoid package checking errors in the package being used. The user then includes this package interface in the declaration of use and a technical evaluation of the uses is therefore also possible.

## Package encapsulation and package interfaces of sub-packages within the main package

Encapsulating the main packages serves to document the dependencies via package checking. However, encapsulation is also useful for sub-packages. To do this, a package interface should be created for each subpackage and the objects used by other subpackages should be included in it. The declaration of use is then maintained accordingly. This involves administrative effort during creation, but has the advantage that the dependencies of the sub-packages are documented and targeted control and monitoring is possible. A clear usage relationship must be defined per main package and mixed reuse within the sub-packages must be avoided.  
Particularly in the case of collector packages, it can make sense to separate individual packages and provide them as independent components if the size is appropriate. It is helpful to already have clear and orderly usage relationships here.

## Pakethierarchien

Using the above methods and tools, a good software architecture can be represented in SAP via the packages with the dependencies. The considerations that go into good package design ultimately lead to good application architecture when clean architecture design principles are followed. Information on the principles of modern software architecture can be found in relevant specialist literature, e.g. "Clean Architecture" by Robert C. Martin.  
When designing packages, you should always look at developments across packages and when creating new or expanding existing packages, you should check to what extent the packages fit together and check whether in-house developments of your own functions should be separated into different packages. For complex system landscapes, it can make sense to define framework packages that offer basic functions, then basic function packages that represent the business logic and optional add-on packages that represent different interface technologies or versions of the functionalities. This creates a hierarchy of main packages whose dependencies can be easily mapped and documented via the package interfaces.
It is important to ensure that the dependency can only ever be defined in one direction.

Another use case would be, for example, to provide the same functionality for different releases, with the core function implemented in a central package and the differentiations according to release in different main packages.

