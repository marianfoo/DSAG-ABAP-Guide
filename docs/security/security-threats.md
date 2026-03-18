---
layout: page
title: Bedrohungen
permalink: /security/threats/
parent: Security
nav_order: 3
---

{: .no_toc}

# Bedrohungen

1. TOC
{:toc}  

## SQL injection in ABAP: attack vectors and defenses

SQL injection is one of the most dangerous and often overlooked vulnerabilities in ABAP systems. While many developers believe that OpenSQL automatically protects against injection attacks, practice shows a different picture. Below you will find various examples from the area of ​​ABAP development, how you should not design the development and what helps as a countermeasure.

### Attack vectors in ABAP

**Native SQL – The Obvious Risk Factor:**
```abap
" GEFÄHRLICH: Direkte Einbindung von Benutzereingaben
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
" GEFÄHRLICH: Dynamische WHERE-Klausel ohne Validierung
DATA: lv_where TYPE string.
lv_where = |KUNNR = '{ p_kunnr }'|.
SELECT * FROM kna1 WHERE (lv_where) INTO TABLE lt_customers.
```

**RFC function blocks as a gateway:**
SQL injections become particularly critical when they can be exploited via RFC interfaces. An insecure function block can become a springboard for attacks from the entire network. The RFC_READ_TABLE function block implements such dynamic programming.

### Effective defense measures

**1. Parametrisierte Queries verwenden:**
```abap
" SICHER: Verwendung von Platzhaltern
SELECT * FROM kna1 
  WHERE kunnr = @p_kunnr 
  INTO TABLE @lt_customers.
```

**2. Input-Validierung implementieren:**
```abap
" Validierung von Eingaben vor Datenbankzugriff
IF p_kunnr CA ';''"`*%_'.
  MESSAGE 'Ungültige Zeichen in Eingabe' TYPE 'E'.
ENDIF.
```

**3. Escaping-Funktionen nutzen:**
For unavoidable dynamic constructs, SAP's own escaping functions should be used to neutralize dangerous characters.

## Cross-Site Scripting (XSS) in SAP web applications

As SAP applications become more web-based through Fiori, UI5 and Web Dynpro, XSS attacks are becoming a critical risk factor. ABAP developers need to understand how their backend logic contributes to frontend security.

### XSS attack vectors in SAP

**Stored XSS in master data:**
```abap
" GEFÄHRLICH: Ungefilterter HTML-Code in Ausgabe
DATA: lv_name TYPE kna1-name1.
lv_name = '<script>alert("XSS")</script>Kunde GmbH'.
" Direkte Ausgabe ohne Encoding führt zu XSS
```

When this customer name is later displayed in a web application, the JavaScript code is executed. Particularly treacherous: The malicious code is stored persistently in the database and affects all users who view this data.

**Reflected XSS in URL parameters:**
Web Dynpro and BSP applications that include URL parameters directly in HTML output are vulnerable to Reflected XSS. A crafted link can be enough to inject malicious code.

**DOM-based XSS in modern UI5 applications:**
When integrating ABAP backend data into modern frontend frameworks, new attack vectors emerge when JSON responses contain unfiltered user data.

### Protection measures against XSS

**1. Output-Encoding implementieren:**
```abap
" HTML-Encoding für Web-Ausgabe
DATA: lv_encoded TYPE string.
lv_encoded = cl_http_utility=>escape_html( lv_user_input ).
```

**2. Content Security Policy (CSP) nutzen:**
Configure CSP headers in your web applications to prevent inline JavaScript execution.

**3. Eingabevalidierung am Backend:**
Implement strict validation rules for all input that will later be presented in web applications.

## Insecure direct access to objects and authorization bypass

This class of vulnerabilities arise when ABAP programs take object references directly from user input without checking whether the user is authorized to access these objects.

### Typische Angriffsmuster

**Horizontale Rechteausweitung:**
A clerk changes a customer number in a URL parameter and suddenly gains access to other customers' data for which he does not have authorization.

**Vertikale Rechteausweitung:**
By manipulating organizational units or company codes in parameters, a user can access data that does not correspond to their hierarchy level.

**Session Hijacking through Predictable IDs:**
When internal object IDs or session identifiers are predictable, attackers can systematically try different values.

### Effective authorization checks

**1. Explicit authorization check:**
```abap
" Immer explizite Berechtigung prüfen
AUTHORITY-CHECK OBJECT 'F_KNA1_BEK'
  ID 'KUNNR' FIELD p_kunnr
  ID 'ACTVT' FIELD '03'.
IF sy-subrc <> 0.
  MESSAGE 'Keine Berechtigung' TYPE 'E'.
ENDIF.
```
The following applies to all objects with ABAP code: 
1) do the authorization check
2) Don't forget SY-SUBRC evaluation
3) Expand ranges accordingly with SIGN = 'E' and 'EQ'
4) Make SELECT on the main table

In many cases, departments have debugging authorization so that development can help quickly in the event of support. In such cases, a clerk could set a break point and download the entire table via the debugger before the authorization check.

**2. Kontextuelle Autorisierung:**
Not only check the authorization for an object, but also the context of the request (organizational unit, time period, etc.). Don't be afraid to run a query multiple times.

## Code injection and dynamic programming risks

ABAP provides powerful dynamic programming features that can lead to serious security vulnerabilities if used improperly.

### Dangerous dynamic constructs

**GENERATE SUBROUTINE POOL:**
```abap
" EXTREM GEFÄHRLICH: Direkte Code-Generierung
DATA: lv_code TYPE string.
lv_code = |FORM test. WRITE '{ p_input }'. ENDFORM.|.
GENERATE SUBROUTINE POOL lv_code NAME lv_prog.
```

If `p_input` contains malicious code, it will be executed at runtime.

**Dynamische Methodenaufrufe:**
```abap
" GEFÄHRLICH: Unkontrollierte Methodenaufrufe
CALL METHOD (p_class)=>(p_method).
```

An attacker could call critical system methods or manipulate data.

### Sichere Alternativen

**1. Whitelist-Ansatz:**
Allow only defined values, methods and parameters and block all unknown options.

```abap
" Nur erlaubte Werte zulassen
CASE p_method.
  WHEN 'GET_DATA' OR 'SAVE_DATA'.
    CALL METHOD (lv_class)=>(p_method).
  WHEN OTHERS.
    MESSAGE 'Unerlaubter Methodenaufruf' TYPE 'E'.
ENDCASE.
```

**2. Factory-Pattern verwenden:**
Implement factory classes that only return safe, predefined objects.

**3. Reflection-APIs sicher nutzen:**
If RTTI (Run Time Type Information) is used, implement strict validation and authorization checks.

### Preventive measures

The most effective defense against these threats is a combination of technical measures and organizational processes:

- **Security-focused code reviews:** Train your team to recognize these vulnerability patterns
- **Automated security testing:** Use tools like the SAP Code Vulnerability Analyzer
- **Penetration Testing:** Have your systems and applications tested regularly by SAP specialized security experts
- **Incident Response Plan:** Define processes for dealing with discovered vulnerabilities