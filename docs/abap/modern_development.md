---
layout: page
title: Design and design of modern SAP applications
permalink: /abap/oo-design/
parent: Modern ABAP Development
nav_order: 2
---

{: .no_toc}
# Design and design modern SAP applications

1. TOC
{:toc}

## Modern business applications require contemporary software development methods

Business applications in classic procedural ABAP development are created in the form of programs characterized by complex, procedural, deeply nested control structures. Modularization was carried out using form routines or for reuse in functional modules. With good planning and application of software development methods, function groups were not overloaded, but instead consist of specific functions that belong together. Maybe you also know one or another function group that contains numerous function modules with different tasks and that has sometimes caused one or another problem during one or another transport. As the number of changes made, this application became more and more complex, more error-prone, and more and more difficult to maintain.  

High demands are placed on modern applications today:

- Applications must perfectly meet the functional requirements.
- Applications must be able to be operated error-free, robust, performant and fault-tolerant.
- Changes should be able to be carried out quickly, efficiently, without errors and with little testing effort and should not create new errors.  

Requirements must therefore also be made for the ABAP code:

- ABAP code must correctly meet the functional requirements and have no negative impact on security issues or other developments.
- ABAP code should be structured in a technically precise manner. It is developed in small, semantically matching and modular units. 
- ABAP code should be written in a readable and understandable manner, and comments help in understanding the implemented functionality.
- ABAP code should correspond to the [Clean Core level model]({{ site.baseurl }}/clean-core/solution-approach/#level-concept).

These requirements are difficult to meet with classic, procedural ABAP programming, as it has a high level of backward compatibility, offers outdated options and makes maintainability difficult. This classic, procedural approach is no longer relevant and should no longer be used.  

The software development methods and techniques that are available to ABAP developers today offer good solutions for the above-mentioned problem areas and the challenges that arise from the requirements of modern business applications.  

The possibility of object-oriented programming has been available in ABAP for many years. Even if this was not necessary at the beginning, it is now technically necessary if new possibilities are to be used. On the other hand, the object orientation methodology offers many good approaches to developing business applications in such a way that they can be implemented in a flexible, maintainable, expandable and robust manner. By using the ABAP unit and a good design, numerous functions can be tested via unit tests. This means that testing by the end user can be reduced to testing the process and thus the testing effort in the specialist department, as the internal structure of the software is secured via ABAP unit tests.

Although the above-mentioned disadvantages of procedural programming and advantages of object-oriented programming are known, functionalities are still not implemented in an object-oriented manner in current projects or the full potential of modern development methods is not used. These can be, for example, programs that are implemented procedurally, classes that do not implement object-oriented principles or implementation of function modules or direct implementation of complex code in BAdI implementation without further structuring in their own classes. All of this must be avoided and solved through appropriate principles of object orientation.

{: .recommendation}
>- Demand that all developments be implemented in ABAP Objects using object-oriented methods.
>- Pay attention to the application of the SOLID principles of object orientation.
>- Apply common object-oriented design patterns when designing applications.
>- Separate the different concerns of the business applications into classes (e.g. controller class, data access, business logic, tests, etc.).
>- Keep the interfaces small and use the factory to transfer important data to the object.
>- Wrap and concentrate calls to SAP code or non-package code in their own private methods.
>- Use class-based exceptions for complete error handling including message handling in the application.
>- Only propagate interfaces or special facade classes in the package interfaces.

We cannot cover the detailed explanation of object orientation and the numerous possibilities of the modern ABAP in this guide, but we would like to give you recommendations, tips and help regarding the procedure that make it easier to get started and provide an overview of areas of action that can quickly lead to improvements.

## Basics and simple application of object orientation in the ABAP context

The topic of object orientation is complex and many existing functionalities in SAP do not follow the design principles of object orientation, even when implemented in ABAP classes. For this chapter, the basic principles of object orientation should already be known.  
The hints and tips are presented here in a very simplified form. It is intended to show a procedure for using object orientation usefully and to support our recommendations in a practical way.  
This is a start and can help to create an understanding of ABAP-OO in the development teams, to achieve initial success experiences and to use the topic sustainably and profitably in the organization with further support through training and coaching, documentation, blogs and online events and through specialist literature.

## Features of object-oriented development in ABAP classes

A class represents a special task that is implemented in manageable methods. A ABAP class consists of attributes that can store values ​​or can be constants. ABAP classes are often viewed as a modern form of function blocks; this comparison does not do justice to the possibilities of a class. The crucial difference is instantiability, i.e. multiple objects can be created for classes in the same program context.

A class that only contains static methods and is not instantiated during use is therefore not a class that follows object-oriented principles.

{: .note }
> Identifying characteristics of a class that **doesn't** follow object-oriented principles are:
> 
> - Size of the class - a class with many (public) methods probably shows that the single responsibility principle has been violated  
> - Size of the methods - extensive methods indicate structural deficiencies, redundant code and violation of the separation of concerns principle.  
> - Extensive parameter interfaces - Objects work with objects and not with parameters. This is usually associated with methods that are too large. Therefore, object-oriented methods often have very narrow interfaces that contain objects as transfer parameters, or return parameters in functional methods.  

Classes that have these identifying features contradict the above requirements for modern ABAP code.
Further indicators can be found, for example, in [Clean-ABAP Styleguide](https://github.com/SAP/styleguides/blob/main/clean-abap/CleanABAP.md).

Classes should be designed clearly and, in accordance with the single-responsibility principle, only fulfill one task. Methods as short as possible and only accomplish one task. This restriction forces tasks to be delegated to different classes. This means that the individual classes are less complex, and the complexity shifts depending on the application in the class network and the interaction of the individual classes. This interaction and the higher-level logic is bundled in a **Controller**.  
In order to reduce a shift in complexity and avoid structural deficits, good planning and design of the structure of the application is required.  
The fact that methods and attributes are moved and renamed and objects are [refactored]({{ site.baseurl }}/abap/oo-design/#die-bedeutung-des-refactorings-von-bestehenden-anwendungen) during development is part of the software development process and can be carried out easily and safely thanks to modern software development tools in the ABAP development tools in Eclipse and additional add-ons.

## Basic principles of object orientation (SOLID)

When you get started with ABAP Objects, it quickly happens that a function group with several function modules simply becomes a class with several static methods. However, the advantages of object orientation cannot be used this way. The use of static methods prevents dependencies in unit tests from being replaced by mocks. You can find more information about this in [Clean ABAP-Guide](https://github.com/SAP/styleguides/blob/main/clean-abap/CleanABAP.md#prefer-objects-to-static-classes).

A tool for object-oriented designs are the SOLID principles. Each letter provides a principle for object-oriented development. There are the following principles:

- **S**ingle Responsibility Principle
- **O**pen/Closed Principle
- **L**iskov Substitution Principle
- **I**interface Segregation Principle and that
- **D**ependency Inversion Principle

A short description of the principles can be found in the [subsection]({{ site.baseurl }}/abap/oo-basics/), a detailed explanation can be found e.g. [on Uncle Bob's blog](https://blog.cleancoder.com/uncle-bob/2020/10/18/Solid-Relevance.html), the author of Clean Code.

In particular, the first two principles can be implemented in ABAP without a very deep understanding of OO and the added value quickly becomes apparent when maintenance and changes to code can be carried out better and fewer side effects occur. Detailed knowledge and application in the ABAP context can be found in specialist literature on the subject of agile software development in ABAP or test-driven design in ABAP.  

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

- Transfer of input data from import parameters 
- Reading the Customizing from the database (e.g. Z table)
- Reading data from the database tables
- Processing the data with loops, read tables and various IF-Endif control structures: e.g. checking, calculating, sorting, mixing...
- Transfer of the result and export parameters
This means that the requirement is represented in imperative form in program code and, if necessary, partial functions are modularized.

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

In addition to the basics, there are other concepts and techniques through which the full added value of object orientation can be achieved and even complex problems can be solved elegantly, which was much more complex or not possible at all with classic technologies. Here, too, we can only provide very brief information in the first version of the new guidelines. You can find further information in the ABAP documentation and in training courses and books.

### Creation of factories

Every object should have a factory method, passing required parameters to the class is done via the class's constructor. If the classes of an application are instantiated via a central factory, the factory method of the class is called in the factory class. By using the factory pattern, control of object instantiation remains with the classes or the central factory class.

{: .note }
Avoid instantiating classes from outside using the *New* or *Create Object* command.

### Example: Formwork of the Customizing in the factory method

A class that is responsible for evaluating the Customizing can be designed in such a way that the Customizing table in which the control of the function is stored is checked in the factory method.  
Only if there is an entry in this table for the parameters of the factory method (e.g. plant or company code, etc.) will an instance be passed to the caller.  
Individual parameters of the Customizing can be stored in attributes of the Customizing class and, if necessary, queried in other associated classes using so-called getter methods.  
If there is no entry for this or a problem, an exception should be thrown that is caught by the caller. This means that the caller no longer has to check the table, but only gets an instance back if the function is active in the relevant case. If positive, the corresponding methods can then be called via the returned instance.  

Alternatively, it is also possible to use the null object design pattern, in which, in the event of a negative customizing check, a class with an empty implementation is returned instead of the class with the implementation. When the methods of the null object are called, nothing simply happens. This has the advantage that the caller does not have to deal with exceptions.  

Since the customizing instance is known to the object construct via the factory, access to the Customizing is standardized throughout the entire construct and possible without redundant code.  
This procedure follows the principle of control reversal and contributes to the separation of concerns. This simplifies the business logic code and the complexity of the Customizing is interconnected or automated.

The creation of technical objects initially appears more complex than the top-down procedural approach. 
By means of autocompletion, use of code templates and quick fixes in the ABAP development tools in Eclipse (ADT), the ABAP code for the technical classes is created very quickly and easily, which means that the additional effort in coding is very limited.  
Once this pattern has been practiced, the advantages of this procedure far outweigh the disadvantage of the supposedly increased initial effort.  
Of course, the procedure must also be practiced in order to develop a certain development performance and efficiency.  
Please note the **[ADT Guide](https://1dsag.github.io/ADT-Leitfaden/)** from DSAG, which supports you in using ADT efficiently and across the board in the company.

### Full use of class-based exceptions for error handling

Use only class-based exceptions to handle errors. These should only be used in the event of errors and should not be misused for success or status messages from the application. Only technical restrictions from SAP force you to use classic exceptions in a few places.  
We advise you against using return codes as well as solely returning message tables such as BAPIRET2, as you often find in BAPI function modules. These concepts create the problem that the calling program has to check within the business logic process whether there is an error and therefore there is no clear separation of technical issues and business logic.
The use of exception classes enables significantly better separation here, and you can also bundle error handling in central locations due to the propagation of exceptions. Please also note the recommendations of the 
[Clean-ABAP Styleguide](https://github.com/SAP/styleguides/blob/main/clean-abap/sub-sections/Exceptions.md)

A developer trained in ABAP-OO defines in the conception phase the error situations that can occur in a (sub)package and, based on this, creates the corresponding exception classes with the error messages (as text ID or message-based).
When the business logic code is implemented and the errors need to be handled, the exception is raised at that point. The handling does not have to take place in each call layer as with function blocks, but can be done centrally in one place.
This ensures consistent handling and reduces effort when errors can occur in multiple places.

### Interfaces

By using interfaces, the definition of methods and their implementation are decoupled from each other. If an interface is used, the implementation of the class can be changed or made more flexible. The interface defines, so to speak, the contract between the user and the implementing class and thus "hides" the implementation (software hiding principle).  
For public methods that provide functions for other classes, you should always define interfaces and thus ensure that users only work with these interfaces. The creation of concrete objects is handled by a separate factory class or, in particularly simple cases, a factory method of the class, e.g.: ```ZCL_BUSINESS_LOGIC=>GET_INSTANCE( CompanyCode )``` [see SAP style guide](https://github.com/SAP/styleguides/blob/main/clean-abap/CleanABAP.md#prefer-multiple-static-creation-methods-to-optional-parameters)

Interfaces are also required for unit tests, since, for example, database accesses in unit tests have to be replaced by programmed test data. The database class implements an interface that is called in the product code. When the unit test is executed, instead of the database class, a so-called mocking class is called, which contains statically stored data, provides methods for local test data generation and returns it. The information on this can be found in chapter [Testing]({{ site.baseurl }}/testing/index).

### Vererbung

An important concept in object orientation is inheritance. A class can be derived from another class and thus inherit the properties of the parent class. An inheriting class has the attributes and methods of the parent class, but can add further specific methods or redefine inherited methods, i.e. receive an addition to the inherited implementation or even its own implementation of the method.  
When it comes to inheritance, the Liskov substitution principle must be observed and it must be carefully examined whether inheritance makes sense in the intended context. It is often better to use interfaces instead of inheritance or to use the delegation method and distribute different aspects of a class to different classes and regulate the interaction via a controller and the instances via a factory.  

## Object orientation in function blocks and form routines

Sometimes it is necessary that functionalities have to be implemented in given artifacts. E.g. function blocks in AIF, remote function blocks, form interface routines in Adobe Forms, etc.
In this case, these development objects serve as a wrapper and only call the actual functionality, which is then implemented in ABAP classes and their methods. The code in these development objects should be limited to technical coding only, such as data mapping, object instantiation, or minimal checks.
This in turn offers the advantage of possible reuse and implementation of unit tests.

## How to use SAP Code - Law of Demeter

The use of SAP code (classes, function blocks, BAPIs, etc.) or code from outside the package should always be in its own access layer. This then corresponds to a clean separation of concerns (S - Separation of Concerns).  
This corresponds to the object orientation design guideline ["Law of Demeter"](https://de.wikipedia.org/wiki/Gesetz_von_Demeter), which states that objects should only communicate with objects in their immediate surroundings.  
Even if these are shared elements, they should always be encapsulated with a class so that there is a central point of transition from internal to third-party code.  

Create classes whose task is to keep the application's program code free of any dependencies on the SAP code or on non-package code. This will also encourage reuse.  
If the creation of your own classes is oversized, in special cases the separation can also be done by calling the third-party code in private methods created specifically for this purpose. The interface definition should be based more on the caller and not on the called object. This makes it easier to replace the third-party code used later. Depending on the complexity, the mapping between internal and external code interfaces can be outsourced to separate methods.  
The goal here is to maintain control over dependencies and increase the maintainability of the software.

For reasons of testability, data access, e.g. CDS views or SAP function blocks, should be implemented in a separate database access layer, which enables decoupling of data access via dependency inversion for ABAP unit tests (see chapter Testing).

A helpful extension of these classes is the transformation of the classic exceptions, or return codes, used by SAP code for error handling, into exception classes.  
This separation is also an important prerequisite for the testability of an application.

## Testability through good design

Good structuring in the packages as well as in the objects are fundamental requirements for increasing the testability of the software. If the responsibilities of the components are clarified within the framework of a good architecture and the tasks are sensibly distributed among different objects, this makes the use of the ABAP Unit much easier.
As part of the aforementioned architecture and design decisions, test-relevant aspects must be included in order to be able to efficiently implement the ABAP unit, as the structure has a direct impact on testability.

If database accesses and accesses to SAP function blocks or classes are already encapsulated in a separate software layer and the instances are created via a factory that provides injection, it is very unproblematic for an experienced developer to test their own code via ABAP unit tests and to decouple database accesses and SAP functions via test mocks objects. This significantly reduces the effort required for unit test creation compared to an approach in which the test developer has to use techniques such as test seams in the code or has to rebuild the code to ensure the decoupling of the in-house development of SAP components in tests.

The procedure, recommendations and information for the ABAP Unit can be found in the [Testing SAP applications]({{ site.baseurl }}/testing/#testen) chapter.

## The importance of refactoring existing applications

The recommendations, technical methodologies and programming techniques described in this guide can be easily planned and applied when creating new applications. In addition, these can and should also be used to improve existing developments. This is called refactoring  

Refactoring should always be carried out when existing applications need to be changed or expanded. Time must be planned for this. Good tips for a sensitive approach to refactoring are described, for example, in [Clean-ABAP Styleguide](https://github.com/SAP/styleguides/blob/main/clean-abap/CleanABAP.md).

Refactoring not only describes the improvement of the code in detail, but can also be applied figuratively to the structure in the form of packages. Objects can be usefully distributed into new sub-packages. If your applications are not currently based on a structure organized by main packages, we recommend creating main packages that represent your main functionalities and previous packages can then be assigned to these packages according to their affiliation. It is possible to split packages that are too large into smaller packages, but the dependencies must be checked, clarified and, if necessary, eliminated. However, packet encapsulation and packet inspection help with this. These functionalities are explained in detail in the optional section [Basics of the package concept]({{ site.baseurl }}/abap/package_extended.md).
Improvements to existing software should occur continuously and in small steps and be backed up by tests. If this is integrated into the development process and part of the day-to-day development business, it will pay off with more maintainable and less error-prone software.

## A good architecture also needs clean code

After you have learned a lot about the architecture and structure of modern application development and methods for designing the software, read in the next section what properties Clean code has and receive our recommendations and tips on how modern and clean code (Clean code) can be achieved in application development. An application should not only have good architecture and structuring. It is equally important to create clean code and follow the Clean code principles. Because this supports the goal of modern and maintenance-friendly software.  
