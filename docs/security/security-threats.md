---
layout: page
title: Threats
permalink: /security/threats/
parent: Security
nav_order: 3
---

{: .no_toc}

# Threats

1. TOC
{:toc}  

## SQL Injection in ABAP: Attack Vectors and Countermeasures

SQL injection is one of the most dangerous and, at the same time, most frequently overlooked vulnerabilities in ABAP systems. While many developers believe that OpenSQL automatically protects against injection attacks, real-world experience tells a different story. Below you will find various examples from the field of ABAP development illustrating how you should not design your code and what countermeasures are effective.

### Attack vectors in ABAP

**Native SQL – The Obvious Risk Factor:**
```abap
" DANGEROUS: Direct inclusion of user input
DATA: lv_where TYPE string.
lv_where = |MANDT = '{ sy-mandt }' AND KUNNR = '{ p_kunnr }'|.
EXEC SQL.
  SELECT * FROM KNA1 WHERE :lv_where
ENDEXEC.
```

An attacker could fill `p_kunnr` with `' OR '1'='1` and gain access to all customer data. It becomes even more critical with UPDATE or DELETE statements.

**OpenSQL – Supposedly safe, but treacherous:**
Even OpenSQL is not automatically immune to injection attacks, especially with dynamic WHERE clauses:
```abap
" DANGEROUS: Dynamic WHERE clause without validation
DATA: lv_where TYPE string.
lv_where = |KUNNR = '{ p_kunnr }'|.
SELECT * FROM kna1 WHERE (lv_where) INTO TABLE lt_customers.
```

**RFC function modules as a gateway:**
SQL injection vulnerabilities become particularly critical when they can be exploited through RFC interfaces. An insecure function module can become a springboard for attacks from across the network. The RFC_READ_TABLE function module is one example that uses dynamic programming.

### Effective defense measures

**1. Use parameterized queries:**
```abap
" SECURE: Use host variables
SELECT * FROM kna1
  WHERE kunnr = @p_kunnr
  INTO TABLE @lt_customers.
```

**2. Implement input validation:**
```abap
" Validate input before database access
IF p_kunnr CA ';''"`*%_'.
  MESSAGE 'Invalid characters in input' TYPE 'E'.
ENDIF.
```

**3. Use escaping functions:**
For unavoidable dynamic constructs, SAP's own escaping functions should be used to neutralize dangerous characters.

## Cross-Site Scripting (XSS) in SAP Web Applications

With the growing adoption of web-based SAP applications such as Fiori, UI5 and Web Dynpro, XSS-attacks have become a significant security risk. ABAP developers must understand how backend logic contributes to the frontend security.

### XSS attack vectors in SAP

**Stored XSS in master data:**
```abap
" DANGEROUS: Unfiltered HTML code in output
DATA: lv_name TYPE kna1-name1.
lv_name = '<script>alert("XSS")</script>Example Corp'.
" Direct output without encoding leads to XSS
```

When this customer name is later displayed in a web application, the JavaScript code is executed. Particularly treacherous: The malicious code is stored persistently in the database and affects all users who view this data.

**Reflected XSS in URL parameters:**
Web Dynpro and BSP applications that include URL parameters directly in HTML output are vulnerable to Reflected XSS. A crafted link can be enough to inject malicious code.

**DOM-based XSS in modern UI5 applications:**
When integrating ABAP backend data into modern frontend frameworks, new attack vectors emerge when JSON responses contain unfiltered user data.

### Protection measures against XSS

**1. Implement output encoding:**
```abap
" HTML encoding for web output
DATA: lv_encoded TYPE string.
lv_encoded = cl_http_utility=>escape_html( lv_user_input ).
```

**2. Use Content Security Policy (CSP):**
Configure CSP headers in your web applications to prevent inline JavaScript execution.

**3. Input validation in the backend:**
Implement strict validation rules for all input that will later be presented in web applications.

## Insecure Direct Object Access and Authorization Bypass

This class of vulnerability arises when ABAP programs directly accept object references from user input without verifying whether the user is authorized to access those objects.

### Typical attack patterns

**Horizontal privilege escalation:**
A clerk changes a customer number in a URL parameter and suddenly gains access to other customers' data for which he does not have authorization.

**Vertical privilege escalation:**
By manipulating organizational units or company codes in parameters, a user can access data that does not correspond to their hierarchy level.

**Session Hijacking through Predictable IDs:**
When internal object IDs or session identifiers are predictable, attackers can systematically try different values.

### Effective authorization checks

**1. Explicit authorization check:**
```abap
" Always perform an explicit authorization check
AUTHORITY-CHECK OBJECT 'F_KNA1_BEK'
  ID 'KUNNR' FIELD p_kunnr
  ID 'ACTVT' FIELD '03'.
IF sy-subrc <> 0.
  MESSAGE 'Not authorized' TYPE 'E'.
ENDIF.
```
The following applies to all objects with ABAP code:
1) do the authorization check
2) Don't forget SY-SUBRC evaluation
3) Expand ranges accordingly with SIGN = 'E' and 'EQ'
4) Make SELECT on the main table

In many cases, business departments have debugging authorizations to that development teams can provide support more efficiently. In such cases, a user could set a breakpoint and download the entire table through the debugger before the authorization check is executed.

**2. Contextual authorization:**
Not only check the authorization for an object, but also the context of the request (organizational unit, time period, etc.). Don't be afraid to run a query multiple times.

## Code Injection and Dynamic Programming Risks

ABAP provides powerful dynamic programming capabilities that can lead to serious security vulnerabilities if used improperly.

### Dangerous dynamic constructs

**GENERATE SUBROUTINE POOL:**
```abap
" EXTREMELY DANGEROUS: Direct code generation
DATA: lv_code TYPE string.
lv_code = |FORM test. WRITE '{ p_input }'. ENDFORM.|.
GENERATE SUBROUTINE POOL lv_code NAME lv_prog.
```

If `p_input` contains malicious code, it will be executed at runtime.

**Dynamic method calls:**
```abap
" DANGEROUS: Uncontrolled method calls
CALL METHOD (p_class)=>(p_method).
```

An attacker could call critical system methods or manipulate data.

### Secure alternatives

**1. Whitelist approach:**
Allow only defined values, methods and parameters and block all unknown options.

```abap
" Allow only permitted values
CASE p_method.
  WHEN 'GET_DATA' OR 'SAVE_DATA'.
    CALL METHOD (lv_class)=>(p_method).
  WHEN OTHERS.
    MESSAGE 'Method call is not permitted' TYPE 'E'.
ENDCASE.
```

**2. Use the factory pattern:**
Implement factory classes that only return safe, predefined objects.

**3. Use reflection APIs securely:**
If RTTI (Run Time Type Information) is used, implement strict validation and authorization checks.

### Preventive measures

The most effective defense against these threats is a combination of technical measures and organizational processes:

- **Security-focused code reviews:** Train your team to recognize these vulnerability patterns
- **Automated security testing:** Use tools like the SAP Code Vulnerability Analyzer
- **Penetration Testing:** Have your systems and applications tested regularly by SAP specialized security experts
- **Incident Response Plan:** Define processes for dealing with discovered vulnerabilities
