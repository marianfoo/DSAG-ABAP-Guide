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

Here you will find further examples and descriptions of vulnerabilities

## Directory Traversal (Write Access)

Directory traversal attacks work by manipulating the file name or path information by entering special characters into a string that acts as a file locator.

If such a string is used to modify the contents of a file, an application can be tricked into modifying files that the user should not have access to. This attack is possible because the application fails to detect and remove command characters in input used as part of the file locator.

This affects files in all directories to which the vulnerable application has write access. This can also include files on the company LAN. By controlling which files an application will modify, at least the following attacks are possible:

- Write access to critical configuration files. This can give attackers the opportunity to penetrate even further into a system that has already been attacked.
- Write access to log files.
- Write access to the data persistence of a productive database.

All of these risks jeopardize the integrity of the productive SAP server.  Many applications access files on the SAP server to write data. Typical use cases include temporary persistence of file uploads and exporting business data for adoption from a legacy system. At the operating system level, files are identified by file locators. These file locators contain information about the drive or file share, directory, name and extension of a particular file. There are cases where part of such file locator information is based on external input. For example, the name of a file uploaded to the server can also be used to save it to a temporary folder. However, external input can contain special characters that can be used to manipulate the overall file locator. As a result, files from other drives, file shares or other directories may be modified. Files of other file types or extensions can also be accessed if necessary. Such an attack is called a directory traversal attack. Illegal directory changes allow an unauthorized user to modify arbitrary files on the SAP server running the vulnerable application. Depending on the file access mode, an attacker can either modify or delete data. This vulnerability leads to improper use of the ABAP commands OPEN DATASET FOR OUTPUT, OPEN DATASET FOR APPENDING, DELETE DATASET, TRUNCATE DATASET and TRANSFER. Such security gaps can compromise the integrity of a productive SAP server. An attacker can delete or modify files that are critical to proper system operation. Additionally, an attacker can modify and delete files containing business data. In any case, unauthorized write access to any file on a server represents a critical security risk. The likelihood of a particular problem changes if a postfix is ​​added to the input.

## Generic ABAP Module Calls

By controlling which ABAP modules are running on a SAP system, at least the following attacks are possible: Crash of the SAP application server Disruption of business logic, resulting in an inconsistent data state Manipulation of business logic, resulting in unprivileged access to protected functions Some of these risks may violate legal requirements because such vulnerabilities allow unprivileged access to critical business logic enable. Details In ABAP there are commands that dynamically call transactions, function modules, methods, forms and reports. Dynamic means that the name of the block to be executed is determined based on the input at runtime. Dynamic block calls are an important feature for writing flexible and reusable code. However, this can be very dangerous if such a device is controlled by a malicious user. Findings take into account the existence of an AUTHORITY CHECK. Indirect AUTHORITY CHECKs (called in submodules) are also taken into account. The likelihood of a particular issue changes when a prefix or postfix is ​​added to the input.

## OS Command Injection (CALL 'SYSTEM')

This test case checks whether an (external) input is executed as an operating system command using the kernel function 'SYSTEM'. In such a case, an attacker could execute arbitrary commands on the SAP application server. Risk Executing arbitrary operating system commands can lead to the following risks: Crash of the SAP application server Installation of malware Creation of privileged user accounts Read/write access to all files of the SAP application server Details The kernel function 'SYSTEM' allows the execution of arbitrary operating system commands. When this processes (external) input, the standard SAP security mechanism for executing operating system commands is bypassed. Using transactions SM49 or SM69, administrators can maintain a list of permitted operating system commands and assign appropriate authorizations for their execution. This allows an administrator to restrict access to dangerous commands. However, the kernel function 'SYSTEM' bypasses the command list from SM49/SM69. For this reason, any operating system command can be executed using the kernel function 'SYSTEM'. This represents a critical security risk.

## ABAP Command Injection (Report)

The ABAP INSERT REPORT and SUBMIT commands together can create and execute dynamic ABAP code at runtime, which can pose a very high security risk if user input is part of such a dynamic report. Risk If a user can execute any ABAP commands on a SAP system, the system must be considered fully compromised: Read and write access to all (business) data in the database Execution of any business logic Such vulnerabilities constitute compliance violations. Details The ABAP INSERT REPORT command is used to dynamically generate a ABAP report. This is done by concatenating character strings that are usually read from a data source. Once the ABAP report has been compiled, it can be executed using the GENERATE REPORT command. Such a programming approach is very dangerous because it allows malicious code to be created spontaneously and leaves no trace of this code in the system.

## Dangerous ABAP Commands

This test case tests the use of the ABAP commands EDITOR-CALL FOR REPORT and COMMUNICATION. Note that this test case determines starting points for further testing and requires manual post-processing. Risk Business risk depends on the discovered functionality and must be determined through manual analysis. Details This test case affects the following ABAP commands: EDITOR-CALL FOR REPORT COMMUNICATION These commands are either critical or obsolete. In any case, they should not be included in your own code. EDITOR-CALL FOR REPORT allows calling a ABAP editor for source code. Special development permissions are still required. Homegrown code should not provide a ABAP code editor. This should only be possible through standard SAP functions that can be properly restricted and audited. COMMUNICATION was used to exchange system data and was used before RFC was available. This type of data exchange is obsolete. From a security perspective, there is a risk because security functions such as: B. SNC cannot be used for COMMUNICATION-based data exchange.
