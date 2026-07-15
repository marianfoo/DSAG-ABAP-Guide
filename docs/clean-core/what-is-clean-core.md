---
layout: page
title: What is Clean Core
permalink: /clean-core/what-is-clean-core/
parent: Clean Core
nav_order: 1
---

{: .no_toc}
# What is Clean Core

1. TOC
{:toc}


## Clean Core at first glance
Clean Core is a concept and for some SAP customers a philosophy - Clean Core is understood, interpreted and lived differently. A common understanding of the DSAG community would be the following:

- **"Clean Core"** - Strictly speaking, the concept should be interpreted as follows: System upgrades should have no influence on customer expansions. Therefore
SAP customers are only allowed to use released interfaces for business process extensions.

- **“Keep the core clean”** - Means that a company carries out new developments according to Clean-Core principles - defined guidelines in a company.

- **"Make the core clean"** - Refers to business transformation and the iterative journey to a Clean Core.


Clean Core has five key areas of focus: S/4HANA software versions, business processes, customer enhancements, business data, operations, and integration. This chapter focuses primarily on the new approaches to customer enhancements.

> “The extensibility features include many options that help customers and partners customize standard business software to meet their business needs”.

Source: SAP Help Portal

![Clean Core]({{ site.baseurl }}/clean-core/img/image-01.png)

Clean Core
{: .img-caption}

The Clean Core concept with its various facets is clearly communicated by SAP in the [TechEd2023 - Clean Core: What It Is, Why to Do It, and How to Get There](https://www.youtube.com/watch?v=jlzdD55ahqY). However, the step-by-step instructions are unclear for established customers who use various "legacy" technologies in their SAP systems.
There are numerous existing customers and SAP partners who have created added value in their systems through in-house developments and system expansions. By definition, these added values do not belong to the Clean Core - the extensions are almost always based on non-approved interfaces. There are different [successor technology matrices](https://www.sap.com/documents/2022/10/52e0cd9b-497e-0010-bca6-c68f7e60039b.html) for the so-called RICEFW objects. Internally, the main questions are: "How can we represent the technology change to our customers? And why should I change well-functioning processes that are based, for example, on IDocs, messages, RFCs and ALV transactions now?"

## Definition of Clean Core
At its core, the Clean Core concept revolves around separating core business logic from non-core functionality within the SAP software suite. By isolating core business processes and data structures, SAP aims for a leaner and more agile foundation that can adapt to changing business needs. The new approaches to customer extensibility are called: ABAP Cloud and Side-by-Side Extensibility.

- **ABAP Cloud or "On-Stack Extensibility"** - These are two different technologies: "Developer Extensibility" and "Key-User Extensibility".

- **Side-by-Side Extensibility** - Is the outsourcing of customer extensions to the Business Technology Platform - BTP.


An example: Instead of sending the MATMAS IDoc in heterogeneous form to different systems, you should use the standardized interface [Product Master API](https://api.sap.com/api/API_PRODUCT_SRV/overview). An interface that can be designed to be homogeneous is then used to supply the SAP and non-SAP systems.

The underlying data model is extended through Key User Extensibility and is also used in generic reports such as Embedded Analytics or the SAP Analytics Cloud (SAC). In cases involving complex business logic, the developer must extend this logic using Developer Extensibility and the ABAP RESTful Application Programming Model (RAP).

Basically, Clean Core is exactly as the vendor describes it:
1. Extensions are clearly separated from the SAP code and extensions do not modify SAP objects.
2. Take advantage of new expansion technologies and the SAP standard. The new extension technologies are: Key User, Developer and Side-by-Side Extensibility.
3. Extensions should only use stable, released SAP APIs and extension points. Classic Extensibility should only be used in released Business Add-Ins (BAdIs) with released development objects.
4. Legacy technologies such as RFCs, IDocs and customer-specific screen transactions or SAP SEGW projects should no longer be used for new developments.
5. Legacy in-house developments and enhancements are to be migrated to new technologies, or the business process requirements are met by the standard SAP system.

According to the vendor's specifications, there are four areas of application, and the requirements for achieving a Clean Core are as follows:

#### Data models
* Regardless of whether simple or complex use cases are to be implemented, data modeling using the Virtual Data Model (VDM) is required.
* There should be no direct access to standard SAP tables.
* SAP focuses on standard data products (e.g. sales order). Customer processes and data models outside the SAP standard remain the responsibility of the SAP customer.

#### Application logic
* Standard SAP code should no longer be extended using traditional methods.
* Extensions to the standard should be migrated to defined and approved BAdIs.
* In-house developments must use development objects that comply with the Clean Core standard (keyword: release contracts).

#### Applications
* In general, customers should use the standard Fiori apps or SAP GUI for HTML with Screen Personas to access existing standard SAP transactions.
* The standard Fiori apps and the underlying standard APIs should be extended.
* For custom apps, Fiori Elements and standard APIs (based on RAP) should be used initially. The app can then be extended using the Flexible Programming Model (FPM). The final step would then be Freestyle Fiori apps.
* Additional approaches: Cloud-native applications in a cloud environment (side-by-side extensibility). Low-code/no-code platforms and the SAP Build portfolio offer further solutions.

#### Interfaces
* Only Clean Core-compliant, approved interfaces are used.
* Extensions are made to APIs and microservices to expand SAP’s functionality without compromising the integrity of the core system.
* External integration must be clearly regulated; process integration and middleware for API management must be in place.
* Legacy technologies such as IDocs, RFCs, and SAP SEGW projects must be phased out gradually.

In summary, SAP’s Clean Core concept represents a paradigm shift in the design of enterprise software. SAP is committed to offering new services exclusively in the cloud and to further expanding the interfaces to the core. For now, there is no added value in migrating well-functioning solutions to a new platform. A company should find new solutions using the new types of extensions to be prepared for the future. This way, an SAP customer benefits from innovations surrounding the standard. The paradigm shift also includes digital transformation: moving away from the SAP GUI and screens toward the Fiori Launchpad—end users are expected to work primarily in the browser. A Clean Core also requires extensive change management by IT and the business departments.

By implementing the principles of Clean Core and strategic initiatives, organizations can prepare for future SAP strategies, particularly cloud technologies.

According to SAP, the main goal of Clean Core is to ensure that customers do not limit their future options and instead establish standardized interfaces. By standardizing business processes and leveraging SAP BTP, SAP services and solutions from SAP partners can be fully utilized.
For many existing customers, the Clean Core strategy serves as a guiding philosophy until internal policies are established to govern the use of successor technologies. Based on these guidelines, developers are aligned organizationally and trained. A committee responsible for ensuring compliance with “Clean Core Governance” is mandatory—with the mandate to maintain, expand, and enforce the guidelines. Research and development should be conducted frequently to identify the added value provided by SAP Services.

## Target Audience
Essentially, there are two major customer groups within the DSAG network: The first group opts for a major investment in its SAP landscape and works with SAP and its partners to achieve a Clean Core as defined by SAP. The other group adopts a more incremental approach, spreading the investments over several years.

Here are some examples of possible SAP customers:

1. New SAP customers migrating to S/4HANA. According to SAP, the greenfield approach and the strict Clean Core model should be applied here.
2. Brownfield to Bluefield: Existing SAP customers who have been working with SAP for decades and are migrating to S/4HANA. Depending on their willingness to invest, the Clean Core can be defined in phases, and new development can be kept compliant with it. Existing customer enhancements are migrated to Clean Core-compliant development through large-scale projects.
3. Brownfield to Greenfield: Existing SAP customers who have been working with SAP for decades and are migrating to S/4HANA. In this scenario, customer-specific enhancements involving significant investment can be migrated.
4. Brownfield in S/4HANA: This is identical to scenario two.

### Private/Public Cloud
The digital transformation of every SAP customer depends on the expertise available within the company, its partners, investment opportunities, and many other factors. The DSAG network recommends consulting with the vendor to determine which SAP systems are suitable for a cloud migration. SAP offers robust analysis tools and strong consulting support. From there, the options are diverse. Ultimately, only one question needs to be answered: Should the company move its SAP systems to the public cloud? Here are some tips on cloud scenarios.


## Differences between models

### Public Cloud

The SAP S/4HANA Cloud, public edition (GROW) is “clean” by definition. If you as a customer start with GROW or migrate your system to a S/4HANA Public Cloud system, then you can only develop Clean Core and have no option to access non-released objects in the standard.

To use existing custom code in a public-cloud system, the code must be compatible with ABAP Cloud and your processes must be mapped to SAP standard processes.


### Private Cloud

The SAP S/4HANA Cloud, private edition (RISE) is an on-premise system operated by SAP. Here you don't have to adhere to a strict Clean Core and you have all the freedom of classic on-premise development. The focus here is on simplifying Industry Solutions developments without completely redesigning all processes. However, it may be that not all modifications to the system are permitted by SAP.


### On-Premise

If you would like to have your system operated in your own data center or by a service provider, then you are in the classic on-premise environment. You are responsible for the upgrades and have complete freedom to modify your system.


### Applicability of Clean Core:
- Relevant scenarios:
  - SAP S/4HANA on-premise
  - SAP S/4HANA Cloud, private edition (RISE)
- Public Cloud is Clean by default:
  - The SAP S/4HANA Cloud, public edition (GROW) is built from the ground up on Clean-Core principles.


## S/4HANA Transformation

This distinction helps in deciding which approach best suits a company's goals, resources and circumstances.

### Greenfield Approach
The Greenfield approach refers to a completely new implementation of an SAP system. In this process, the existing system is not migrated; instead, a new system is built from scratch.

Characteristics:
- Restart: Complete new implementation without legacy problems.
- Flexibility: Possibility to completely redesign processes, structures and architectures.
- Effort: Requires intensive preparation, training and high investments.
- Advantage: Ideal solution for companies that want to fundamentally revise and optimize their business processes.
- Risk: Higher implementation effort, longer project durations.


### Brownfield Approach
The brownfield approach refers to the transition from an existing SAP system to a new SAP system (e.g. SAP S/4HANA) through migration. Unlike the greenfield approach, this involves transferring existing systems, data, and processes.

Characteristics:
- Inventory preservation: use of existing systems and processes.
- Efficiency: Faster implementation by using existing infrastructure.
- Effort: Lower effort compared to the greenfield approach.
- Advantage: Minimal disruption to business operations; lower risks.
- Risk: Taking over legacy issues (e.g. outdated processes or poor data quality).


### Bluefield Approach
The Bluefield approach represents a hybrid approach between Greenfield and Brownfield. It involves selective data and process migration, which allows for the elimination of legacy issues while also leveraging existing systems.

Characteristics:
- Selectivity: Companies can decide which data and processes are adopted or redesigned.
- Flexibility and control: Optimization of existing processes without completely re-implementing them.
- Effort: Between greenfield and brownfield.
- Advantage: Optimal balance between innovation and efficiency.
- Risk: Complexity in planning and implementation, as both old and new components have to be integrated.


## Delimitation at a glance

| Characteristic    | **Greenfield**                 | **Brownfield**                 | **Bluefield**                  |
|--------------------|--------------------------------|--------------------------------|--------------------------------|
| **Approach**       | Complete new beginning         | System migration               | Selective migration            |
| **Data transfer**  | No                             | Complete                       | Partial                        |
| **Process takeover** | New                          | Existing                       | Selective                      |
| **Effort**         | High                           | Medium                         | Medium to high                |
| **Flexibility**    | Very high                      | Low                            | High                           |
| **Risks**          | Long implementation time       | Takeover of legacy assets      | High complexity                |
| **Suitable for**   | Companies in need of radical redesign | Companies with proven processes | Companies with mixed requirements |


See also the following SAP guides for additional S/4HANA and Cloud topic areas [Mapping your journey to SAP S/4HANA Cloud Private Edition - A practical guide for senior IT leadership](https://d.dam.sap.com/x/HvXc6b7/94115_92460_enUS.pdf?rc=19&inline=true)


## Modifications in SAP code

Here is some help for SAP customers who cannot yet migrate to the public Cloud in the medium term.

### Principles for Modifications  
- **Definition according to SAP Help**:  
  A modification changes SAP standard code directly. SAP strongly advises against this because it complicates future updates and maintenance cycles. Transaction SPAU must be processed after every system upgrade.
- **Definition according to the document "Extend SAP S/4HANA in the cloud and on premise with ABAP based extensions"**:
   You should also look critically at the remaining standard classic extension types and favor the use of BADIs.
  See: ["5.3.2 Using classical business logic extension techniques"](https://www.sap.com/documents/2022/10/52e0cd9b-497e-0010-bca6-c68f7e60039b.html)
- **Recommended approach**:  
 Modifications and extensions (enhancements) are classic extension methods and should only be carried out when all other options, such as the new types of extensions, the use of BADIs or adjustments using customer-specific objects, have been exhausted.  

### Important Notes  
- Always perform an **Impact Analysis** before making a modification to minimize potential conflicts with future updates.  
- The use of customer-specific extensions should be preferred. In the SAP Help portal you will find numerous options for extensions, including:  
  - **User Exits**: Intended for custom logic.  
  - **BAdIs (Business Add-Ins)**: Flexible extension points in the SAP standard.  
  - **Enhancements**: Technologies such as Enhancement Framework and Switch Framework for targeted changes.  

### “NEVER COPY SAP CODE”  
- **SAP Help principle**:  
  Copying standard SAP code risks inconsistencies and makes both traceability and maintenance difficult. Changes should only be made via the SAP extension options provided such as user exits, BAdIs or enhancement points.  
- **Exception rule**:  
  - In specific cases, for example in the area of **FI** (Financial Accounting), it may be necessary to define exceptions. These concern scenarios in which auditors have specific requirements or there is high audit complexity.  
  - A modification implementation due to OSS Notes or third party add-ons is usually the reason for the majority of modifications.

  In such cases:  
  - **Documentation and justification of the measure** is mandatory.  
  - The affected code must be clearly commented and marked as modified code.  


#### Justification for modifications  
Modifications may only be made after careful consideration. The reasons for this must be clearly documented and understandable.  

#### Possible justifications:  
- **Implementation of unique selling points (USPs)**:  
  Creation or adaptation of functions that allow the company to differentiate.  
- **Process optimization**:  
  Mapping customer-specific business processes or automating standard processes and internal procedures.  
- **Cost savings**:  
  Reduction of operational or long-term expenses through targeted adjustments.  


## Clean modifications
If you want to modify the SAP standard, consider the following rules and best practices. Adhering to these guidelines ensures maintainable, traceable, and future-proof code that can withstand SAP upgrades and patches.  

### DO
- **Open SAP code and create an enhancement spot**:  
  - Create an **Enhancement Spot** in the modification.  
  - Use all the advantages of the enhancements, e.g. B. the separation of standard and customer code, as well as storage in the **Z package**.  
- **Clear separation of logic**:  
  - Separate business process logic into separate classes or methods.  
  - Use **standalone testing methods** to be able to test the logic independently.  
- **Don't forget documentation**:  
  - Any modification must be fully documented, including:  
    - Purpose of the change.  
    - Impact on future updates.  
    - Tested scenarios.  

### DON'T
- **Write business process logic directly in the modification**:  
  - Such changes complicate future maintenance and testing.  
- **Copying SAP default code**:  
  - Avoid copying code as this can lead to inconsistencies and technical debt.  
- **Confusing changes**:  
  - Do not mix standard code and custom code.  

## Clean ABAP - Delimitation

Clean ABAP is about writing ABAP code that focuses on understandability and maintainability. Clean Core and SAP are about dealing with the limits of customer-specific programs in the SAP standard. Just because an implementation corresponds to the Clean Core strategy does not automatically make it Clean ABAP and vice versa. More about this in chapter [ABAP]({{ site.baseurl }}/abap).
