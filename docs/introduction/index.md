---
layout: page
title: Introduction
permalink: /introduction/
nav_order: 0
---

{: .no_toc}
# Introduction

1. TOC
{:toc}

{: .important }
> **Machine-Translated Version**
> This chapter is part of an unofficial machine-translated English version of the original German DSAG ABAP-Leitfaden.
> The translation is published with the authors' allowance.
> The original German source remains authoritative: [https://1dsag.github.io/ABAP-Leitfaden/](https://1dsag.github.io/ABAP-Leitfaden/).

## The New DSAG ABAP Guide

A warm welcome to DSAG’s new “ABAP Guide”. Before you lies a comprehensive document on the subject of application development in SAP.

As standard software, SAP’s Business Suite is characterized by a high degree of flexibility and extensibility. In almost all companies that use SAP software, there are customer-specific customizations and enhancements. SAP software is therefore subject to continuous adaptation and enhancement by both the vendor and the customer in response to changing customer needs. This flexibility and extensibility bring both advantages and disadvantages:

* The software can be tailored perfectly to specific customer requirements, thereby significantly increasing the value added through its use.
* At the same time, this extensibility carries the risk of customized developments that are complex, costly to maintain and prone to errors.

Previous editions of the ABAP Guide were published in 2012 and 2016. Since then, application development in SAP has changed significantly and become considerably more complex. Whereas in the past the majority of development took place using ABAP and GUI-based tools, it is now necessary to use and master a variety of technologies and tools. Major innovations include:

* The introduction of the ABAP Development Tools (ADT)
* HANA database
* S/4HANA Business Suite
* CDS for data modelling
* the RESTful Application Programming Model (RAP)
* and the rapid evolution of the ABAP programming language towards ABAP Cloud

Consequently, there were calls within the SAP community for an updated guide to be made available that takes account of the latest developments in SAP.

In 2024, following a call from DSAG, a team of experts in the SAP field came together once again to produce a new version of the ABAP guide, which provides guidance, advice and practical tips to business managers, developers and consultants alike, helping them use both established and new technologies for application development successfully and effectively.

## Structure and Content of the Guide

The key factors for a successful transition to modern ABAP development do not lie primarily in technical issues, but are shaped by the framework conditions that a development team encounters. At the start of this guide, you will find explanations and recommendations regarding **development organization**, which will provide guidance on how to establish the framework conditions for modern application development in SAP.  
You will then be given an overview of the concepts of **“Clean Core”** and recommendations on how to proceed. Understanding the Clean Core concept is important so that you can define your strategies and also understand how the new development methodologies put the Clean Core approach into practice. This will already give you a good overview of the framework conditions.  

The topics

* **Core Data Services**
* **ABAP**
* **ABAP Unit Test**
* **User Interfaces and**
* **Forms**

provide explanations, recommendations and details on the technical aspects and technologies of modern SAP development.  
At the start of each chapter, you will find introductory information and an overview of the topic. This section is primarily intended for managers and decision-makers within the company who wish to gain an overview of the subject area.  
The further you delve into the chapter, the more detailed the information on the individual topics becomes. These sections are particularly suitable for architects, developers and those with a technical interest who wish to gain a more detailed insight into the subject.  

In the following section, you will find sections on **open source**, including key explanations of why open source is also important in the ABAP domain, as well as sections on Application Lifecycle Management (ALM), where you will also find explanations of modern methods of **version control**.  
Finally, you will find further discussion on the topics of **security** and **integration**, which are more important than ever in the development of SAP software today. And, of course, we must not forget to mention artificial intelligence.

## Positioning

SAP provides a wealth of documentation on application development and the extension of the SAP platform. Specialist publishers have also published very good publications on this subject. Furthermore, there are now numerous freely available learning journeys covering various topics. Nevertheless, it is not easy to find one’s way through the jungle of tools and techniques.  
The value of this document lies in its summary of best practices, practical tips and tried-and-tested guidelines from user organizations. This guide therefore addresses the topics primarily from a slightly broader perspective.

This guideline is intended to provide you – whether you are a user, developer, or a development, project or IT manager – with ideas and assistance so that you do not have to ‘keep reinventing the wheel’ and can build on the experience of others. The recommendations set out in this guideline do not claim to be exhaustive or universally applicable but rather represent a selection of practical tips.

As a team of authors, we have endeavored to strike the right balance between providing an overview and delving into the finer details. We therefore refer readers to further sources or recommended reading where appropriate, so as not to repeat topics that have already been discussed at length.  

## Motivation

Some of the newer technologies and tools are not yet widely adopted, even though they have been available for years. The team of authors therefore aims to demonstrate, by highlighting the benefits and opportunities, why it is worthwhile to invest in these new methods and to explore new approaches to application development.  
This guide is intended to help you assess the current state of SAP development within your company and identify areas of action for achieving efficient and effective SAP development.  
To do this, the framework conditions in the SAP development environment must be adapted or even changed. The ABAP Guide is designed to help you overcome any reservations, make it easier to get started with these topics, and encourage you to actively seek out and promote the topics described in the guide.

## Feedback

In addition to the printable version, this guide will also be available as a digital edition as a Git repository on the Internet:  
[DSAG ABAP Guide Git Pages](https://1dsag.github.io/ABAP-Leitfaden/) and [DSAG ABAP Guide Git repository](https://github.com/1DSAG/ABAP-Leitfaden).  
This also gives you the opportunity to get involved and contribute feedback, corrections, and additions to the guide via Git issues. This document thrives on the community and reader feedback. DSAG and the team of authors welcome any feedback on the ABAP Guide and are interested in hearing whether and how the guide has helped you, as well as where you would like to see further detail.  

## Disclaimer

This document is based on the collective knowledge of DSAG members in various fields and is further developed by the community. As a result, there may be deviations from SAP’s standard procedures or best practices if a company has had different experiences.
