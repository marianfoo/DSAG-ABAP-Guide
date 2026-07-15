---
layout: page
title: Design and design of modern SAP applications
permalink: /abap/oo-design/
parent: Modern ABAP Development
nav_order: 2
---

{: .no_toc}
# Design and Development of Modern SAP Applications

1. TOC
{:toc}

## Modern Business Applications Require Modern Software Development Practices

Business applications developed using traditional procedural ABAP implemented as programs characterized by complex, procedural, deeply nested control structures. Modularization was achieved through form routines or, for reuse, through function modules. With good planning and the application of software development methods, function groups were not overloaded but consisted of related, specific functions. However, you may have encountered one or two function groups that accumulate a large number of function modules with different tasks and have occasionally caused problems during one or another transport. As the number of changes increased, these applications became increasingly complex, more error-prone, and harder to maintain.

Modern applications face high demands today:

- Applications must fully meet functional requirements.
- Applications must be able to operate error-free, robustly, with high performance, and be fault-tolerant.
- Changes should be implementable quickly, efficiently, and without errors, requiring minimal testing effort, and should not introduce new bugs.

Requirements must therefore also be made for the ABAP code:

- ABAP code must correctly meet the functional requirements and have no negative impact on security issues or other developments.
- ABAP code should be structured in a technically precise manner. It is developed in small, semantically matching and modular units.
- ABAP code should be written in a readable and understandable manner, and comments help in understanding the implemented functionality.
- ABAP code should correspond to the [Clean Core level model]({{ site.baseurl }}/clean-core/solution-approach/#level-concept).

These requirements are difficult to meet using traditional, procedural ABAP programming, as this approach offers high backward compatibility, relies on outdated features, and makes maintenance more difficult. This traditional, procedural approach is no longer up to date and should no longer be used.

The software development methods and techniques available to ABAP developers today offer effective solutions to the issues mentioned above and to the challenges posed by the requirements of modern business applications.

For many years now, ABAP has offered the ability to program in an object-oriented manner. Even though this was not initially required, it is now technically necessary if new capabilities are to be utilized. Furthermore, the methodology of object-oriented programming offers many effective approaches for developing business applications in a way that ensures they are flexible, maintainable, extensible, and robust. By using ABAP Unit and a sound design, numerous functions can be verified through unit tests. This allows end-user testing to be limited to verifying the process, thereby reducing the testing effort in the business department, since the internal structure of the software is validated via ABAP unit tests.

Although the aforementioned disadvantages of procedural programming and the advantages of object-oriented programming are well known, functionalities in current projects are still often implemented in a non-object-oriented manner, or the full potential of modern development methods is not utilized. Examples of this include programs implemented procedurally, classes that do not implement object-oriented principles, or implementations of function modules, as well as direct implementations of complex code in BAdI implementations without further structuring into separate classes. All of this should be avoided and resolved by applying appropriate object-oriented principles.

{: .recommendation}
>- Demand that all developments be implemented in ABAP Objects using object-oriented methods.
>- Pay attention to the application of the SOLID principles of object orientation.
>- Apply common object-oriented design patterns when designing applications.
>- Separate the different concerns of the business applications into classes (e.g. controller class, data access, business logic, tests, etc.).
>- Keep the interfaces small and use the factory to transfer important data to the object.
>- Wrap and concentrate calls to SAP code or non-package code in their own private methods.
>- Use class-based exceptions for complete error handling including message handling in the application.
>- Only propagate interfaces or special facade classes in the package interfaces.

While we cannot provide a comprehensive overview of object-oriented programming and the many capabilities of modern ABAP in this guide, we would like to offer recommendations, tips, and guidance on how to proceed. These will help you get started and provide an overview of areas where you can quickly make improvements.

## Fundamentals and Basic Application of Object-Oriented Programming in the ABAP Context

The topic of object-oriented programming is complex, and many existing functionalities in SAP do not follow the design principles of object-oriented programming, even when they are implemented in ABAP classes. For this chapter, you should already be familiar with the basic principles of object-oriented programming.

The notes and tips provided here are presented in a simplified form. They are intended to demonstrate an approach for effectively applying object-oriented programming and to support our recommendations with practical examples.

## Features of Object-Oriented Development in ABAP Classes

A class represents a specific task that is implemented in manageable methods. An ABAP class consists of attributes that can store values or define constants. ABAP classes are often viewed as a modern form of function modules, but this comparison does not do justice to the capabilities of a class. The crucial difference is instantiability: multiple objects of a class can be created in the same program context.

A class that contains only static methods and is not instantiated during use is therefore not a class that follows object-oriented principles.

{: .note }
> Identifying characteristics of a class that **doesn't** follow object-oriented principles are:
>
> - Size of the class - a class with many (public) methods probably shows that the single responsibility principle has been violated  
> - Size of the methods - extensive methods indicate structural deficiencies, redundant code and violation of the separation of concerns principle.  
> - Extensive parameter interfaces - Objects work with objects and not with parameters. This is usually associated with methods that are too large. Therefore, object-oriented methods often have very narrow interfaces that contain objects as transfer parameters, or return parameters in functional methods.  

Classes that have these identifying features contradict the above requirements for modern ABAP code.
Further indicators can be found, for example, in the [Clean ABAP Style Guide](https://github.com/SAP/styleguides/blob/main/clean-abap/CleanABAP.md).

Classes should be designed clearly and, in accordance with the single-responsibility principle, only fulfill one task. Methods as short as possible and only accomplish one task. This restriction forces tasks to be delegated to different classes. This means that the individual classes are less complex, and the complexity shifts depending on the application in the class network and the interaction of the individual classes. This interaction and the higher-level logic is bundled in a **Controller**.  
In order to reduce a shift in complexity and avoid structural deficits, good planning and design of the structure of the application is required.  
Moving and renaming methods and attributes, and [refactoring]({{ site.baseurl }}/abap/oo-design/#the-importance-of-refactoring-existing-applications) objects during development, are normal parts of the software-development process. Modern tools in ABAP Development Tools for Eclipse and additional add-ons make these changes easier and safer.

## Basic Principles of Object-Oriented Programming (SOLID)

When you get started with ABAP Objects, it quickly happens that a function group with several function modules simply becomes a class with several static methods. However, the advantages of object orientation cannot be used this way. The use of static methods prevents dependencies in unit tests from being replaced by mocks. You can find more information about this in [Clean ABAP-Guide](https://github.com/SAP/styleguides/blob/main/clean-abap/CleanABAP.md#prefer-objects-to-static-classes).

The SOLID principles are a useful tool for object-oriented design. Each letter represents a principle for object-oriented development. The principles are as follows:

- **S**ingle Responsibility Principle
- **O**pen/Closed Principle
- **L**iskov Substitution Principle
- **I**interface Segregation Principle and that
- **D**ependency Inversion Principle

A short description of the principles can be found in the [subsection]({{ site.baseurl }}/abap/oo-basics/), a detailed explanation can be found e.g. [on Uncle Bob's blog](https://blog.cleancoder.com/uncle-bob/2020/10/18/Solid-Relevance.html), the author of Clean Code.

In particular, the first two principles can be implemented in ABAP without requiring an overly deep understanding of OO, and the added value becomes quickly apparent when code maintenance and modification can be performed more effectively and fewer side effects occur. Detailed knowledge and their application in the ABAP context can be found in the technical literature on Agile Software Development in ABAP and Test-Driven Design in ABAP.  

## Design patterns

In object orientation, there are numerous design patterns that offer ready-made and tried-and-tested software mechanisms for various problems and use cases. These can also be applied in ABAP. The following patterns can be used directly and sensibly in ABAP:  

- **Factory** - Creation of instances of a class
- **Singleton** - Creation of a central instance of a class
- **Facade** - Enclosing the complexity of a function  
   Facades are suitable for propagation in package interfaces for use by other packages
- **MVC** (Model-View-Controller) - Separation of the interests of an application

Detailed explanations and code examples can be found in the [subsection]({{ site.baseurl }}/abap/oo-basics/)

Here, too, we unfortunately cannot go into all the design patterns in detail; on the Internet and in specialist literature you will find numerous opportunities to approach the topic and bring it into the organization. A good starting point for your own research is, for example, [ABAP-OO Design Patterns m. Beispielen](https://zevolving.com/category/abapobjects/oo-design-patterns/).

## Comparison of procedural vs. object-oriented development

### Process procedural development

When implementing a requirement, for example in a report or a function module, the design according to the specification would typically be as follows:

- Retrieving input data from import parameters
- Reading Customizing settings from the database (e.g., Z-table)
- Reading data from database tables
- Processing data using loops, read tables, and various IF-ENDIF control structures: e.g., checking, calculating, sorting, filtering …
- Transferring the result and the export parameters. This represents the requirement in imperative form as program code; where necessary, subfunctions are modularized.

### Process with object-oriented approach

Once the requirements are known and analyzed, the different tasks must first be defined and grouped. The classes and derived meaningful class names can be defined based on the tasks. Based on this approach, the object-oriented implementation can look like this:

- Definition object for reading and evaluating the Customizing based on organizational data = **Customizing object**
- Definition of object for reading the database, if necessary split by business object depending on complexity = **data object(s)**.
- Definition object which carries out the data checks and validations = **Check object**
- Definition object that carries out the data processing and is responsible for creating the result **business logic**.
- Definition object that maps the business functionality and orchestrates and manages the interaction of the individual objects = **Controller**.
- Creation of a factory class that creates the individual object instances.
- Definition of an injector class that enables mocking of individual functions.

The details about the ABAP unit and how to create unit tests can be found in the chapter [**Testing**]({{ site.baseurl }}/testing/index))

## Concepts in object orientation

In addition to the fundamentals, there are other concepts and techniques whose use is essential for realizing the full benefits of object-oriented programming and for elegantly solving even complex problems—tasks that would be significantly more time-consuming or even impossible to accomplish using traditional technologies. We can only briefly touch on these topics in the first version of the new guide. You can find further information in the ABAP documentation, as well as in training courses and books.

### Creation of factories

Each object should have a factory method; the necessary parameters are passed to the class via its constructor. If the classes in an application are instantiated via a central factory, the class’s factory method is called within the factory class. By applying the factory pattern, control over object instantiation remains with the classes or the central factory class.

{: .note }
Avoid instantiating classes from outside using the *New* or *Create Object* command.

### Example: Formwork of the Customizing in the factory method

A class responsible for evaluating Customizing settings can be designed so that the factory method checks the Customizing table where the function's control logic is stored.

An instance is only passed to the caller if there is an entry in this table corresponding to the parameters of the factory method (e.g., plant or company code, etc.).

Individual Customizing parameters can be stored in attributes of the Customizing class and retrieved as needed in other related classes using so-called getter methods.

If no entry exists or a problem occurs, an exception should be thrown, which is caught by the caller. Thus, the caller no longer needs to check the table but only receives an instance if the function is active in the given case. If successful, the corresponding methods can then be called via the returned instance.  

Alternatively, the Null Object design pattern can also be used here, in which, in the event of a negative Customizing check, a class with an empty implementation is returned instead of the class with the actual implementation. When the methods of the null object are called, nothing happens. This has the advantage that the caller does not have to deal with exceptions.  

Since the object structure is aware of the Customizing instance via the factory, access to Customizing is standardized throughout the structure and can be achieved without redundant code. This approach follows the principle of inversion of control and contributes to the separation of concerns. This simplifies the business logic code and encapsulates or automates the complexity of Customizing.

The creation of technical objects initially appears more complex than the top-down procedural approach.
By means of autocompletion, use of code templates and quick fixes in the ABAP development tools in Eclipse (ADT), the ABAP code for the technical classes is created very quickly and easily, which means that the additional effort in coding is very limited.  
Once this pattern has been practiced, the advantages of this procedure far outweigh the disadvantage of the supposedly increased initial effort.  
Of course, the procedure must also be practiced in order to develop a certain development performance and efficiency.  
Please note the **[ADT Guide](https://1dsag.github.io/ADT-Leitfaden/)** from DSAG, which supports you in using ADT efficiently and across the board in the company.

### Full use of class-based exceptions for error handling

Use only class-based exceptions for error handling. These should be used exclusively for errors and should not be misused for success or status messages from the application. Only technical limitations on SAP’s part force you to use classic exceptions in a few specific cases.  
We advise against using return codes as well as the sole returning message tables such as BAPIRET2, as is often found in BAPI function modules. These approaches create the problem that the calling program must check for errors within the business logic flow, thereby preventing a clear separation of technical concerns and business logic.
The use of exception classes enables significantly better separation here, and you can also bundle error handling in central locations due to the propagation of exceptions. Please also note the recommendations of the
[Clean ABAP Style Guide](https://github.com/SAP/styleguides/blob/main/clean-abap/sub-sections/Exceptions.md)

A developer experienced in ABAP-OO defines, during the design phase, the error scenarios that can occur in a (sub)package and, based on this, creates the corresponding exception classes with the error messages (as text IDs or message-based).
When the business logic code is implemented and errors need to be handled, the exception is raised at the relevant point. Handling does not have to take place in every call layer, as is the case with function modules, but can be performed centrally in one location.
This ensures consistent handling and reduces the effort required when errors can occur in multiple locations.

### Interfaces

The use of interfaces decouples the definition of methods from their implementation. When an interface is used, the implementation of the class can be modified or made more flexible. The interface, so to speak, defines the contract between the user and the implementing class and thus "hides" the implementation (software hiding principle).  
For public methods that provide functions for other classes, you should always define interfaces and thus ensure that users only work with these interfaces. The creation of concrete objects is handled by a separate factory class or, in particularly simple cases, a factory method of the class, e.g.: ```ZCL_BUSINESS_LOGIC=>GET_INSTANCE( CompanyCode )``` [see SAP style guide](https://github.com/SAP/styleguides/blob/main/clean-abap/CleanABAP.md#prefer-multiple-static-creation-methods-to-optional-parameters)

Interfaces are also required for unit tests, since, for example, database accesses in unit tests have to be replaced by programmed test data. The database class implements an interface that is called in the product code. When the unit test is executed, instead of the database class, a so-called mocking class is called, which contains statically stored data, provides methods for local test data generation and returns it. The information on this can be found in chapter [Testing]({{ site.baseurl }}/testing/index).

### Inheritance

An important concept in object-oriented programming is inheritance. In this context, a class can be derived from another class and thus inherit the properties of the parent class. Consequently, a derived class has the attributes and methods of the parent class, but can add additional specific methods or redefine inherited methods—that is, it can extend the inherited implementation or even provide its own implementation of the method.  
When using inheritance, the Liskov Substitution Principle must be observed, and you should carefully consider whether inheritance makes sense in the intended context. It is often better to use interfaces or delegation instead of inheritance, to distribute different aspects of a class across different classes, and to manage their interaction via a controller and their instances via a factory.  

## Object-Oriented Programming in Function Modules and Form Routines

Sometimes it is necessary to implement functionality within predefined artifacts—for example, function modules in AIF, remote function modules, or form interface routines in Adobe Forms, etc.
In such cases, these development objects serve as wrappers and merely call the actual functionality, which is then implemented in ABAP classes and their methods. The code in these development objects should be limited to technical coding, such as data assignments, object instantiation, or minimal checks.
This in turn offers the advantage of possible reuse and implementation of unit tests.

## Use of SAP Code – Demeter’s Law

The use of SAP code (classes, function modules, BAPIs, etc.) or code from outside the package should always be placed in a separate access layer. This also ensures a clear separation of concerns (S – Separation of Concerns).  
This corresponds to the object orientation design guideline ["Law of Demeter"](https://de.wikipedia.org/wiki/Gesetz_von_Demeter), which states that objects should only communicate with objects in their immediate surroundings.  
Even if these are shared elements, they should always be encapsulated within a class so that there is a central point of transition between internal and external code.  

Create classes whose purpose is to keep the application’s program code free of any dependencies on SAP code or code from outside the package. This will also promote code reuse.  
If creating custom classes is overly complex, in special cases the separation can also be achieved by calling the external code within private methods created specifically for this purpose. The interface definition should be oriented more toward the caller and not the called object. This makes it easier to replace the external code used later on. Depending on the complexity, the mapping between proprietary and external code interfaces can be outsourced to separate methods.  
The goal here is to maintain control over dependencies and increase the maintainability of the software.

Data access, e.g. CDS views or SAP function modules, should be implemented in a separate database access layer for testability reasons, which enables decoupling of data access via dependency inversion for ABAP unit tests (see the Testing chapter).

A helpful extension of these classes is the transformation of classic exceptions or return codes used by SAP code for error handling into exception classes.  
This separation is also an important prerequisite for the testability of an application.

## Testability Through Good Design

Good structuring, both within packages and within objects, is essential for improving the testability of the software. If the responsibilities of the components are clearly defined within a sound architecture and tasks are sensibly distributed across different objects, this significantly facilitates the use of ABAP Unit.
Test-related aspects must already be taken into account as part of the aforementioned architecture and design decisions in order to implement ABAP Unit efficiently, since the structure directly impacts testability.

If database accesses and accesses to SAP function modules or classes are already encapsulated in a separate software layer and the instances are created via a factory that provides for injection, it is straightforward for an experienced developer to test their own code using ABAP Unit tests and to decouple database accesses and SAP functions via test mock objects. This significantly reduces the effort required for unit test creation compared to an approach in which the test developer must apply techniques such as test seams in the code or modify the code to ensure the decoupling of in-house development from SAP modules in tests.

Procedures, recommendations, and information about ABAP Unit can be found in the [Software Testing with ABAP Unit]({{ site.baseurl }}/testing/#software-testing-with-abap-unit) chapter.

## The Importance of Refactoring Existing Applications

The recommendations, technical methodologies, and programming techniques described in this guide can be easily incorporated and applied when developing new applications. In addition, they can and should also be used to improve existing applications. This is known as refactoring.  

Refactoring should always be carried out when existing applications need to be changed or extended, and time must be planned for it. The [Clean ABAP Style Guide](https://github.com/SAP/styleguides/blob/main/clean-abap/CleanABAP.md), for example, offers useful advice on approaching refactoring carefully.

Refactoring not only describes the improvement of the code in detail, but can also be applied figuratively to the structure in the form of packages. Objects can be usefully distributed into new sub-packages. If your applications are not currently based on a structure organized by main packages, we recommend creating main packages that represent your main functionalities and previous packages can then be assigned to these packages according to their affiliation. It is possible to split packages that are too large into smaller packages, but the dependencies must be checked, clarified and, if necessary, eliminated. However, packet encapsulation and packet inspection help with this. These functionalities are explained in detail in the optional section [Basics of the package concept]({{ site.baseurl }}/abap/package_extended.md).
Improvements to existing software should occur continuously and in small steps and be backed up by tests. If this is integrated into the development process and part of the day-to-day development business, it will pay off with more maintainable and less error-prone software.

## Good Architecture Also Requires Clean Code

Now that you have learned about the architecture and structure of modern application development and about methods for designing software, the next section will explain the characteristics of clean code and provide our recommendations and tips on how to achieve modern, clean code in application development. After all, an application should not only have good architecture and structure. It is equally important to write clean code and follow the principles of clean code. This supports the goal of modern and maintainable software.  
