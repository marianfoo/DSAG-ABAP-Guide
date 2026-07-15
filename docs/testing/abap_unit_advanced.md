---
layout: page
title: ABAP Unit - advanced techniques
permalink: /testing/abap_unit_advanced/
parent: Software test with ABAP unit
nav_order: 3
---

{: .no_toc}
# ABAP Unit: Advanced Techniques

1. TOC
{:toc}

## Advanced Testing Techniques with ABAP Unit  

In this section you will find explanations and notes on advanced testing techniques and frameworks provided as part of the ABAP Unit. Each of the techniques described here has specific uses and offers advantages and disadvantages. Before using these techniques, the basics of unit testing must be well mastered. The use of advanced techniques must be carefully weighed against standard unit testing techniques.

### Test Double Frameworks

You can use test double frameworks (TDFs) to customize calls to methods, functions, or database queries (SELECT) to suit your needs. Generally, TDFs work by having you define the object whose behavior you want to manipulate, and then specify which results should be returned for which input parameters.

If you need to use a test double framework, this already suggests that the architecture was not optimized for unit tests. Test double frameworks should only be used when it is too costly or too risky to change the existing architecture.

One reason to avoid TDFs is their cumbersome use. They require an extensive setup that must also be adapted whenever the unit tests are modified or expanded.

#### Test Double Framework for ABAP Database Access, CDS Views, and AMDP

SAP provides various frameworks to help you resolve dependencies on different database artifacts. These frameworks are based on techniques that allow you to replace the actual data in the tables with preconfigured mock data.

The goal is to create a stable, repeatable environment in which tests can be run as often as needed without having to recreate documents.

You can find an overview of the available options in the [SAP Help](https://help.sap.com/docs/abap-cloud/abap-development-tools-user-guide/managing-database-dependencies-with-ABAP-Unit).


The challenge lies in identifying the tables/views and populating the mock database. Be sure to schedule time for this during development. Create an infrastructure that allows you to access the mock database for many tests. This way, other business units can also benefit from the data.

#### Test Double Framework for Function Modules

Similar to other mocking frameworks, the test double framework for function modules allows you to redirect calls to configurable doubles (class CL_FUNCTION_TEST_ENVIRONMENT). This allows you to specify, for the unit test, how the function module should behave. You are therefore not dependent on the parameters that the function module would otherwise determine. This makes it easy, for example, to provoke potential error cases and verify that the business code handles them correctly.  


#### Test Double Framework for Classes

SAP also provides a test double framework (class CL_ABAP_TESTDOUBLE) for classes. You can use the test double framework to control method calls from classes that cannot be replaced by other techniques. Just as with function modules, you can specify which results should be returned for which input parameters.

### Test Seams

A test seam is a code fragment that is executed in place of production code when unit tests are run. Unlike test double frameworks, the use of test seams requires modifications to the production code. The code to be replaced in the unit test is enclosed within the production code by the keywords TEST-SEAM and END-TEST-SEAM. During the execution of unit tests, you can use the TEST-INJECTION and END-TEST-INJECTION blocks to define what should happen there instead of the production code.

Test seams are suitable, for example, for bypassing user prompts or calls to remote systems.

The test seam technique is **not** a preferred technique for unit tests. It should only be used temporarily. Test seams do not replace a well-designed software architecture that incorporates testability as a feature. Test seams can be effectively used when unit tests need to be integrated into existing or legacy software and mocking of components or functions is required. The modification is minimal and can therefore be implemented without risk. In the medium term, however, the software should be modernized and test seams eliminated.  
See [Clean ABAP Test Seams](https://github.com/SAP/styleguides/blob/main/clean-abap/CleanABAP.md#use-test-seams-as-temporary-workaround)

### SAP Components such as BAPIs and function modules in unit testing

If your component or integration tests rely on an SAP function module or class to execute a step that is part of the test, you usually need repeatable and stable test data in the relevant tables. See [Mocking database tables](#test-data-management-in-ecatt-containers).

### Automatically Generating a VALUE Statement for Mock Data

Generating VALUE statements from current data while debugging:
-  ADT: Standard
-  SAPGUI: [Debugger Data View Extension](https://github.com/objective-partner/abap_debugger_data_view_extension)

Generate in ADT from the data preview for selected rows and columns https://community.sap.com/t5/application-development-and-automation-blog-posts/abap-unit-tests-generate-a-value-statement-for-the-contents-of-an-internal/ba-p/13543137

### Test Data Management in ECATT Containers

The creation and management of many different test data for many different objects is cumbersome and time-consuming. The ECATT tool (Extended Computer Aided Test Tool, transaction SECATT) offers you more convenient options for managing this data. Data can be managed in a structured manner in the ECATT containers. You can access this data manually or programmatically.
Using the ECATT containers, you can maintain and view test cases manually. If a new test case is added, it may be sufficient to insert additional values into the corresponding containers.

tbd: Attention: Data will be lost during a system copy! Back up your data!

#### Manual Management

You can use transaction SECATT to define, view, and modify ECATT containers.

#### Programmatic Access

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
