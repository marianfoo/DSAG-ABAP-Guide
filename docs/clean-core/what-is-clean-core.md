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


Clean Core has five areas of focus: S/4HANA software versions, business processes, customer extensions, business data, operations and integration. Above all, the new ways of customer expansion are the focus of this chapter.

> “Extensibility features include many options to help customers and partners adapt standard business software to their business needs.”

Source: SAP Help Portal

![Clean Core]({{ site.baseurl }}/clean-core/img/image-01.png)

Clean Core
{: .img-caption}

The Clean Core concept with its various facets is clearly communicated by SAP in the [TechEd2023 - Clean Core: What It Is, Why to Do It, and How to Get There](https://www.youtube.com/watch?v=jlzdD55ahqY). However, the step-by-step instructions are unclear for established customers who use various "legacy" technologies in their SAP systems. 
There are numerous existing customers and SAP partners who have created added value in their systems through in-house developments and system expansions. By definition, these added values ​​do not belong to the Clean Core - the extensions are almost always based on non-approved interfaces. There are different [successor technology matrices](https://www.sap.com/documents/2022/10/52e0cd9b-497e-0010-bca6-c68f7e60039b.html) for the so-called RICEFW objects. Internally, the main questions are: "How can we represent the technology change to our customers? And why should I change well-functioning processes that are based, for example, on IDocs, messages, RFCs and ALV transactions now?"

## Clean Core Definition
At its core, the Clean Core concept revolves around separating core business logic from non-core functionality within the SAP software suite. By isolating core business processes and data structures, SAP aims for a leaner and more agile foundation that can adapt to changing business needs. The new ways of customer expansion are called: ABAP Cloud and Side-by-Side Extensibility. 

- **ABAP Cloud or "On-Stack Extensibility"** - These are two different technologies: "Developer Extensibility" and "Key-User Extensibility".

- **Side-by-Side Extensibility** - Is the outsourcing of customer extensions to the Business Technology Platform - BTP.


An example: Instead of sending the MATMAS IDoc in heterogeneous form to different systems, you should use the standardized interface [Product Master API](https://api.sap.com/api/API_PRODUCT_SRV/overview). An interface that can be designed to be homogeneous is then used to supply the SAP and non-SAP systems.

The data model underneath is expanded through key user extensibility and is also used in generic reports such as embedded analytics or the SAP Analytic Cloud (SAC). For complex customer logic, the developer must extend this customer logic with Developer Extensibility and the ABAP RESTful Application Programming Model (RAP).

Basically, Clean Core is as the manufacturer describes it: 
1. Extensions are clearly separated from the SAP code and extensions do not modify SAP objects.
2. Take advantage of new expansion technologies and the SAP standard. The new extension technologies are: Key User, Developer and Side-by-Side Extensibility. 
3. Extensions only use stable, released SAP APIs and extension points. Classic Extensibility should only take place in released Business Add-Ins (BADI) with released development objects. 
4. Legacy technologies such as RFCs, IDocs and customer-specific screen transactions or SAP SEGW projects should no longer be used for new developments. 
5. Old customer developments and extensions should be migrated to new technologies or the business process requirement will be found in the SAP standard.

The manufacturer's information indicates four areas of application and the facts for achieving a Clean Core are as follows:

#### Data models
* Regardless of whether simple or complex use cases are to be implemented, data modeling with the Virtual Data Model (VDM) is required. 
* There should be no direct access to SAP standard tables.
* SAP focuses on standard data products (e.g. customer order). Customer processes and data models outside of the SAP standard remain the responsibility of the SAP customer.

#### Application logic
* SAP standard coding should no longer be expanded in the classic way.
* Extensions to the standard should be migrated to defined and released BADIs.
* In-house developments must use Clean Core compliant development objects (keyword: release contracts).

#### Applications
* In principle, customers should use the standard Fiori apps or SAP GUI for HTML with screen personas to use existing SAP standard transactions.
* The standard Fiori apps and the standard APIs behind them are to be expanded.
* For custom apps, Fiori Elements and standard APIs (based on RAP) should initially be used. The app can then be expanded using the Flexbile Programming Model (FPM). The last step would then be Freestyle Fiori apps. 
* Other solutions: Cloud Native applications in a Cloud environment (Side-by-Side Extensibility). Low/no-code platforms and the SAP build portfolio offer further solutions.

#### Interfaces
* Only Clean Core compliant, approved interfaces are used.
* Extensions are made to APIs and microservices to extend the functionality of SAP without affecting the integrity of the core system.
* External integration must be clearly regulated; process integration and middleware for API management must be available.
* Legacy technologies such as IDocs, RFCs and SAP SEGW projects must be gradually replaced.

In summary, the Clean Core concept of the SAP represents a paradigm shift in the design of corporate software. SAP aims to only offer new services in the Cloud and to further expand the interfaces to the Core. The added value of bringing well-running solutions to a new platform is not present for the time being. A company should adopt new solutions with the new types of expansion in order to be prepared for the future. This is how a SAP customer benefits from the innovations surrounding the standard. The paradigm shift also includes digital transformation: away from the SAP GUI and Dynpros towards the Fiori Launchpad, the end users should primarily work in the browser. A Clean Core also includes massive change management by IT and the departments.

By implementing the Clean Core principles and strategic initiatives, organizations can prepare for future SAP strategies, particularly Cloud technologies. 

According to SAP, the main thing with Clean Core is that customers do not block the future and build standardized interfaces. By standardizing business processes and using the SAP BTP, SAP services or solutions from SAP partners can be used completely.
The Clean Core strategy is a philosophy for many existing customers until internal guidelines regulate the use of the successor technologies. Based on the guidelines, developers are organizationally aligned and trained. A committee to comply with the "Clean Core Governance" is mandatory with the mandate to maintain, expand and enforce the guidelines. Research and development should be carried out frequently to identify the added value of SAP service.

## Target Group
Essentially, two large customer groups are visible in the DSAG network: The first group decides to make a large investment in their SAP landscape and works with SAP and their partners to move towards a Clean Core in accordance with the SAP definition. The other group opts for a scaled approach, where investments are spread over several years. 

Here are some examples of possible SAP customers:

1. New SAP customers migrating to S/4HANA. The greenfield approach and the strict Clean Core according to SAP should be applied here.
2. Brownfield to Bluefield: Existing SAP customers who have been working with SAP for decades and are migrating to S/4HANA. Depending on your willingness to invest, the Clean Core can be defined step by step and the new development can be kept compliant with it. Existing customer extensions are converted to a Clean Core compliant development in large projects.
3. Brownfield to Greenfield: Existing SAP customers who have been working with SAP for decades and are migrating to S/4HANA. Customer expansions with very high investment volumes can be depicted here.
4. Brownfield in S/4HANA: Is identical to scenario two.

### Private/Public Cloud
The digital transformation of every SAP customer depends on the company's existing expertise, partners, investment opportunities and many other factors. The DSAG network can recommend asking the manufacturer and evaluating which SAP systems can be transformed into the Cloud. The analysis tools and willingness to provide advice from SAP are very high. After that, the steps are varied. The only question that needs to be answered at some point is: Should the company and its SAP systems go public Cloud? Here are some tips for Cloud scenarios.


## Differences between models

### Public Cloud

The SAP S/4HANA Cloud, public edition (GROW) is “clean” by definition. If you as a customer start with GROW or migrate your system to a S/4HANA Public Cloud system, then you can only develop Clean Core and have no option to access non-released objects in the standard.

If you want to use an existing customer code on a public Cloud system, it must be ABAP-Cloud-capable and your processes must be mapped to the SAP standard.


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

### Greenfield approach
The greenfield approach describes a complete reimplementation of a SAP system. The existing system is not migrated, but rather a completely new system is built on a “greenfield site”.

Characteristics:
- Restart: Complete new implementation without legacy problems.
- Flexibility: Possibility to completely redesign processes, structures and architectures.
- Effort: Requires intensive preparation, training and high investments.
- Advantage: Ideal solution for companies that want to fundamentally revise and optimize their business processes.
- Risk: Higher implementation effort, longer project durations.


### Brownfield approach
The brownfield approach refers to the conversion of an existing SAP system to a new SAP system (e.g. SAP S/4HANA) through migration. In contrast to the greenfield approach, existing systems, data and processes are largely adopted here.

Characteristics:
- Inventory preservation: use of existing systems and processes.
- Efficiency: Faster implementation by using existing infrastructure.
- Effort: Lower effort compared to the greenfield approach.
- Advantage: Minimal disruption to business operations; lower risks.
- Risk: Taking over legacy issues (e.g. outdated processes or poor data quality).


### Bluefield approach
The bluefield approach represents a hybrid approach between greenfield and brownfield. Selective data and process migration is carried out, which means that legacy issues can be eliminated and existing systems can be used.

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
  A modification refers to directly changing the SAP standard code. This is a measure that SAP strongly does not recommend as it complicates future updates and maintenance cycles. With every system upgrade, processing with transaction SPAU will have to be carried out.
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
  - In specific cases, for example in the area of ​​​​**FI** (Financial Accounting), it may be necessary to define exceptions. These concern scenarios in which auditors have specific requirements or there is high audit complexity.  
  - A modification implementation due to OSS Notes or third party add-ons is usually the reason for the majority of modifications.

  In such cases:  
  - **Documentation and justification of the measure** is mandatory.  
  - The affected code must be clearly commented and marked as modified code.  


#### Justification for modifications  
Modifications may only be made after careful consideration. The reasons for this must be clearly documented and understandable.  

#### Possible justifications:  
- **Implementation of unique selling points (USPs)**:  
  Creation or adaptation of functions that allow the company to differentiate.  
- **Prozessoptimierung**:  
  Mapping customer-specific business processes or automating standard processes and internal procedures.  
- **Kosteneinsparungen**:  
  Reduction of operational or long-term expenses through targeted adjustments.  


## Saubere Modifikationen
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
    - Getestete Szenarien.  

### DON'T
- **Write business process logic directly in the modification**:  
  - Such changes complicate future maintenance and testing.  
- **Copying SAP default code**:  
  - Avoid copying code as this can lead to inconsistencies and technical debt.  
- **Confusing changes**:  
  - Do not mix standard code and custom code.  

## Clean ABAP - Delimitation

Clean ABAP is about writing ABAP code that focuses on understandability and maintainability. Clean Core and SAP are about dealing with the limits of customer-specific programs in the SAP standard. Just because an implementation corresponds to the Clean Core strategy does not automatically make it Clean ABAP and vice versa. More about this in chapter [ABAP]({{ site.baseurl }}/abap).
