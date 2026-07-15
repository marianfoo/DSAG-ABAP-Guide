---
layout: page
title: Fundamentals
permalink: /security/basics/
parent: Security
nav_order: 2
---

{: .no_toc}

# Fundamentals

1. TOC
{:toc}  

## The most common ABAP security vulnerabilities at a glance

After introducing the importance of secure ABAP programming, it is important to understand the specific threats that SAP systems face on a daily basis. Experience from hundreds of SAP security audits shows a clear picture: certain vulnerability patterns repeat again and again in ABAP code.

### The top ABAP vulnerabilities

**1. SQL injection via dynamic database queries**
The classic security vulnerability: User input is incorporated unfiltered into SQL statements. A harmless-looking report can become a gateway for data theft. Particularly tricky: Most developers know SQL injection from web development, but overlook the ABAP-specific variants in Open SQL and Native SQL. ABAP protects against the most serious issues here, such as web development with “DROP DATABASE.” However, the SAP system always contains the crown jewels of data, so unauthorized access has more serious consequences in the business context.

**2. Missing or incomplete authorization checks**
ABAP programs often run with elevated system privileges (including in batch mode or against the operating system). If explicit checking of user permissions is missing or incompletely implemented, users can access data and functions that they should not be able to access. It becomes particularly critical with RFC-capable function modules that can be called via the network.

**3. Cross-Site Scripting (XSS) in Web Dynpro and BSP applications**
As soon as ABAP code outputs data to web applications, there is a risk of XSS. Unfiltered HTML code in user input can lead to various problems in the backend. Many SAP systems do not “sanitize” user input, and the problem is further amplified by the increasingly widespread use of modern front-end technologies such as Fiori and UI5.

**4. Code injection in dynamic ABAP constructs**
ABAP offers powerful features for dynamic programming: GENERATE SUBROUTINE POOL, dynamic method calls, RTTI (Run-Time Type Information), or XCO. This flexibility can become a security risk if user input is used unfiltered in dynamic code constructs.

**5. Directory traversal (write access)**
Directory traversal attacks work by manipulating the filename or path information through the insertion of special characters into a string that serves as a file locator. If such a string is used to modify the contents of a file, an application can be tricked into modifying files that the user should not have access to. This attack is possible because the application fails to detect and remove command characters in inputs that are used as part of the file locator.

### Why do these vulnerabilities keep emerging?

The causes are varied but predictable:

**Time constraints and project pressure**: Security checks are viewed as “extra effort” and are cut when deadlines are tight. Yet secure code is often no more complex than insecure code—it just requires the right mindset.

**Lack of security awareness**: Many ABAP developers come from traditional business application development or were technically inclined key users and never systematically learned security aspects. What is standard in the Java or .NET world is often unknown in the ABAP world.

**Complexity of SAP authorization concepts**: SAP authorizations are complex and multi-layered. Developers rely on the assumption that “the system is already configured correctly” without understanding where their responsibility begins.

**Legacy code without a security focus**: Many SAP systems contain code from the 1990s, when security was not yet a priority. This code is often copied and used as a template for new developments - including its vulnerabilities.

## Security mindset: From reactive to proactive thinking

The crucial difference between secure and insecure software does not lie in the technology—it lies in the developers’ mindset. A “security mindset” means viewing security not as an afterthought, but as an integral part of the development process.

### Reactive vs. proactive security thinking

**Reactive approach – “Security as a Fire Department”:**
- Vulnerabilities are only fixed when they are discovered
- Security testing only takes place at the end of development (or not at all)
- Vulnerabilities often require fundamental code changes
- High costs due to fixes and potential security incidents

**Proactive approach – “Security by Design”:**
- Security requirements are considered from the very beginning
- Every feature is designed with security in mind
- Continuous security testing during development
- Lower overall costs by avoiding fixes

### The principles of the security mindset

**1. Never trust, always verify** – Every input is potentially dangerous – regardless of whether it comes from a trusted system or an internal user. Implement validation and sanitization for all inputs, including internal interfaces. The worst thing a developer can hear is: “I don’t need to test this – I trust you!” This shifts the responsibility solely onto the developer.

**2. Minimize the attack surface** – Expose only the functions that are truly needed; remove what has become redundant. An RFC-capable function module that is used only internally is an unnecessary vulnerability. The old, obsolete report that is still left in the system for “documentation reasons” becomes a trap. Implement the principle of least privilege—for both code and users. Furthermore, UCON can also help you control access to standard function modules that may not even be used in your processes.

**3. Think like an attacker** – Ask yourself for every function: “How could someone abuse this?” Consider not only the intended use case, but also possible misuse scenarios. What happens if someone enters unexpected data or calls multiple functions in an unforeseen order? Are all errors caught?

**4. Implement defense in depth** – Never rely on a single security measure. Combine input validation, authorization checks, output encoding and logging. If one protective measure fails, others should kick in. Ensure a consistent logging approach within your department so that issues become visible quickly.

**5. Make security transparent** – Document your security measures in the code. Use meaningful variable names and comments that also show future developers why certain checks were implemented.

### The path to a security culture in the team

Developing a security mindset is not just an individual task—it requires a cultural shift across the entire development team. It therefore makes sense for you to think about the following topics in advance:

**Knowledge building**: Regular security training and discussions about current threats raise awareness. Use internal presentations to discuss concrete examples from your own systems.

**Integration into the development process**: Make security checks an integral part of your code reviews. Develop checklists and guidelines that help every developer take security-relevant aspects into account.

**Positive error culture**: Treat discovered security vulnerabilities as learning opportunities, not as failures. Teams that can speak openly about vulnerabilities develop a stronger security awareness.

**Continuous improvement**: Regularly analyze security issues that have arisen and derive systematic improvements. Which vulnerability patterns occur repeatedly? How can you avoid these in the future?

The security mindset is not a goal to be achieved once and for all—it is an ongoing attitude that must be practiced every day. With knowledge of the most common vulnerabilities and the right mindset, you can help ensure that your ABAP developments are not only functional and high-performing, but also secure.
