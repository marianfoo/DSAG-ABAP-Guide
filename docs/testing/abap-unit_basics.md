---
layout: page
title: ABAP Unit - testing techniques
permalink: /testing/abap-unit_basics/
parent: Software test with ABAP unit
nav_order: 2
---


{: .no_toc}
# ABAP Unit: Testing Techniques

1. TOC
{:toc}

Technical Fundamentals: Object Level

## What Can Be Tested Using ABAP Unit?

> {: .Zitat }
> “You can’t test that”  

Basically almost everything can be tested with ABAP Unit. There are program areas that cannot be checked using ABAP unit tests. This includes all program parts that rely on a dialog or display data (e.g. ALV grid).
For everything else, there are options to secure these programs with ABAP unit tests. Initially this will be complex and tedious. But the effort will be worth it and will pay off quickly. It is definitely possible to secure BAPIs, BAdIs, RFCs and IDOCs with Unitests.  

## Handling Data in Unit Tests

The traditional system configuration in the development environment, which includes a development and a test tenant, poses a challenge to the smooth execution of component or integration tests, as these tests typically rely on data from the database when standard unit testing methodologies are not used.  
The same applies to scenarios in which there is no data in the database on the development system.

{: .recommendation }
> Create your ABAP unit tests independently of the database so that they can run in any client using dependency injection and mocks and produce the same results.  
> If this approach is not followed—for example, if tests are developed in client x and executed in client y—the tests would not provide reliable results and would therefore be run less frequently or not at all.
> The same applies to unit tests that depend on a specific data configuration on the test system.
> According to unit testing methodology, direct database queries should therefore be avoided by using mocking or an injection framework.
> The [advanced techniques]({{ site.baseurl }}/testing/abap_unit_advanced/) section explains how to achieve this independence.

## Test Environment

ABAP Unit tests can be created and used in ABAP Development Tools or the SAP GUI development environment (SE80, SE24). The procedures differ only in minor details.
ADT is clearly recommended here, as [Test Relations](https://www.youtube.com/watch?app=desktop&v=yiKhKlQz89Y&t=14s) can also be used here.  
However, the techniques required for creation are very similar. Unit tests created in SE80 can also be maintained and tested in Eclipse, and vice versa. The keyboard shortcut for running unit tests is **CTRL + SHIFT + F10** in both tools. Some functions in the ABAP Workbench are accessible only via the menu, whereas in ADT there is a keyboard shortcut for them.

The following section covers these topics:

* Creating unit tests
* Run unit tests
* Result display
* Code coverage (Code Coverage)

We assume that you have experience with the respective tool. For this reason, there are no step-by-step instructions, just a brief overview of the most important commands.

### Creating a local test class in ADT

* Open Global Class
* Navigate to the "Test Classes" view
* Template "testClass"

### Keyboard shortcuts in ADT

* **Ctrl + Shift + F9:** Show Unit Test Preview
* **Ctrl + Shift + F10:** Run unit tests
* **Ctrl + Shift + F11:** Run unit tests with coverage
* **Ctrl + Shift + F12:** Open unit test execution dialog
* **Ctrl + Shift + F2:** Run ATC check with standard variant

### Keyboard shortcuts in the workbench

* **Ctrl + Shift + F10:** Run unit tests
* **Ctrl + Shift + F11:** Show local test classes (form-based editor only)
* **Ctrl + F11:** Show local test classes (code-based editor only)

## Testing methodologies and principles

### GIVEN – WHEN – THEN

GIVEN – WHEN – THEN is a style used to write unit tests. GIVEN specifies the conditions under which the test should run. WHEN describes the action to be performed, and THEN describes the expected result.

Based on our example with the house number, the wording could be:\
GIVEN is the street name "ABC-Straße 13"\
WHEN the house number is determined from this string\
THEN should be the house number "13".

### Clean Code in Unit Tests

It is often believed that there is no need to adhere to code quality guidelines (Clean ABAP, naming conventions, modularization, etc.) in unit tests. Poor maintainability and quality in unit tests will result in the tests not being further developed and becoming useless. Duplicate code and a lack of modularization should be avoided here just as much as in production code.

### Keep Unit Tests Clean

It is also essential that all unit tests run successfully. Do not be careless here; prioritize tasks that require fixing the business code or the unit test until all tests run without errors again.  

### Handling Exceptions

[SAP recommends](https://help.sap.com/doc/saphelp_crm700_ehp03/7.0.3.11/de-DE/dd/587324e2424b14ab5afb3239a77a8d/frameset.htm): If the code under test is capable of throwing an exception, the test method itself should not handle it, but declare it in its signature (apart from provoked exceptions), so that the test case fails if it occurs at runtime.


### Creating a Unit Test Class

A unit test class has a few special features in contrast to a common ABAP class. In this chapter we describe how the unit test class is structured and what properties it has.

* General procedure
* Risk level
* Duration
*Plant in
  * Eclipse
  * SE80
* SETUP
* TEARDOWN
* FOR TESTING

### General Procedure

Each class has an include file in which multiple local classes and test classes can be defined. A test class has attributes that provide information about the risk level and the duration of the tests. Each test class has test methods marked with the suffix FOR TESTING. Test methods are executed in random order and must not be dependent on one another.

In a test method, a (public) method of the class under test is executed and compared with an expected result. If the result matches the expectation, the test is successful. The instance of the class under test is called F_CUT or CUT. CUT stands for Code Under Test. Before executing the tests, the SETUP method can optionally be executed to perform preparations for the test case (e.g., creating the CUT instance). After executing a test method, cleanup tasks can be performed in the TEARDOWN method. Any number of other methods or classes can be defined to support the tests.

### Risk Level

Use the RISK LEVEL attribute to define the risk level of the test cases

Follow SAP’s guidelines regarding risk levels:
* CRITICAL - a test changes system settings or customizing data (default)
* DANGEROUS - a test changes persistent data
* HARMLESS - a test does not change system settings or persistent data

As a general rule, you should avoid writing tests that make actual changes to the database. This is often a sign of poor dependency management or failure to replace dependencies. Your goal should be to classify as many tests as possible as harmless. This is possible using the frameworks provided by SAP for mocking database tables and CDS views—see the section on Mocking.

### Duration

Use the DURATION attribute to specify the expected duration of the test cases.
The following categories are available. The default duration in seconds is shown in parentheses:
* LONG (3600 sec)
* MEDIUM (300 sec)
* SHORT (60 sec)

If a test exceeds the value defined in the system, it is terminated and interpreted as “failed”.  

You can configure the various runtimes using transaction SAUNIT_CLIENT_SETUP. Here, too, the clear goal is that your tests must run quickly so that they can be executed repeatedly.

### ASSERT

Within a test method, the result of a test method can be checked using the methods of the CL_ABAP_UNIT_ASSERT class. The class has many methods that can be used for such comparisons. The most commonly used methods are:
* ASSERT_EQUALS
* ASSERT_FALSE
* ASSERT_BOUND

An ASSERT is performed to compare the calculated value with the expected value. In other words, you call a method of the class under test and compare the result with what you expect as output. The parameters of the corresponding ASSERT method always have the same names:
* EXP is the expected value (EXPECTED VALUE)
* ACT is the value determined in the Test (ACTUAL VALUE)
*
The expectation may be that the result has a specific value, a specific table row is present in the result table, or an object has been instantiated. The result does not have to come directly from a method. You can also execute multiple methods of the test class and check the value of a global attribute at the end.

### Example test class

The following example shows the test class `LTCL_VERIFY_ADDRESSES` to the global class `ZCL_ADDRESS`. The `SPLIT_ADDRESS` method is responsible for dividing a string containing the address and house number into the components `Straße` and `Hausnummer`.

```
CLASS ltcl_verify_addresses DEFINITION FINAL FOR TESTING
  DURATION SHORT
  RISK LEVEL HARMLESS.

  PRIVATE SECTION.
    DATA cut TYPE REF TO zcl_address.
    METHODS:
      setup,
      strasse_17_juni FOR TESTING,
      abc_strasse FOR TESTING,
      parkallee FOR TESTING.
ENDCLASS.


CLASS ltcl_verify_addresses IMPLEMENTATION.

  METHOD strasse_17_juni.
    DATA(address) = cut->split_address( |Straße des 17. Juni 134| ).
    cl_abap_unit_assert=>assert_equals(
      exp = |Straße des 17. Juni|
      act = address-street ).
    cl_abap_unit_assert=>assert_equals(
      exp = |134|
      act = address-house_no ).
  ENDMETHOD.

  METHOD abc_strasse.
    DATA(address) = cut->split_address( |ABC-Straße 89| ).
    cl_abap_unit_assert=>assert_equals(
      exp = |ABC-Straße|
      act = address-street ).
    cl_abap_unit_assert=>assert_equals(
      exp = |89|
      act = address-house_no ).
  ENDMETHOD.

  METHOD parkallee.
    DATA(address) = cut->split_address( |Parkallee 11 a-f| ).
    cl_abap_unit_assert=>assert_equals(
      exp = |Parkallee|
      act = address-street ).
    cl_abap_unit_assert=>assert_equals(
      exp = |11 a-f|
      act = address-house_no ).
  ENDMETHOD.

  METHOD setup.
    cut = NEW #( ).
  ENDMETHOD.

ENDCLASS.
```


#### Methods for composing dependent classes

In the case of complicated test cases, extensive preparatory work may need to be done so that the actual tests can be carried out. There should be as few dependencies as possible, but unfortunately dependencies cannot always be completely avoided. Auxiliary methods can help prepare the necessary setup for a test.

**Example:**

The `prepare_setup( ).` method creates two instances that are necessary to verify the address:
* Street directory
* Postal code catalog

#### Auxiliary methods for building test data

If test data consists of many components (header data, item data, partners, materials, etc.), then compiling this data can be extensive. Appropriate auxiliary methods are absolutely necessary here to make compilation easier.

**Example:**

The `get_setup_for_document( doc_id = c_nice_docuemt_id ).` method provides all the necessary data associated with the requested document.
{: .note }
If you need to access documents from the database, maintain central constants with descriptive names and explanations.  Otherwise, at some point you will no longer know what peculiarities Exhibit 564 had.  
```ABAP
CONSTANTS:  "! Sales order that has one item, Material ..., not released ...
             c_order_one_iten_ok
```


#### Methods for Modularizing Tests

When conducting tests, it may be necessary to test not just one aspect of the result, but many. Such logic can usually be effectively delegated to methods.

**Example:**

The `verify_address_is_valid( address = data )` method not only checks whether the street name and house number were successfully extracted, but also whether the ZIP code consists of five digits and matches the city name.

### Testing Private, Protected, and Public Methods
Some believe that only public methods should be tested. Code coverage can be used to analyze whether all sections of code have been executed. However, providing the necessary data can be very time-consuming, so it may make sense to test smaller units (private and protected methods). Furthermore, extensive data sets can “dilute” the purpose of a unit test. Tests for private methods can also help to locate the source of an error more quickly.

**Example: Address Processing:**

Let us assume we have a class that accepts and analyzes addresses. We have already encountered the method `SEPARATE_HOUSENO_FROM_STREET`. There is also a method called `CHECK_POST_CODE`, which is designed to ensure that the ZIP code is 5 digits long and consists only of numbers. If both private methods are called by the public method `CHECK_ADDRESS`, we always have to pass a complete address for testing. It is simpler and clearer to test the private methods separately. This way, you can test the basic functionality of the `SEPARATE_HOUSENO_FROM_STREET` method.

### Extending Unit Tests

If we look at the example of determining a house number, there are many pitfalls that can lead to unexpected results. However, we do not know in advance which inputs will result in an incorrect output. We only become aware of them when users complain about receiving an incorrect result. In this case, the inputs that led to incorrect outputs can be included in a unit test. After the code is modified, all previously defined unit tests are run, and the developer can be sure that everything works as before.

#### Example test class with helper method

This example uses the demo class from the previous chapter, which divides an address into its street and house number components. This class has three testing methods for individual variants. Since the schema is always the same, it would be easier if the street names and house numbers were put together and then tested in one method.

So for example:

```
verify_address( strasse = 'Beispielstraße'  house_number = '23' ).
```

The test class could then look like this:

```
CLASS ltcl_verify_addresses_helper DEFINITION FINAL FOR TESTING
  DURATION SHORT
  RISK LEVEL HARMLESS.

  PRIVATE SECTION.
    DATA cut TYPE REF TO zcl_address.
    METHODS:
      setup,
      verify_address
        IMPORTING
          street   TYPE string
          house_no TYPE string,

      test_german_standards FOR TESTING.
ENDCLASS.


CLASS ltcl_verify_addresses_helper IMPLEMENTATION.

  METHOD test_german_standards.

    verify_address( street = |Straße des 17. Juni| house_no = |134| ).
    verify_address( street = |ABC-Straße| house_no = |89| ).
    verify_address( street = |Parkallee| house_no = |11 a-f| ).
  ENDMETHOD.

  METHOD setup.
    cut = NEW #( ).
  ENDMETHOD.

  METHOD verify_address.

    DATA(address_string) = |{ street } { house_no }|.
    DATA(address_result) = cut->split_address( address_string ).
    cl_abap_unit_assert=>assert_equals(
      exp = street
      act = address_result-street
      msg = |Streetname should be { street }| ).
    cl_abap_unit_assert=>assert_equals(
      exp = house_no
      act = address_result-house_no
      msg = |House number should be { house_no }| ).

  ENDMETHOD.

ENDCLASS.
```

The test class now contains only the single test method `TEST_GERMAN_STANDARDS`, in which all tests are performed.

There is a helper method `VERIFY_ADDRESS` that takes a street name and a house number, combines them, and then has them split again by the method under test, `SPLIT_ADDRESS`. Since a test case no longer corresponds 1:1 to a test method, the parameter `MSG` from `CL_ABAP_UNIT_ASSERT=>ASSERT_EQUALS` was used to directly point out the faulty test case.

The test class is now much clearer, and the test cases are easily identifiable at a glance.

This approach allows you to continue running tests that follow a different structure.

Note: This is not a recommendation to place all tests within a single test method. The example is merely intended to demonstrate that helper methods can be used to make unit tests more compact, easier to maintain, and more readable.

### Test Environment

ABAP Unit tests can be executed in ADT as well as in the SAP GUI and their results can be analyzed.
ADT is clearly recommended here, as [Test Relations](https://www.youtube.com/watch?app=desktop&v=yiKhKlQz89Y&t=14s) can also be used here.

### Resolving Dependencies with Mocking, Faking, Stubbing and Spying

An important characteristic of testable code is that (business) logic, data retrieval, and presentation are strictly separated. Once this is ensured, dependent classes can be replaced with non-functional objects. These objects can serve different purposes and are named accordingly. The following types are possible:
* Mock
* Stub
* Faker
* Spy

A **Mock** object is an object that can dynamically respond to the caller’s inputs. For example, a mock object can simulate a query in an external system or the database and provide the desired data depending on the test case.

A **Stub** is an object with a minimal implementation of the methods necessary for testing. This object exists solely to ensure the error-free invocation of the methods under test.

A **Fake** object provides necessary data according to a simplified algorithm. For example, the real object might perform an extensive ZIP code validation, verifying geodata, districts, and ZIP codes based on various services. The corresponding fake could perform simple checks that are sufficient for running the tests.

A **Spy** object can incorporate features of stubs, fakes, and mocks, but additionally takes on the function of logging accesses. For example, a spy could be called during testing; however, the result is not checked directly, but only whether this method was called. This type is often used to ensure that emails or other messages would have been sent during certain actions.

* [Martin Fowler – Mocks Aren’t Stubs](https://www.martinfowler.com/articles/mocksArentStubs.html)

#### Test Doubles

The use of test doubles is necessary when there are dependencies that have not been sufficiently resolved or could not be resolved. With appropriate test double frameworks, the results of database accesses or function calls can be simulated.

Test double frameworks are usually cumbersome to use and can be confusing. Input parameters and desired results must be specified through numerous definitions and method calls. If possible, eliminate dependencies to avoid test doubles; however, this is not always possible. The [advanced techniques]({{ site.baseurl }}/testing/abap_unit_advanced/) section provides further information about test double frameworks.

#### Automated, Regular Runs of Unit Tests
There are several ways to run unit tests on a regular basis.

- Program RS_AUCV_RUNNER
- ATC runs
- Rest service (Communication Scenario SAP_COM_0735)

{: .recommendation }
> Schedule unit testing of a system regularly and create notifications for it.
> It should be part of every developer's morning routine to check whether all tests are error-free so that this can be discussed daily if necessary.


## Do's & Dont's
* If in doubt, create one more unit test
+ check less in one test
* No longer use or replace class CL_AUNIT_ASSERT because it is obsolete. The CL_ABAP_UNIT_ASSERT class must be used.
