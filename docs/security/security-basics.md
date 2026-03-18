---
layout: page
title: Grundlagen
permalink: /security/basics/
parent: Security
nav_order: 2
---

{: .no_toc}

# Grundlagen

1. TOC
{:toc}  

## The most common ABAP security vulnerabilities at a glance

After introducing the importance of secure ABAP programming, it is important to understand the specific threats that SAP systems face on a daily basis. Experience from hundreds of SAP security audits shows a clear picture: certain vulnerability patterns repeat again and again in ABAP code.

### The top ABAP vulnerabilities

**1. SQL injection through dynamic database queries**
The classic among security holes: user input is integrated into SQL statements without filtering. A harmless-looking report can become a gateway for data theft. Particularly tricky: Most developers know SQL injection from web development, but overlook the ABAP-specific variants in Open SQL and Native SQL. ABAP Protects against the really big problems, for example web development with "DROP DATABASE;". However, the SAP system always contains the crown jewels of data, so unauthorized access has more serious consequences in the business context.

**2. Missing or incomplete authorization checks**
ABAP programs often run with extended system rights (including in batch or compared to the operating system). If explicit checking of user permissions is missing or incompletely implemented, users can access data and functions that they should not be able to access. It becomes particularly critical with RFC-capable function modules that can be called via the network.

**3. Cross-Site Scripting (XSS) in Web-Dynpro and BSP applications**
As soon as ABAP code outputs data to web applications, there is a risk of XSS. Unfiltered HTML code in user input can lead to various problems in the backend. Many SAP systems do not "clean up" user input, and the problem is compounded by the ever-increasing use of modern front-end technologies such as Fiori and UI5. 

**4. Code injection into ABAP dynamic constructs**
ABAP offers powerful functions for dynamic programming: GENERATE SUBROUTINE POOL, dynamic method calls, RTTI (Run Time Type Information) or XCO. This flexibility can become a security risk if user input is used unfiltered in dynamic code constructs.

**5. Directory Traversal (Write Access)**
Directory traversal attacks work by manipulating the file name or path information by entering special characters into a string that acts as a file locator. If such a string is used to modify the contents of a file, an application can be tricked into modifying files that the user should not have access to. This attack is possible because the application fails to detect and remove command characters in input used as part of the file locator.

### Why do these vulnerabilities keep emerging?

The causes are varied but predictable:

**Lack of time and project pressure**: Security checks are seen as “additional effort” and are canceled when deadlines are tight. Secure code is often no more complex than unsafe code – it just requires the right level of awareness.

**Lack of security awareness**: Many ABAP developers come from classic business application development or have been key users with a technical interest and have never learned security aspects systematically. What is standard in the Java or .NET world is often unknown in the ABAP world.

**Complexity of SAP authorization concepts**: SAP authorizations are complex and multi-layered. Developers rely on the fact that "the system is already configured correctly" without understanding where their responsibility begins.

**Legacy code without a security focus**: Many SAP systems contain code from the 1990s, when security was not yet a priority. This code is often copied and used as a template for new developments - including its vulnerabilities.

## Security-Mindset: Vom reaktiven zum proaktiven Denken

The key difference between secure and insecure software isn't the technology - it's the way developers think. A "security mindset" means not viewing security as an afterthought, but rather as an integral part of the development process.

### Reaktives vs. proaktives Security-Denken

**Reactive approach – “Security as a fire department”:**
- Vulnerabilities are only fixed when they are discovered
- Security tests only take place at the end of development (or not at all).
- Vulnerabilities often require fundamental code changes
- High costs due to improvements and possible security incidents

**Proaktiver Ansatz – "Security by Design":**
- Safety requirements are taken into account right from the start
- Every feature is designed with security in mind
- Continuous security checks during development
- Lower overall costs by avoiding rework

### The principles of the security mindset

**1. Never trust, always check**
Any input is potentially dangerous, whether it comes from a trusted system or an internal user. Implement validation and sanitization for all inputs, including internal interfaces. The worst sentence for a developer should be "I don't need to test this, I trust you!" be. This places the responsibility solely on the developer.

**2. Minimize the attack surface**
Expose only the functions that are really needed, delete what has become unnecessary. An RFC-enabled function module that is only used internally is an unnecessary vulnerability. The old, obsolete report that is still left in the system for “documentation reasons” becomes a trap. Implement the principle of minimum permission - for both code and users. Furthermore, UCON can also support you in controlling access to standard function blocks that may not even be used in your processes.

**3. Denken Sie wie ein Angreifer**
For each feature, ask yourself, "How could someone abuse this?" Consider not only the intended use case, but also possible misuse scenarios. What happens if someone makes unexpected input or calls multiple functions in an unexpected order? Are all errors caught?

**4. Implement Defense in Depth**
Never rely on a single security measure. Combine input validation, authorization checks, output encoding and logging. If one protective measure fails, others should take effect. Ensure that your department uses a consistent method of logging so that problems become quickly visible.

**5. Make security transparent**
Document your security measures in code. Use meaningful variable names and comments that show later developers why certain checks were implemented.

### The path to a security culture in the team

Developing a security mindset is not just an individual task – it requires a culture change across the entire development team. It therefore makes sense for you to think about the following topics in advance:

**Knowledge building**: Regular security training and exchanges about current threats create awareness. Use internal presentations to discuss concrete examples from your own systems.

**Integrate into the development process**: Make security checks an integral part of your code reviews. Develop checklists and guidelines that help every developer take security-relevant aspects into account.

**Positive error culture**: Treat discovered vulnerabilities as learning opportunities, not as failures. Teams that can openly discuss vulnerabilities develop greater security awareness.

**Continuous Improvement**: Analyze regularly encountered security issues and derive systematic improvements. Which vulnerability patterns occur repeatedly? How can you avoid these in the future?

The security mindset is not a goal that can be achieved once - it is an ongoing attitude that must be lived every day. With knowledge of the most common vulnerabilities and the right attitude, you can help ensure that your ABAP developments are not only functional and performant, but also secure.