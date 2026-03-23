---
layout: page
title: ABAP Unit - advanced techniques
permalink: /testing/abap_unit_advanced/
parent: Software test with ABAP unit
nav_order: 3
---

{: .no_toc}
# ABAP Unit: advanced techniques

1. TOC
{:toc}

## Advanced testing techniques with ABAP Unit  

In this section you will find explanations and notes on advanced testing techniques and frameworks provided as part of the ABAP Unit. Each of the techniques described here has specific uses and offers advantages and disadvantages. Before using these techniques, the basics of unit testing must be well mastered. The use of advanced techniques must be carefully weighed against standard unit testing techniques.

### Test-Double-Frameworks

You can use test double frameworks (TDF) to adapt calls to methods, function modules or database queries (SELECT) to your needs. In general, TDFs work in such a way that you define the object whose function you want to manipulate and then determine which results are to be delivered for which input parameters. 

If you have to use a test double framework, this already indicates that the architecture has not been optimized for unit testing. Test double frameworks should only be used if it is too complex or risky to change the existing architecture.

One reason for avoiding TDFs is that they are difficult to use. You need an extensive setup, which must also be adapted if the unit tests are changed or expanded. 

#### Test double framework for ABAP database accesses/ CDS views/ AMDP

SAP provides you with various frameworks to solve dependencies on various database artifacts. These frameworks are based on techniques that allow the real data in the tables to be replaced by preconfigured MOCK data.

The aim is to build a stable, repeatable environment in which tests can be repeated as often as required without having to create new documents.

You can find an overview of the available options in the [SAP Help](https://help.sap.com/docs/abap-cloud/abap-development-tools-user-guide/managing-database-dependencies-with-ABAP-Unit).


The challenge lies in identifying the tables/views and filling the mock database. 
Plan time for this in development. Create an infrastructure that allows you to access the mock database for many tests. In this way, other business areas also benefit from the data.

#### Test double framework for function blocks

Analogous to other mocking frameworks, the test double framework for function blocks allows you to redirect calls to configurable doubles (class CL_FUNCTION_TEST_ENVIRONMENT). 
You are therefore able to determine for the unit test how the function block should behave. So you are not dependent on the parameters that the function block would determine. This makes it easy, for example, to provoke possible error cases and check the business code to ensure they are handled correctly.  


#### Test double frame wordk for classes

SAP also provides a test double framework (class CL_ABAP_TESTDOUBLE) for classes. You can control method calls of classes that cannot be replaced by other techniques using the test double framework. Just like with function blocks, you can specify which results should be returned for which input parameters. 

### Test-Seams

A test seam is a code fragment that runs instead of production code when executing unit tests. The use of test seams - in contrast to test double frameworks - requires changes to productive code. The code to be replaced in the unit test is enclosed in the productive code by the keywords TEST-SEAM and END-TEST-SEAM. While executing the unit tests, you can use the TEST-INJECTION and END-TEST-INJECTION blocks to define what should happen there instead of the productive code. 

Test seams are suitable, for example, for bypassing user queries or calls in remote systems. 

The test seams technique is **not** a preferred technique for unit testing. It should only be used temporarily.
Test seams do not replace a cleanly designed software architecture that has testability as a feature. Test teams can be used well when unit tests need to be integrated into existing software or legacy software and mocking of components or functions is required. The change is minimal and can therefore be used relatively risk-free. In the medium term, however, the software should be modernized and testing teams eliminated.  
See [Clean ABAP Test Seams](https://github.com/SAP/styleguides/blob/main/clean-abap/CleanABAP.md#use-test-seams-as-temporary-workaround)

### SAP Components such as BAPIs & function modules in unit test

If your component or integration tests rely on a SAP function block or class executing a step that is supposed to be part of your test, it is usually necessary to have repeatable and stable test data in the relevant tables. See [Mocking database tables](#test-data-management-in-ecatt-containers). 

### Automatically generate VALUE statement for mock data

Generating VALUE statements from current data while debugging:
-  ADT: Standard
-  SAPGUI: [Debugger Data View Extension](https://github.com/objective-partner/abap_debugger_data_view_extension)

Generate in ADT from the data preview for selected rows and columns
https://community.sap.com/t5/application-development-and-automation-blog-posts/abap-unit-tests-generate-a-value-statement-for-the-contents-of-an-internal/ba-p/13543137

### Test data management in ECATT containers

The creation and management of many different test data for many different objects is cumbersome and time-consuming. The ECATT tool (Extended Computer Aided Test Tool, transaction SECATT) offers you more convenient options for managing this data. Data can be managed in a structured manner in the ECATT containers. You can access this data manually or programmatically. 
Using the ECATT containers, you can maintain and view test cases manually. If a new test case is added, it may be sufficient to insert additional values ​​into the corresponding containers.

tbd: Attention: the data is lost during a system copy! Save data!

#### Manual management

You can use transaction SECATT to define, view and change the ECATT containers.

#### Programmatic access 

ECATT test data containers can be used to create stable test data. 

Access to the ECATT test data: 
 
 ```
 DATA(lo_tdc_api) = cl_apl_ecatt_tdc_api=>get_instance( 
   i_testdatacontainer         = get_tdc_name( )
   i_testdatacontainer_version = get_tdc_version( ) ).
```

This test data from the ECATT containers can then be inserted into the mock database. 

```
sql_environment = cl_osql_test_environment=>create( change_dependencies( tables_to_be_mocked ) ).
```

{: .warning }
> The insert_from_tdc method is 5 times slower than manually inserting the test data via the insert_test_data method
