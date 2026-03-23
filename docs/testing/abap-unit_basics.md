---
layout: page
title: ABAP Unit - Testtechniken
permalink: /testing/abap-unit_basics/
parent: Software test with ABAP unit 
nav_order: 2
---


{: .no_toc}
# ABAP Unit: Testtechniken

1. TOC
{:toc}

Technical basics at object level

## What can be tested using the ABAP unit?

> {: .Zitat }
> “You can’t test that”  

Basically almost everything can be tested with ABAP Unit. There are program areas that cannot be checked using ABAP unit tests. This includes all program parts that rely on a dialog or display data (e.g. ALV grid).
For everything else, there are options to secure these programs with ABAP unit tests. Initially this will be complex and tedious. But the effort will be worth it and will pay off quickly. It is definitely possible to secure BAPIs, BAdIs, RFCs and IDOCs with Unitests.  

## Handling data in unit tests

The classic system configuration in the development system with a development and a test client represents a hurdle for the smooth running of component or integration tests, as these usually depend on data from the database if common unit test methodologies are not used.  
This applies analogously to scenarios in which there is no data in the database on the development system. 

{: .recommendation } 
> Create your ABAP unit tests independently of the database so that they can run in every client using dependency injection and mocks and deliver the same result.  
> If this procedure is not used and the tests are developed in client x and executed in client y, the tests would not provide any reliable information and would therefore be carried out less often or not at all.
> The same applies to unit tests, which depend on a data constellation on the test system.
> According to the unit test methodology, direct database queries using mocking or injection frameworks should be avoided.
> You can find out which techniques will support you in achieving this independence here in section [Advanced techniques](#abap_unit_advanced)

## Test Environment

The ABAP unit tests can be created and used from the ABAP development tools or the SAP-GUI development environment (SE80, SE24). The procedure only differs in small details.
ADT is clearly recommended here, as [Test Relations](https://www.youtube.com/watch?app=desktop&v=yiKhKlQz89Y&t=14s) can also be used here.  
However, the techniques required to create them are very similar. Unit tests created in SE80 can also be maintained and tested in Eclipse and vice versa. The key combination for running the unit tests in both tools is **CTRL + SHIFT + F10.** Other functions in the ABAP Workbench can sometimes only be accessed through the menu, while there is a key combination for this in the ADT.

The following section covers these topics:

* Creating unit tests
* Run unit tests
* Ergebnisanzeige
* Codeabdeckung (Code Coverage)

We assume that you have experience with the respective tool. For this reason, there are no step-by-step instructions, just a brief overview of the most important commands.

### Creating a local test class in ADT

* Open Global Class
* Springen zur View "Test Classes"
* Template "testClass"

### Keyboard shortcuts in ADT

* **Ctrl + Shift + F9:** Unit Test Preview anzeigen
* **Ctrl + Shift + F10:** Run unit tests
* **Ctrl + Shift + F11:** Run unit tests with coverage
* **Ctrl + Shift + F12:** Open unit test execution dialog
* **Ctrl + Shift + F2:** Run ATC check with standard variant

### Keyboard shortcuts in the workbench

* **Ctrl + Shift + F10:** Run unit tests
* **Ctrl + Shift + F11:** Show local test classes (form-based editor only)
* **Ctrl + F11:** Show local test classes (code-based editor only)

## Testing methodologies and principles

### GIVEN - WHEN - THEN

GIVEN-WHEN-THEN is a style for formulating unit tests. GIVEN specifies a condition under which the test should take place. WHEN describes the action that will be taken and THEN describes the expected result.

Based on our example with the house number, the wording could be:\
GIVEN is the street name "ABC-Straße 13"\
WHEN the house number is determined from this string\
THEN should be the house number "13".

### Clean Code in unit tests

You often come across the attitude that it is not necessary to adhere to code quality rules in unit tests (CleanABAP, naming conventions, modularization, ...). Poor maintainability and quality in unit tests will result in the tests not being further developed and becoming useless. Duplicate code and a lack of modularization should be avoided here as well as in productive code.

### Keep unit tests clean

It is also imperative to carry out all unit tests successfully. Don't be careless here and prioritize tasks that require fixing the business code or unit test until all tests are running error-free again.  

### Exception handling

[SAP empfiehlt](https://help.sap.com/doc/saphelp_crm700_ehp03/7.0.3.11/de-DE/dd/587324e2424b14ab5afb3239a77a8d/frameset.htm): If the code under test is capable of throwing an exception, the test method itself should not handle it, but declare it in its signature (apart from provoked exceptions), so that the test case fails if it occurs at runtime. 


### Building a unit test class

A unit test class has a few special features in contrast to a common ABAP class. In this chapter we describe how the unit test class is structured and what properties it has.

* general process
* Risklevel
* Duration
*Plant in
  * Eclipse
  * SE80
* SETUP 
* TEARDOWN
* FOR TESTING

### General process

Each class has an include in which several local classes and test classes can be defined. A test class has attributes that say something about the _danger_ (risk level) and the _duration_ (duration) of the tests. Each test class has test methods that are identified as such with the addition _FOR TESTING_. Test methods are executed in random order and must not depend on each other.

In a test method, a (public) method of the class under test is executed and compared with an expected result. If the expectation matches, then the test is successful. The instance of the class under test is called _F_CUT_ or _CUT_. _CUT_ stands for _Code Under Test_. Before executing the tests, the _SETUP_ method can optionally be executed, in which preparations for the test case can be made (e.g. the creation of the _CUT_ instance). After executing a test method, cleanup work can be carried out in the _TEARDOWN_ method. Any number of other methods or classes can be defined to support the tests.

### Risk Level

With the addition _RSIK LEVEL_ you define the risk level of the test cases

Follow the SAP guidelines for risk levels:
* CRITICAL - a test changes system settings or customizing data (default)
* DANGEROUS - a test changes persistent data
* HARMLESS - a test does not change system settings or persistent data

In general, you should avoid writing tests that make real changes to the database. This is often an indicator of a lack of management of dependencies or their exchange. Your goal must be able to define as many tests as _Harmless_. This is possible with the help of the frameworks provided by SAP for mocking database tables and CDS views. See section [Mocking..](Mocking, faking, spying und stubbing)

### Duration

You use the addition _DURATION_ to define the expected runtime of the test cases. 
The following categories are possible. The preset duration in seconds is shown in the brackets:
* LONG (3600 sec)
* MEDIUM (300 sec)
* SHORT (60 sec)

If a test exceeds the value defined in the system, the test is aborted and interpreted as "failed".   

You can set the different runtimes using transaction SAUNIT_CLIENT_SETUP. Here too, the clear goal is that your tests must be fast so that they can be run again and again. 

### ASSERT 

Within a test method, the result of a test method can be checked using the methods of the class _CL_ABAP_UNIT_ASSERT_. The class has many methods that can be used for appropriate comparisons. The most commonly used methods are:
* ASSERT_EQUALS
* ASSERT_FALSE
* ASSERT_BOUND

An _ASSERT_ is performed to compare the determined value with the expected value. So you call a method of the class under test and compare the result with what you expect as output. The parameters of the corresponding ASSERT method always have the same name:
* EXP is the expected value (EXPECTED VALUE)
* ACT is the value determined in the test (ACTUAL VALUE)
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
* Postleitzahlenkatalog

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


#### Auxiliary methods for modularizing tests

Testing may require testing not just one aspect of the result, but many. Such programming can usually be easily outsourced to methods.

**Example:**

The `verify_address_is_valid( address = data )` method not only checks whether the street name and house number were successfully extracted, but also whether the postal code consists of five numbers and matches the place name.

### Testing private, protected and public methods
There is an opinion that only public methods should be tested. The code coverage can be used to analyze whether all code sections have been passed through.
However, providing the necessary data can be very time-consuming, so it may make sense to test the smaller units (private and protected methods). In addition, extensive data constellations “dilute” the purpose of a unit test. Private method tests can also help pinpoint the source of an error more quickly. 

**Example address preparation:**
Let's say we have a class that receives and parses addresses. We have already gotten to know one method `SEPARATE_HOUSENO_FROM_STREET`. In addition, there is a method `CHECK_POST_CODE`, which is intended to ensure that the zip code has 5 digits and consists only of numbers. If both private methods are called by the public method `CHECK_ADDRESS`, we always have to pass a complete address for testing. It is easier and clearer if we test the private methods separately. This way you can test the actual function of the `SEPARATE_HOUSENO_FROM_STREET` method. 

### Unit Tests erweitern

If we look at the example of finding the house number, there are many pitfalls that can produce an unexpected result. However, we do not know in advance the entries that lead to an incorrect result. We only get to know them when users complain about getting an incorrect result. In this case, the inputs that resulted in erroneous outputs can be included in a unit test. After changing the coding, all unit tests that have already been defined are carried out and the developer can be sure that everything works as before.

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

The test class now only contains the one test method `TEST_GERMAN_STANDARDS` in which all tests are carried out.

There is an auxiliary method `VERIFY_ADDRESS` that takes a street name and a house number, puts them together and then splits them up again using the method `SPLIT_ADDRESS` being tested. Since a test case no longer corresponds 1:1 to a test method, the parameter `MSG` was used by `CL_ABAP_UNIT_ASSERT=>ASSERT_EQUALS` to point directly to the faulty test case.

The test class is now much clearer and the test cases can be easily identified at a glance.

This variant allows you to continue carrying out tests that work according to a different scheme. 

Note: This is not a recommendation to accommodate all tests in one test method. The example is simply intended to show that auxiliary methods can be used to make the unit tests more compact, easier to maintain and more readable.

### Test Environment

ABAP Unit tests can be executed in ADT as well as in the SAP GUI and their results can be analyzed. 
ADT is clearly recommended here, as [Test Relations](https://www.youtube.com/watch?app=desktop&v=yiKhKlQz89Y&t=14s) can also be used here. 

### Resolving dependencies with mocking, faking, stubbing and spying

An important property of testable code is that (business) logic, data acquisition and presentation are strictly separated. If this is guaranteed, then dependent classes can be replaced by non-productive objects. These objects can have different tasks and are named accordingly. The following types are possible:
* Mock
* Stub
* Faker
* Spy

A **Mock** object is an object that can respond dynamically to the caller's input. A mock object can, for example, imitate a query in an external system or the database and deliver the desired data depending on the test case.

A **Stub** is an object with minimal implementation of the methods necessary for testing. This object is only there to ensure that the methods to be tested are called without errors.

A **Fake** object provides necessary data according to a simplified algorithm. For example, the Real Object could perform a comprehensive zip code check, verifying geospatial data, districts and zip codes based on various services. The corresponding faker could make simple checks that are sufficient to carry out the tests.

A **Spy** object can contain properties of stubs, fakes and mocks, but also has the additional function of logging access. For example, a spy could be called during testing; However, the result is not checked directly, only whether this method was called. This type is often used to ensure that emails or other messages would have been sent for certain actions. 

* [Martin Fowler - Mocks Aren't Stubs](https://www.martinfowler.com/articles/mocksArentStubs.html)

#### Test-Doubles

The use of test doubles is necessary if there are dependencies that have not been or could not be resolved sufficiently. With appropriate test double frameworks, the results of database accesses or function module calls can be faked. 

Test double frameworks are usually cumbersome to use and very confusing. Input parameters and the desired results must be specified with many definitions and methods. If possible, you should eliminate the dependencies to avoid using test doubles. However, this is not always possible. We provide further information about the test double frameworks in section [Advanced techniques](#abap_unit_advanced).

#### Automated regular runs of unit tests
There are several ways to run unit tests regularly. 

- Programm RS_AUCV_RUNNER  
- ATC Ran 
- Rest Service (Communication Scenario SAP_COM_0735)

{: .recommendation }
> Schedule unit testing of a system regularly and create notifications for it. 
> It should be part of every developer's morning routine to check whether all tests are error-free so that this can be discussed daily if necessary. 


## Do's & Dont's 
* If in doubt, create one more unit test
+ check less in one test
* No longer use or replace class CL_AUNIT_ASSERT because it is obsolete. The CL_ABAP_UNIT_ASSERT class must be used. 
