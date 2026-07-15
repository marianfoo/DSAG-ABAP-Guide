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

## ABAP Security: Why Secure Programming in SAP is Critical

An SAP system or ABAP runtime environment includes various functions for managing the identities and access of users who execute ABAP programs. These functions include:

- User management tools, such as creating, locking, and deleting users in accordance with current compliance standards
- Various authentication protocols, including single sign-on options
- Enforcement of password policies and credential management for users
- An extensible role and authorization management system with the ability to design and assign custom roles to users
- Implicit access control at the program level when an ABAP program is started by checking the user’s startup authorizations
- APIs for access control within a program and implicit access control at the statement level for specific APIs (e.g., access to the file system)

Over time, SAP has implemented various security APIs and security features into the functional core of the language and into the promoted frameworks to enable programmers to implement security requirements in ABAP programs. An ABAP developer can often choose from several statements or APIs to implement specific functions. Implicit security features such as input validation and encryption also vary depending on the chosen framework. The following APIs and security frameworks are available for reuse:

- OS command restriction
- RFC callback whitelisting
- Unified Connectivity Protocol (UCON)
- HTTP path whitelist
- Output encoding and
- Input validation utilities
- Virus Scan Interface (VSI)
- access control API
- Logging APIs (a variety) and implicit logging

### From Working Code to a Secure Application

As an ABAP developer, you know the drill: A new project is on the horizon, the requirements are clearly defined, and the time pressure is high. Priorities are quickly set—the functionality must be implemented, and the code should be maintainable and performant. But where does security fit into all this?

In the reality of many SAP projects, code quality checks play a secondary role. While we spend a great deal of time thinking about data structures, algorithms, and performance optimization, security is often viewed as a “nice-to-have” or overlooked entirely. Yet SAP systems, in particular, are worth protecting—they house a company’s most valuable data.

### ABAP Code: The Key to the Crown Jewels

Your ABAP code is more than just program logic. It is the key to your company's digital crown jewels:

- **Full access to company data**: master data, financial data, personnel information -- everything is accessible via ABAP
- **Cross-system connections**: RFC calls, web services and interfaces connect your SAP system with the entire IT landscape
- **Privileged System Access**: ABAP programs often run with elevated privileges and can bypass security barriers

Insecure ABAP code can undermine nearly all established security measures:

- Role and profile permissions are bypassed
- Client separations lose their effect
- Operating system permissions are skipped
- Firewall rules and network blocks are circumvented

### The Vicious Cycle of Post-Implementation Security

Many development projects follow a familiar pattern:

1. **Implement function** -- The program must run first
2. **Ensure maintainability** -- Code quality and documentation
3. **Optimize performance** -- If it becomes too slow, improvements will be made
4. **Upgrade security?** -- There is often no time or budget for this

This approach is problematic because implementing security retroactively is not only costly but often impossible without a fundamental reimplementation. What was planned as a small “security fix” quickly turns into a complete architectural overhaul.

## Why Security Must be Considered From the Very Beginning

### Economic reasons clearly favor “Security by Design”:

- **Cost factor**: Closing security gaps afterwards is 10-100x more expensive than secure programming from the start
- **Risk minimization**: A single security incident can cause millions in damages
- **Compliance**: Regulatory requirements (GDPR, SOX, etc.) require demonstrably secure development processes
- **Reputation**: Data breaches permanently damage the trust of customers and business partners

### Technical advantages of secure programming:

- **Data economy**: Secure code only processes necessary data and conserves server resources
- **Stability**: Security-aware programming leads to more robust code
- **Maintainability**: Explicit security checks make code more understandable and comprehensible

## Your Contribution to Enterprise Security

As an ABAP developer, you bear a special responsibility. Your code runs at the heart of the enterprise IT infrastructure and has access to the most valuable data. With the knowledge from this chapter, you can:

- Avoid security gaps during the development phase
- Analyze existing code for potential vulnerabilities
- Create awareness of security aspects in your development team
- Contribute to the overall security of the SAP landscape

Secure ABAP code is not a luxury—it is a necessity in today’s interconnected business world. Let’s work together to ensure that your developments are not only functional and high-performing, but also secure.

{: .solution }
>     The following sections guide you through specific security aspects with practical ex- amples and solutions. Each code snippet has been selected to reflect real-world challenges from everyday development.
