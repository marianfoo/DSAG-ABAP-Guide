---
layout: page
title: Secure Development
permalink: /security/secure-development/
parent: Security
nav_order: 4
---

{: .no_toc}

# Secure Development

1. TOC
{:toc}  

In an increasingly digital business world, securing ABAP applications is essential. Security begins right at the development stage—through the consistent application of secure programming practices.

## Input Validation: The First Line of Defense

Validating user input is one of the most effective lines of defense against attacks. Without validation, manipulated inputs can lead to code injections or unauthorized access. In ABAP, therefore, only known and expected values should be accepted. Whitelists, input masks, and type checks are useful tools here. For dynamic SQL statements or file operations, a prior plausibility check is essential.

**Prefer a whitelist approach:**
```abap
" SECURE: Allow only permitted characters
IF p_kunnr CO '1234567890'.
  " Process only numeric customer numbers
ELSE.
  MESSAGE 'Customer number may contain digits only' TYPE 'E'.
ENDIF.
```

**Data type and length check:**
```abap
" Explicit length and format validation (a regular expression can be used)
IF strlen( p_email ) > 50 OR p_email CN '@.'.
  MESSAGE 'Invalid email address' TYPE 'E'.
ENDIF.
```
**Harden web service inputs:**
For SOAP and REST services, in addition to the above input validations, XML/JSON content passed as a string may also need to be checked for structural integrity before it is deserialized into ABAP structures.

## Output Encoding: Secure Data Output

In web technologies such as BSP, Web Dynpro, or UI5, insecure output can lead to Cross-Site Scripting (XSS) vulnerabilities. To prevent this, consistent output encoding is required. The SAP-provided method `cl_http_utility=>escape_html` offers a simple way to secure HTML output. All potentially dangerous characters should be neutralized before output, especially when user input is displayed in HTML, JavaScript, or XML contexts.

### HTML Encoding for Web Applications

```abap
" HTML encoding for web output
DATA: lv_encoded TYPE string.
lv_encoded = cl_http_utility=>escape_html( lv_user_input ).
```

## Secure Database Access: Open SQL Best Practices

OpenSQL provides an abstracted and secure way to access data. However, security risks arise from dynamic statements, especially when table or WHERE conditions are generated from user input. Using `CLIENT SPECIFIED` or direct SQL manipulation (e.g. `EXEC SQL`) can lead to tenant overruns and audit bypass. Best practices here include:

* Use of fixed table and field names
* No dynamic WHERE clauses from user input
* No direct access with native SQL
* Waiver of `MODIFY` without checking permissions
* Do not use tenant exceedances

### Securing Dynamic WHERE Clauses

```abap
" Secure implementation of dynamic queries
DATA: lt_where TYPE stringtab,
      lv_where TYPE string.

" Whitelist of permitted fields
CASE p_field.
  WHEN 'KUNNR' OR 'NAME1' OR 'ORT01'.
    APPEND |{ p_field } = @p_value| TO lt_where.
  WHEN OTHERS.
    MESSAGE 'Field is not permitted in the query' TYPE 'E'.
ENDCASE.

SELECT * FROM kna1 WHERE (lt_where) INTO TABLE @lt_result.
```

## Implementing Authorization Checks Correctly

A common mistake is missing or incomplete authorization checks. Every security-relevant access must be protected by an `AUTHORITY-CHECK`, and the return value `sy-subrc` must be evaluated immediately. Particularly problematic are:

* Checks with DUMMY fields (e.g. `ACTVT = ' '`)
* Checks for superuser permissions (`*`)
* missing check after `AUTHORITY-CHECK` on `SY-SUBRC`
* Use of alias users in `SUBMIT ... USER` statements

It must also be ensured that customer programs are provided with an authorization group in order to trigger implicit checks. For a good UI and secure programming, it is recommended to check the most important authorization objects with `DUMMY` immediately after the start, before the user input, in order not to burden both the application server and the database server with requests that are not authorized afterwards anyway.
For example, a report may display customer data within a sales organization. The report uses a custom authorization object to verify whether the user is allowed to view the customer. During the initial call (for example, in the INITIALIZATION event of the report), the authorization object can already be checked against dummy values. If the check fails at this stage, the user does not need to spend time trying to find a valid input combination.

```abap
" Complete authorization check
AUTHORITY-CHECK OBJECT 'Z_KNA1_BEK'
  ID 'KUNNR' FIELD lv_kunnr
  ID 'ACTVT' FIELD '03'
  ID 'VKORG' FIELD lv_vkorg.

CASE sy-subrc.
  WHEN 0.
    " Authorization granted
  WHEN 4.
    MESSAGE 'No authorization for customer' TYPE 'E'.
  WHEN 12.
    MESSAGE 'Authorization object is not maintained for the user' TYPE 'E'.
ENDCASE.
```

### Authorizations in CDS Views

CDS views introduce a paradigm shift in SAP authorization concepts through the use of Data Control Language (DCL). Whereas traditional ABAP programs must implement authorization checks explicitly in the code, authorizations in CDS views are defined declaratively at the data level. DCL makes it possible to define authorization logic directly within the data structures rather than implementing it separately in every consuming report or application. This reduces redundancy and implementation effort while increasing the consistency of authorization checks.

By consistently applying DCL, designing well-thought-out authorization concepts, and performing regular security reviews, you can fully leverage the benefits of CDS.

The investment in secure CDS development pays off in the long term. It enables the development of modern SAP applications that are both performant and secure.

### Always Check Organizational Authorizations Completely

```abap
" Multi-level authorization check
" 1. Functional authorization
AUTHORITY-CHECK OBJECT 'Z_BKPF_BUK'
  ID 'BUKRS' FIELD lv_bukrs
  ID 'ACTVT' FIELD '02'.
IF sy-subrc <> 0.
    RAISE EXCEPTION TYPE zcx_no_authority.
 ENDIF.

" 2. Organizational authorization  
AUTHORITY-CHECK OBJECT 'Z_BKPF_GSB'
  ID 'GSBER' FIELD lv_gsber
  ID 'ACTVT' FIELD '02'.
IF sy-subrc <> 0.
    RAISE EXCEPTION TYPE zcx_no_authority.
 ENDIF.
```

### Secure RFC and Web Service Communication

Remote Function Calls (RFCs) are a central communication mechanism but are authorized only in the target system. The use of trusted RFC connections increases the risk of uncontrolled function calls. Therefore, RFCs should:

* Be additionally secured through authorization checks,
* Be explicitly authorized through role assignments,
* Be protected through whitelisting when used for external communication.

For web services, particular attention should be paid to the secure handling of parameters and to proper serialization and deserialization.

### Securing RFC Function Modules

```abap
FUNCTION z_secure_customer_read.
  " Berechtigungsprüfung am Funktionseinstieg
  AUTHORITY-CHECK OBJECT 'Z_FUNC'
    ID 'ACTVT' FIELD '03'.
  
  IF sy-subrc <> 0.
    RAISE EXCEPTION TYPE zcx_no_authority.
  ENDIF.
```

## Client Security: Ensuring Data Separation

SAP systems are based on the strict separation of clients. However, this separation can be bypassed through improper use of `CLIENT SPECIFIED`. Programs should not contain cross-client access unless it is absolutely necessary and properly authorized. Data integrity and compliance requirements mandate that client boundaries are respected and regularly audited.

## Secure File Access and Protection Against Path Traversal

File access is security-critical because it provides direct access to the server file system.

ABAP provides statements such as `OPEN DATASET`, `READ`, `TRANSFER` etc., all of which are protected through authorization object `S_DATASET`. Recommended security measures include:

* Use of `AUTHORITY_CHECK`
* Use of logical file names (Transaction FILE)
* Prevention of directory traversal by blocking sequences such as ".." or `/`
* Maintenance of table `SPTH`

In addition, file uploads and downloads should only be performed through the dialog functions of `CL_GUI_FRONTEND_SERVICES`, enabling security checks on the client side.

**Implement path validation**

```abap
" Secure path validation
DATA: lv_safe_path TYPE string,
      lv_filename TYPE string.

" Allow only permitted characters in filenames
IF p_filename CA '\/:*?"<>|'.
  MESSAGE 'Invalid characters in filename' TYPE 'E'.
ENDIF.

" Prevent path traversal
IF p_filename CS '..'.
  MESSAGE 'Path traversal attempt detected' TYPE 'E'.
ENDIF.

" Use a secure base path
lv_safe_path = |/secure/upload/{ p_filename }|.
```

## General
In general, current techniques in other languages should always be checked to see whether and in what way they are relevant in ABAP. With some techniques the risk shifts but remains the same.
