---
layout: page
title: More examples
permalink: /security/additional-examples/
parent: Security
nav_order: 6
---

{: .no_toc}

# Examples

1. TOC
{:toc}

Here you will find additional examples and descriptions of security vulnerabilities.

## Directory Traversal (Write Access)

Directory traversal attacks work by manipulating the filename or path information through the inclusion of special characters in a string that serves as a file locator.

If such a string is used to modify the contents of a file, an application can be tricked into modifying files that the user should not have access to. This attack is possible because the application fails to detect and remove command characters in inputs that are used as part of the file locator.

This affects files in all directories to which the vulnerable application has write access. This may also include files on the corporate LAN. By controlling which files an application modifies, at least the following attacks are possible:

- Write access to critical configuration files. This can allow attackers to penetrate an already compromised system even further.
- Write access to log files.
- Write access to the data persistence layer of a production database.

All of these risks compromise the integrity of the production SAP server. Many applications access files on the SAP server to write data. Typical use cases include the temporary storage of file uploads and the export of business data for transfer from a legacy system. At the operating system level, files are identified by file locators. These file locators contain information about the drive or file share, the directory, the name, and the extension of a specific file. There are cases where part of this file locator information is based on external input. For example, the name of a file uploaded to the server can also be used to save it to a temporary folder. However, external input may contain special characters that can be used to manipulate the file locator. As a result, files on other drives, file shares, or other directories may be altered. Files of other types or with different extensions may also be accessible. Such an attack is known as a directory traversal attack. By performing unauthorized directory traversals, an unauthorized user can modify any files on the SAP server where the vulnerable application is running. Depending on the file access mode, an attacker can either modify or delete data. This vulnerability results from the improper use of the ABAP commands OPEN DATASET FOR OUTPUT, OPEN DATASET FOR APPENDING, DELETE DATASET, TRUNCATE DATASET, and TRANSFER. Such security vulnerabilities can compromise the integrity of a production SAP server. An attacker can delete or modify files that are critical to proper system operation. Additionally, an attacker can modify and delete files containing business data. In any case, unauthorized write access to any file on a server represents a critical security risk. The likelihood of a particular problem changes if a postfix is added to the input.

## Generic ABAP Module Calls

By controlling which ABAP modules run on an SAP system, an attacker could cause at least the following:

- A crash of the SAP application server
- A malfunction in the business logic, resulting in inconsistent data
- Manipulation of the business logic, resulting in unauthorized access to protected functions

Some of these risks may violate legal requirements because such vulnerabilities allow unauthorized access to critical business logic.

**Details**

ABAP provides statements that dynamically call transactions, function modules, methods, forms, and reports. “Dynamically” means that the name of the module to execute is determined at runtime based on user input. Dynamic module calls are useful for writing flexible and reusable code. However, they can be dangerous if a malicious user can control which module is called. Findings take into account the presence of an AUTHORITY-CHECK, including indirect checks performed in called modules. The likelihood of a specific issue changes if a prefix or suffix is added to the input.

## OS Command Injection (CALL 'SYSTEM')

This test case checks whether external input is executed as an operating system command using the kernel function `SYSTEM`. If so, an attacker could execute arbitrary commands on the SAP application server.

**Risk**

Executing arbitrary operating system commands can lead to the following risks:

- A crash of the SAP application server
- Installation of malware
- Creation of privileged user accounts
- Read/write access to all files on the SAP application server

**Details**

The kernel function `SYSTEM` allows arbitrary operating system commands to be executed. If external input is processed in this way, the standard SAP security mechanism for executing operating system commands is bypassed. Using transactions SM49 or SM69, administrators can maintain a list of permitted operating system commands and assign the appropriate authorizations for their execution. This allows administrators to restrict access to dangerous commands. However, the kernel function `SYSTEM` bypasses the command list from SM49/SM69, creating a critical security risk.

## ABAP Command Injection (Report)

The ABAP statements `INSERT REPORT` and `SUBMIT` can work together to generate and execute dynamic ABAP code at runtime. If user input is included in such a report, this poses a significant security risk.

**Risk**

If a user can execute arbitrary ABAP statements on an SAP system, the system must be considered fully compromised. An attacker could:

- Read and modify any business data in the database
- Execute arbitrary business logic

Such security vulnerabilities may also constitute compliance violations.

**Details**

The statement `INSERT REPORT` is used to generate an ABAP report dynamically. This is done by concatenating strings, which are typically read from a data source. Once the ABAP report has been assembled, it can be executed using `SUBMIT` or compiled using `GENERATE REPORT`. This programming approach is dangerous because it allows malicious code to be created and executed without leaving the source code permanently stored in the system.

## Dangerous ABAP Commands

This test case checks the use of the ABAP statements `EDITOR-CALL FOR REPORT` and `COMMUNICATION`. It identifies starting points for further testing and requires manual follow-up.

**Risk**

The business risk depends on the identified functionality and must be determined through manual analysis.

**Details**

The statements `EDITOR-CALL FOR REPORT` and `COMMUNICATION` are either security-critical or obsolete and should not be included in custom-developed code. `EDITOR-CALL FOR REPORT` opens an ABAP source-code editor, although special development authorizations are still required. Custom code should not provide such an editor; source-code editing should remain limited to standard SAP functions that can be properly restricted and audited.

`COMMUNICATION` was used to exchange system data before RFC became available. This form of data exchange is obsolete and cannot use security features such as Secure Network Communications (SNC).
