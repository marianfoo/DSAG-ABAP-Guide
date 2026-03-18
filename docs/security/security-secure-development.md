---
layout: page
title: Sichere Entwicklung
permalink: /security/secure-development/
parent: Security
nav_order: 4
---

{: .no_toc}

# Sichere Entwicklung

1. TOC
{:toc}  

In an increasingly digitalized business world, securing ABAP applications is essential. Security begins with development – ​​​​through consistently applied secure programming practices.

## Input validation: The first protective barrier

Validating user input is one of the most effective lines of defense against attacks. Without validation, manipulated input can lead to code injections or unauthorized access. Therefore, only known and expected values ​​​​should be accepted in ABAP. Whitelists, input masks and type checks are useful here. A prior plausibility check is essential, especially for dynamic SQL statements or file operations.

**Whitelist-Ansatz bevorzugen:**
```abap
" SICHER: Nur erlaubte Zeichen zulassen
IF p_kunnr CO '1234567890'.
  " Verarbeitung nur für numerische Kundennummern
ELSE.
  MESSAGE 'Kundennummer darf nur Ziffern enthalten' TYPE 'E'.
ENDIF.
```

**Data type and length check:**
```abap
" Explizite Längen- und Formatprüfung (Gerne mit REGEX arbeiten)
IF strlen( p_email ) > 50 OR p_email CN '@.'.
  MESSAGE 'Ungültige E-Mail-Adresse' TYPE 'E'.
ENDIF.
```
**Harden web service inputs:**
For SOAP and REST services, in addition to the above input validations, XML/JSON content passed as a string may also need to be checked for structural integrity before it is deserialized into ABAP structures.

## Output-Encoding: Daten sicher ausgeben

With web technologies such as BSP, Web Dynpro or UI5, unsafe output can lead to Cross Site Scripting (XSS). To prevent this, consistent output encoding is necessary. SAP's own method `cl_http_utility=>escape_html` offers a simple way to secure HTML output. All potentially dangerous characters should be defused during output, especially when user input appears in HTML, JavaScript, or XML contexts.

### HTML encoding for web applications

```abap
" HTML-Encoding für Web-Ausgabe
DATA: lv_encoded TYPE string.
lv_encoded = cl_http_utility=>escape_html( lv_user_input ).
```

## Sichere Datenbankzugriffe: OpenSQL Best Practices

OpenSQL provides an abstracted and secure way to access data. However, security risks arise from dynamic statements, especially when table or WHERE conditions are generated from user input. Using `CLIENT SPECIFIED` or direct SQL manipulation (e.g. `EXEC SQL`) can lead to tenant overruns and audit bypass. Best practices here include:

* Use of fixed table and field names
* No dynamic WHERE clauses from user input
* No direct access with native SQL
* Waiver of `MODIFY` without checking permissions
* Do not use tenant exceedances

### Dynamische WHERE-Klauseln absichern

```abap
" Sichere Implementierung dynamischer Abfragen
DATA: lt_where TYPE stringtab,
      lv_where TYPE string.

" Whitelist für erlaubte Felder
CASE p_field.
  WHEN 'KUNNR' OR 'NAME1' OR 'ORT01'.
    APPEND |{ p_field } = @p_value| TO lt_where.
  WHEN OTHERS.
    MESSAGE 'Unerlaubtes Feld in Abfrage' TYPE 'E'.
ENDCASE.

SELECT * FROM kna1 WHERE (lt_where) INTO TABLE @lt_result.
```

## Implement authorization checks correctly

A common mistake is missing or incomplete authority checks. Every security-relevant access must be secured by `AUTHORITY-CHECK` and the return value `sy-subrc` must be evaluated immediately. The following are particularly problematic:

* Checks with DUMMY fields (e.g. `ACTVT = ' '`)
* Checks for superuser permissions (`*`)
* missing check after `AUTHORITY-CHECK` on `SY-SUBRC`
* Use of alias users in `SUBMIT ... USER` statements

It must also be ensured that customer programs are provided with an authorization group in order to trigger implicit checks. For a good UI and secure programming, it is recommended to check the most important authorization objects with `DUMMY` immediately after the start, before the user input, in order not to burden both the application server and the database server with requests that are not authorized afterwards anyway.
For example, a report displays data for a customer in a sales organization. The report is provided with a Z authorization object to check whether the user is allowed to see this customer. Here, the authorization object can be checked against dummy objects the first time it is called (INITIALIZATION in the report). If this fails, the user doesn't need to bother finding a combination that works.

```abap
" Vollständige Berechtigungsprüfung
AUTHORITY-CHECK OBJECT 'Z_KNA1_BEK'
  ID 'KUNNR' FIELD lv_kunnr
  ID 'ACTVT' FIELD '03'
  ID 'VKORG' FIELD lv_vkorg.

CASE sy-subrc.
  WHEN 0.
    " Berechtigung vorhanden
  WHEN 4.
    MESSAGE 'Keine Berechtigung für Kunde' TYPE 'E'.
  WHEN 12.
    MESSAGE 'Berechtigungsobjekt für den User nicht gepflegt' TYPE 'E'.
ENDCASE.
```

### Permissions in CDS Views

CDS Views bring a paradigmatic change to the SAP authorization logic with the Data Control Language (DCL). While traditional ABAP programs must implement authorization checks explicitly in code, permissions in CDS Views are defined declaratively at the data level. DCL makes it possible to define authorization logic directly on the data structures instead of implementing it in every consuming report or application. This reduces redundancy and workload and significantly increases the consistency of authorization checks.

With the consistent use of DCL, well thought-out authorization concepts and regular security checks, you can take advantage of the advantages of CDS.

Investing in secure CDS development pays off in the long term. It makes it possible to develop modern SAP applications that are both performant and secure.

### Always check organizational authorizations completely

```abap
" Mehrstufige Berechtigungsprüfung
" 1. Funktionale Berechtigung
AUTHORITY-CHECK OBJECT 'Z_BKPF_BUK'
  ID 'BUKRS' FIELD lv_bukrs
  ID 'ACTVT' FIELD '02'.
IF sy-subrc <> 0.
    RAISE EXCEPTION TYPE zcx_no_authority.
 ENDIF.

" 2. Organisatorische Berechtigung  
AUTHORITY-CHECK OBJECT 'Z_BKPF_GSB'
  ID 'GSBER' FIELD lv_gsber
  ID 'ACTVT' FIELD '02'.
IF sy-subrc <> 0.
    RAISE EXCEPTION TYPE zcx_no_authority.
 ENDIF.
```

### Secure RFC and web service communication

Remote Function Calls (RFC) represent a central communication element, but are only authorized for authorization in the target system. The use of Trusted RFC connections increases the risk of uncontrolled function calls. Therefore RFCs must:

* be secured with,
* be specifically authorized by role assignment,
* In the case of external communication, be secured with whitelisting.

For web services, particular attention must be paid to the secure transfer of parameters and clean serialization/deserialization.

### RFC-Funktionsbausteine absichern

```abap
FUNCTION z_secure_customer_read.
  " Berechtigungsprüfung am Funktionseinstieg
  AUTHORITY-CHECK OBJECT 'Z_FUNC'
    ID 'ACTVT' FIELD '03'.
  
  IF sy-subrc <> 0.
    RAISE EXCEPTION TYPE zcx_no_authority.
  ENDIF.
```

## Mandantensicherheit: Datentrennungen garantieren

SAP systems are based on the strict separation of clients. However, this separation is broken if `CLIENT SPECIFIED` is used improperly. Programs may not contain cross-client access unless this is absolutely necessary and authorized. Data integrity and compliance requirements require that client limits are adhered to and regularly audited.

## Secure file access and path traversal protection

File accesses are particularly critical because they access the server's file system directly. ABAP offers `OPEN DATASET`, `READ`, `TRANSFER` etc., all of which are secured via the object `S_DATASET`. Protective measures include:

* Use of `AUTHORITY_CHECK`
* Verwendung logischer Dateinamen (Transaktion FILE)
* Avoiding directory traversal by blocking ".." or `/`
* Maintain table `SPTH`

In addition, file uploads/downloads should only take place via dialog functions of the `CL_GUI_FRONTEND_SERVICES` in order to enable a security check on the client side.

**Pfadvalidierung implementieren**

```abap
" Sichere Pfadvalidierung
DATA: lv_safe_path TYPE string,
      lv_filename TYPE string.

" Nur erlaubte Zeichen in Dateinamen
IF p_filename CA '\/:*?"<>|'.
  MESSAGE 'Ungültige Zeichen im Dateinamen' TYPE 'E'.
ENDIF.

" Pfadtraversal verhindern
IF p_filename CS '..'.
  MESSAGE 'Pfadtraversal-Versuch erkannt' TYPE 'E'.
ENDIF.

" Sicheren Basispfad verwenden
lv_safe_path = |/secure/upload/{ p_filename }|.
```

## Generelles
In general, current techniques in other languages ​​​​should always be checked to see whether and in what way they are relevant in ABAP. With some techniques the risk shifts but remains the same.