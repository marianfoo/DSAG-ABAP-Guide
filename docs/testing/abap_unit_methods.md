---
layout: page
title: Basics of unit testing
permalink: /testing/abap_unit_methods/
parent: Software test with ABAP unit
nav_order: 1
---

{: .no_toc}
# Basics of ABAP Unit Tests

1. TOC
{:toc}

## Prerequisites for ABAP Unit Tests

Since the previous section addressed challenges and prerequisites—primarily of an organizational nature—the following section will focus on the technical aspects and considerations that must be taken into account in order to successfully implement ABAP unit tests.

### Separation of the Data Model, Business Logic, and Presentation Layer

Unfortunately, it has become common practice in the SAP environment for everything required for program execution to happen wherever it happens to fit. Data is enriched, processed, and output using additional SELECT statements. A double-click triggers the reading of additional data and displays a pop-up that informs the user about something. All of this happens in a single piece of software that was created as a business function in accordance with the described business requirement and implements it with everything necessary.  
This results in a code where, for example a method create_sales_order calls a BAPI that posts data and thereby creates an order number. In this classic, business-process-oriented development-which was standard for many years and is still in use today-there is no separation of concerns according to the “Separation of Concerns” principle.

A fundamental rule for professional work is that data retrieval, business logic, and data output (presentation layer) are technically separated within the application and do not intermingle in the code. In a unit test, there is no user who can click away an info message, which makes the automated testability of such all-in-one program components much more difficult.  

There are program areas that cannot be verified using unit tests. These include all program components that depend on a dialog or other presentation functions, such as the ALV Grid. Likewise, SAP functions should not be tested using custom unit tests.
Separating data retrieval, business logic, and display is always an improvement for software quality. Unit tests can be implemented more easily if existing programs are restructured (refactored) and written according to the rules of Clean ABAP, following the design principles of object-oriented programming (SOLID).

To avoid extensive revisions later, good application design is essential when implementing unit tests. Explanations are available in [Modern ABAP Development]({{ site.baseurl }}/abap/oo-design/#design-and-development-of-modern-sap-applications) and [Testability Through Good Design]({{ site.baseurl }}/abap/oo-design/#testability-through-good-design).

### Unit Tests Are Not Optional – Unit Tests as Part of the Definition of Done

> "First implement the feature – then we will do the Unit Tests (if there’s still time)".

Unfortunately, this statement is still commonly heard in day-to-day ABAP development projects. When time is tight, the focus is simply on delivering the functionality.
Expand your “Definition of Done” to include unit tests.  
In the long run, it will be extremely helpful to integrate the early creation of unit tests into the development process. Creating tests later on will hardly work due to (project) time constraints.
Every software developer should always have the opportunity to create high-quality software. Automated tests are an important part of this, even if these tests may be longer and more comprehensive than the program itself. This reflects the business requirements and complexity of the feature.

### TDD (Test-Driven Development)

Whenever the term “unit tests” comes up, the topic of Test-Driven Development, or TDD for short, almost inevitably follows. TDD is a programming methodology in which—to put it simply—one first defines which inputs to a function should produce which outputs. Only then is the function implemented. The previously defined behavior allows one to verify whether the desired functionality is present.

At this point, we are explicitly not discussing the Test-Driven Development method. Unit tests can also be used effectively even if this method was not followed. From our perspective, the most important thing is understanding how unit tests work and why they are important.

As the most important cornerstones of TDD, the following questions must be clarified in advance before the functionality is implemented:

* What functions is the overall function divided into?
* What interfaces do these functions have?
* What data is required to perform the tests?
* Which functions are not included in the tests and require appropriate test substitutes (mocks, stubs, etc.)?

Applying TDD strictly according to the textbook is not easy and requires some experience. However, simply having developers consider the points mentioned above ensures that many issues are identified early in the development process, thereby avoiding time-consuming (design) changes and rework — including retesting — later on.

## General Information on Unit Tests – Definitions and Explanations

### Getting Started

Unit tests are important. Creating, managing, and developing unit tests requires extensive knowledge that goes beyond simply writing ABAP code. This seems to contradict the statement that this chapter is intended for all programmers, regardless of their level of expertise. However, this contradiction is only apparent at first glance, because our goal with this chapter is to reach everyone. If someone is not yet proficient in object-oriented programming—or is not familiar with design patterns and other programming paradigms—then they should learn these skills. Unit tests can provide a good environment for learning techniques and subsequently applying them to production code. We aim to offer suggestions and guidance on this topic. Nevertheless, we can only provide limited information on this subject at this point.

{: .recommendation }
> - We recommend unit tests

#### Skills that are trained when working with unit tests

* Object-oriented design, e.g. loose coupling
* Creating testable designs (Inversion of Control & Dependency Injection)
* Agile principles and methods of software development e.g. (S.O.L.I.D)
* Test principles ( F.I.R.S.T )
* Creating small units

### What Exactly Are Unit Tests?

Unit tests call modularized units, such as methods or function modules, with defined inputs and compare the actual results with the expected results.

The following example demonstrates the procedure: There is a class with a method designed to determine the street and house number from a text. Unit tests are now created that use known errors to verify whether the expected result is obtained.

Call the method ZCL_ADDRESS->SEPARATE_HOUSENO_FROM_STREET with the input ABC-Street 13 and check whether the result is 13. If the result differs from the expected value, the unit test fails and generates an error message in the test environment.

The CL_ABAP_UNIT_ASSERT class provides several methods for checking the result. The best-known method is EQUALS. It checks whether the specified value is equal to the expected value. Other methods are discussed in the following chapter.

Unit tests are typically defined as local test classes associated with a global class. The unit tests are run only on the development system.

### When Are Unit Tests Useful?

When it comes to unit tests, there are generally two camps: Some say that all code must be tested with unit tests (100% code coverage). Others believe that unit tests are overrated.
We believe that unit tests are an integral part of everyday programming and should be used where they make sense.

Each team should determine for itself what “appropriate” means. Likewise, teams should assess whether a feature can be classified as “critical.” If there is a critical business function, then that feature should definitely be covered by unit tests.

Methods that involve complex logic and/or are business-critical are particularly well-suited for unit testing.

### Mocking

An important term that is frequently mentioned here is “mocking.” Generally speaking, mocking refers to the practice of replacing SAP objects—such as function modules or classes—that are not part of the unit test with stand-in objects. How mocking is achieved is covered in relevant ABAP courses and technical books; therefore, we will not go into further detail here due to the technical complexity involved.  
There are also various forms of mocking, which are briefly explained in the section on testing techniques.

### Test Levels

#### Method tests

Tests of individual methods, with a focus on ensuring that the methods function correctly. It is essential that these tests be run independently of the database.  
This definition often provides the initial basis for refactoring, since many methods perform multiple tasks. A large number of unit tests or extensive unit tests often indicate that you should break a method down into smaller parts.

#### Component Testing

Tests of entire classes or related components, such as a class and a BAPI for posting.
These tests are often database-dependent. Appropriate techniques should be used here to ensure a consistent database state for each test.

The relevant SAP frameworks are suitable for this purpose:

* CDS Test Double Framework (read access)
* ABAP SQL Test Double Framework (read and write access) see [Managing Dependencies with ABAP Unit](https://help.sap.com/docs/ABAP_PLATFORM_NEW/c238d694b825421f940829321ffa326a/04a2d0fc9cd940db8aedf3fa29e5f07e.html?locale=en-US)

#### Integration Tests

Integration tests involve testing parts of processes or entire processes to ensure that the components work together properly.
These tests are often characterized by the fact that preparing the initial data setup is time-consuming. The following scenarios are required: a customer with a delivery block, a material with no inventory but an incoming purchase order, and so on. A significant portion of the testing effort will need to be devoted to efficiently preparing this test data.

## Procedures and Methods

### Clean Islands

So-called Clean Islands can help illustrate what effective implementation of unit tests looks like.
These are packages or classes that serve as models of excellence in terms of software quality – and unit testing as well.
As such, they serve as a reference for teams, external stakeholders, and new colleagues to use as a model when developing new software.

### Modularizing Unit Tests

Unit tests consist of code that, just like production code, must be modularized, maintained, and extended.
It is almost always advisable to modularize a unit test into small methods, since it is inherent in the nature of testing that multiple test cases use identical input data or verification criteria.
The goal must be to make unit tests clearer and easier to maintain.

Procedure and recommendations for modularizing test code:

* Create a separate new test method for each method in your class.
* If there are different test cases for a method, create a separate test method for each case (e.g., success case and failure case).
* Do not duplicate methods. If you need code that has already been written, extract it into a new test method so you can reuse it.
* Be sure to review your existing tests regularly. An engine capable of generating test data in various required business scenarios will be a great asset when creating tests.

There are the following additional options that can also be used for modularization:

* Methods for assembling dependent classes
* Methods for generating test data
* Methods for modularizing tests

### Code Coverage

Development tools allow you to track which sections of code were executed during unit tests.
The goal should be 100% code coverage.

For existing classes where separation was not carefully considered, 100% test coverage is nearly impossible to achieve.
You must weigh the effort of refactoring against the benefits.
If a class does not have 100% test coverage, it is certainly not a major issue, but it makes it easier to assess how reliable the unit tests for a module are.
If there is a class that contains 100% business logic, then with 100% test coverage you can be fairly certain that this class works as it should.
However, if a class consists of a mix of business logic and data presentation, it is difficult to determine whether parts of the code could not be tested well via unit tests or whether they were simply forgotten.


{: .note }
> * [Unit tests in ABAP](https://help.sap.com/docs/ABAP_PLATFORM_NEW/c238d694b825421f940829321ffa326a/08c60b52cb85444ea3069779274b43db.html?locale=en-US)
> * [Sample chapter "ABAP To The Future" (Paul Hardy): ABAP Unit and Test Driven Development](https://tinyurl.com/tddph2)
> * [SAP Help "ABAP Unit in Test-Driven Development"](<https://help.sap.com/doc/saphelp_nw75/7.5.5/en-US/4e/c2efe26e391014adc9fffe4e204223/content.htm?no_cache=true>)
> * [SAP-Community Blogs: Unit Testing ](https://community.sap.com/t5/forums/searchpage/tab/message?advanced=false&allow_punctuation=false&filter=location&location=blog-board:application-developmentblog-board&q=abap%20unit%20tests)
> * [GIVEN - WHEN - THEN (Martin Fowler)](https://martinfowler.com/bliki/GivenWhenThen.html)
> * [CACAMBER (Dominik Panzer)](https://github.com/dominikpanzer/cacamber-BDD-for-ABAP)
> * [Agile ABAP development by Winfried Schwarzmann - Reinwerk](https://www.rheinwerk-verlag.de/agile-abap-entwicklung)
> * [ABAPKoans by Damir Majer](https://github.com/damir-majer/ABAPKoans)
> * [ABAP Unit Tests - SAP Learning Hub](https://learning.sap.com/learning-journeys/acquire-core-abap-skills/implementing-code-tests-with-abap-unit_b23c7a00-c2e8-406d-8969-b00db3f1fd87)
