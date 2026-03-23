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

## Requirements for ABAP unit tests

After addressing challenges and requirements of a primarily organizational nature in the previous section, in the following section we will address technical aspects and concerns that must be taken into account in order to successfully use ABAP unit tests.

### Separation of data model, business logic and presentation layer

Unfortunately, in the SAP environment it has become established that everything that is needed for the program to run happens wherever it is convenient. The data is enriched, processed and output with additional SELECTS. When you double-click, more data is read and a popup is displayed informing the user about something. All of this happens in a piece of software that was created as a business function according to the described business requirement and implements it with everything that is necessary.  
This creates code in which, for example, a method ```create_sales_order``` calls a BAPI that posts data and thus creates an order number. In this classic, business process-oriented development, which was common practice for many years and is still in use today, there is no separation of various concerns according to the “Separation of Concerns” principle. 

A fundamental rule of professional work is that data acquisition, business logic and data (presentation layer) are technically separate in the application and do not mix in the code. In a unit test, there is no user who can click away an information message, which makes the automated testability of such all-in-one program parts very difficult.  

There are program areas that cannot be checked using unit tests. This includes all program parts that depend on a dialog or other presentation functions, such as ALV Grid. Likewise, SAP functions should not be tested using your own unit tests. 
Separating data acquisition, business logic and display is definitely an improvement for software quality. Unit tests can be implemented more easily if existing programs are restructured (refactored) and written according to the rules of Clean-ABAP and follow the design principles of object orientation (SOLID).

In order to avoid extensive revision of created software, a good design of the application is essential for the implementation of unit tests. You can find explanations in chapter [Modern ABAP Development]({{ site.baseurl }}/abap/oo-design/#design-and-design-modern-sap-applications) and section [Testability through good design]({{ site.baseurl }}/abap/oo-design/#testability-through-good-design).

### Unit tests are not optional - unit tests as part of the definition of done

> "First implement the function - then we'll do the unit tests (if there's still time)."

Unfortunately, this sentence is still very often found in ABAP development projects in everyday life. When there is time pressure, the focus is on delivering the functionality. 
Expand your “Definition of Done” and include unit tests.  
In the long term, it will be extremely helpful to integrate the creation of unit tests early into the development process. Creating tests later will hardly work due to (project) time pressure.
Every software developer should always have the opportunity to create high-quality software. Automatic tests are an important part of this, even if these tests can be longer and more comprehensive than the actual program. This is an expression of the business requirement and complexity of the function.

### TDD (Test-Driven-Development)

When the keyword “Unit Tests” is mentioned, the topic of _Test Driven Development_, or _TDD_ for short, almost inevitably comes up. TDD is a programming procedure in which - in simple terms - it is first defined which inputs of a function should lead to which results. Only then is the function implemented. The previously defined behavior can be used to check whether the desired functionality is present.

This point is explicitly not about the Test Driven Development method. Unit tests can be used sensibly even if this method was not used. From our perspective, the most important thing is to understand how unit tests work and what importance they have.

As the most important cornerstones of TDD, the following questions must be clarified in advance before the functionality is implemented:

* Which functions is the overall function divided into?
* which interfaces have these functions
* what data is needed to carry out the tests
* which functions are not tested and require appropriate test replacement (mocks, stubs...)

Using TDD based on pure teaching is not easy and requires some experience. But at least the approach of thinking about the above-mentioned points as a developer means that many questions arise in an early phase of development and therefore there are no later complex (concept) changes and rework with re-tests.

## General information about unit tests - definitions and explanations

### Introduction

Unit tests are important. Creating, managing, and developing unit tests requires extensive knowledge beyond just writing ABAP. This contradicts the statement that this chapter is aimed at all programmers, regardless of their level of knowledge. However, this is only contradictory at first glance, because we want to reach everyone with this chapter. If someone doesn't know how to program object-oriented well or at all, or isn't familiar with design patterns and other programming paradigms, then this should be learned. Unit tests can provide a good environment to learn techniques and then transfer them to productive code.
We want to provide suggestions and assistance. However, we can only provide limited information on this topic at this point.

{: .recommendation }
> - We recommend unit tests

#### Skills that are trained when working with unit tests

* Object-oriented design, e.g. loose coupling
* Creating testable designs (Inversion of Control & Dependency Injection)
* Agile principles and methods of software development e.g. (S.O.L.I.D)
* Test principles ( F.I.R.S.T )
* Creating small units

### What exactly are unit tests?

Unit tests are functions that call modularized units (methods, function blocks) or entire processes with specified functions and compare the result with the expected specifications. 

The following example demonstrates the procedure: There is a class with a method that is supposed to determine the street and house number from a text. Unit tests are now created that use known errors to test whether the expected result is determined.

Call the method ```ZCL_ADDRESS->SEPARATE_HOUSENO_FROM_STREET``` with the input ```ABC-Straße 13``` and check if the result is ```13```. If the result deviates from the expected value, the unit test fails and generates an error message in the test environment.

There are a number of methods of class ```CL_ABAP_UNIT_ASSERT``` for checking the result. The most popular method is ```EQUALS```. It checks whether the specified value is equal to the expected value. There are other methods, which we will discuss in the following chapter.

Unit tests are usually defined as local test classes to a global class. The unit tests are only carried out in the development system. 

### When do unit tests make sense?

When it comes to unit testing, there are usually two camps: Some say that all coding must be checked with unit tests (100% code coverage). The others are of the opinion that unit tests are overrated.
We believe that unit tests are part of everyday programming and should be used where they make sense. 

Each team should find out for themselves what is meant by “useful”. It should also be assessed whether a functionality can be classified as “critical”. If there is a critical business function, then the functionality should definitely be covered via unit tests.

Methods that have complex logic and/or are business-critical are particularly ideal for unit tests. 

### Mocking

A very important term that is often mentioned here is so-called mocking. In general, mocking means that objects such as function blocks or classes from SAP, which are not part of the unit test, are replaced by substitute objects. How mocking is achieved is taught in relevant courses on ABAP or specialist books, so we will not go into it further here due to the level of technical detail.  
There are also different forms of mocking, which are briefly explained in the testing techniques section.

### Test levels

#### Method tests

Tests of individual methods with the focus on ensuring that the methods work correctly. The tests should definitely be run independently of the database.  
This definition often provides the initial basis for refactoring, as many methods carry out multiple tasks.
A large number or very extensive unit tests often indicate that you should decompose a method.

#### Component tests

Tests of entire classes or related components such as a class and a BAPI for updating.
These tests are often database dependent. Appropriate techniques should be used here to create a consistent database state for each test.  
The corresponding frameworks from SAP are suitable for this:

* CDS Test Double Framework (Read Access)
* ABAP SQL Test Double Framework (Read and Write Access)    
See [Managing Dependencies with ABAP Unit](https://help.sap.com/docs/ABAP_PLATFORM_NEW/c238d694b825421f940829321ffa326a/04a2d0fc9cd940db8aedf3fa29e5f07e.html?locale=en-US)

#### Integration tests

During integration tests, parts of or entire processes are tested to ensure the interaction of the components. 
These tests are often characterized by the fact that the preparation of the initial data is laborious. It is required: customer with a delivery block, material without stock but with an incoming order, etc. Here, a large part of the tests will have to be spent on the efficient provision of this test data. 

## Approach and methodologies

### Clean Islands

So-called _Clean Islands_ can help to convey what a good implementation of unit tests can look like.
These are packages or classes that have exemplary status in terms of software quality - and also unit tests.
They therefore serve as a reference for teams, external parties and new colleagues in order to create new software.

### Modularizing unit tests

Unit tests consist of code that, like product code, needs to be modularized, maintained and extended. It is almost always advisable to modularize a unit test into small methods, since the nature of the tests means that multiple cases use identical starting data or validations. The goal must be to make the unit tests clearer and easier to maintain.

*Procedure and recommendations for modularizing test code:*

* Create a separate new test method for each method of your class.
* If there are different test cases for a method, create your own test method for each case (e.g. success case and error case)
* Do not copy any method. If you need code you've already written, extract it into a new test method so you can reuse it.
* Always check the previous tests. An engine that is able to create test data in the various required technical constellations will serve you well when creating tests.

There are the following additional options that can also be used for modularization:

* Methods for composing dependent classes
* Methods for building test data
* Methods for modularizing tests

### Code coverage

The development tools can be used to track which code sections were run through when executing the unit tests. The goal should be 100% code coverage.

For existing classes where separation was not taken into account, 100% test coverage is hardly achievable. You have to balance the effort of refactoring with the benefits. If a class doesn't have 100% test coverage, it's certainly not a bad thing, but it makes it easier to assess how trustworthy unit tests are for a module. If there is a class that contains 100% business logic, then with 100% test coverage you can be relatively confident that that class works the way it is supposed to work. However, if a class consists of a mix of business logic and data presentation, then it is difficult to determine whether pieces of code could not be unit tested well or whether they were simply forgotten.


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
