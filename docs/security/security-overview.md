---
layout: page
title: overview
permalink: /security/overview/
parent: Security
nav_order: 1
---

{: .no_toc}

# Overview

1. TOC
{:toc}

## ABAP Security: Why secure programming is crucial in SAP

A SAP system or ABAP runtime includes various features for identity and access management of users running ABAP programs. Features include:

- User management tools, such as creating, blocking and deleting users in accordance with common compliance standards.
- Various authentication protocols including single sign-on options
- Enforcing password policies and credential management for users
- An extensible role and permissions management with the ability to design and assign individual roles for users.
- Implicit program-level access control when launching a ABAP program by checking users' launch permissions
- APIs for access control within a program and implicit access control at the instruction level for certain APIs (e.g. access to the file system).

SAP has over time implemented various security APIs and security features into the functional core of the language and propagated frameworks to enable programmers to implement security requirements in ABAP programs. A ABAP developer can often choose from multiple instructions or APIs to implement specific functionality. Implicit security features such as input validation and encryption also vary depending on the framework chosen. The following APIs and security frameworks are available for reuse:

- OS command limitation
- RFC-Callback-Whitelisting
- Unified Connectivity Protocol (UCON)
- HTTP path whitelist
- Output encoding and
- Input validation utilities
- Virus Scan Interface (VSI)
- access control API
- Logging-APIs (a lot) and implicit logging

### From working code to secure applications

As a ABAP developer, you know this: a new project is coming up, the requirements are clearly defined, and the time pressure is high. The priorities are quickly set -- the function must be implemented, the code should be maintainable and performant. But where is the security?

In the reality of many SAP projects, code security plays a minor role. While we think deeply about data structures, algorithms and performance optimization, security is often viewed as a "nice-to-have" or overlooked entirely. SAP systems are particularly worth protecting - they house a company's most valuable data.

### ABAP Code: The Key to the Crown Jewels

Your ABAP code is more than just program logic. It is the key to your company's digital crown jewels:

- **Full access to company data**: master data, financial data, personnel information -- everything is accessible via ABAP
- **Cross-system connections**: RFC calls, web services and interfaces connect your SAP system with the entire IT landscape
- **Privileged System Access**: ABAP programs often run with elevated privileges and can bypass security barriers

Insecure ABAP code can defeat almost all established security measures:

- Role and profile permissions are bypassed
- Client separations lose their effect
- Operating system permissions are skipped
- Firewall rules and network blocks are circumvented

### The vicious circle of downstream security

Many development projects follow a familiar pattern:

1. **Implement function** -- The program must run first
2. **Ensure maintainability** -- Code quality and documentation
3. **Optimize performance** -- If it becomes too slow, improvements will be made
4. **Upgrade security?** -- There is often no time or budget for this

This approach is problematic because retroactively implementing security is not only time-consuming, but often impossible without fundamental reimplementation. What was planned as a small “security fix” quickly turns into a complete architectural overhaul.

## Why security must be considered from the start

### Economic reasons clearly speak for “Security by Design”:

- **Cost factor**: Closing security gaps afterwards is 10-100x more expensive than secure programming from the start
- **Risk minimization**: A single security incident can cause millions in damages
- **Compliance**: Regulatory requirements (GDPR, SOX, etc.) require demonstrably secure development processes
- **Reputation**: Data breaches permanently damage the trust of customers and business partners

### Technical advantages of secure programming:

- **Data economy**: Secure code only processes necessary data and conserves server resources
- **Stability**: Security-aware programming leads to more robust code
- **Maintainability**: Explicit security checks make code more understandable and comprehensible

## Your contribution to company security

As a ABAP developer, you have a special responsibility. Your code runs at the heart of the company's IT and has access to the most valuable data. With the knowledge from this chapter you can:

- Avoid security gaps during the development phase
- Analyze existing code for potential vulnerabilities
- Create awareness of security aspects in your development team
- Contribute to the overall security of the SAP landscape

Secure ABAP code is not a luxury -- it is a necessity in today's connected business world. Let us work together to ensure that your developments are not only functional and performant, but also safe.

{: .solution }
> The following sections guide you through specific security aspects with practical examples and solution approaches. Each code snippet was chosen so that it reflects real challenges from everyday development.
