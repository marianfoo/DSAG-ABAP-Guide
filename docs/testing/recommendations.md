---
layout: page
title: Empfehlungen
permalink: /testing/recommendations/
parent: Software test with ABAP unit
nav_order: 99
---


{: .no_toc}
# Empfehlungen

1. TOC
{:toc}

Below we would like to try to put together a recommendation from the wealth of information that will give you and your team a quick and sustainable start.

## Konsens

Unit tests and therefore code quality are not an end in themselves, but an important component for your productive software products. That's why, in our opinion, there is no excuse not to use unit tests. 

There are two different perspectives that have to fit together:
1. Developers must want to create unit tests
2. Management must support the use of unit tests

If developers are forced to create unit tests but refuse to do so for various reasons, then there will be no or useless unit tests.
If management does not support the developers and does not provide backing (training, time, etc.), then there will be a few unit tests, but they will not be sufficient.

## Verantwortlichkeiten

In chapter [ABAP Unit](#abap_unit_advanced) we tried to make clear the necessity and advantages of unit tests. You have to work out in what form and to what extent you will use this in your company and in your team. For this reason, there should be a responsible person who sets the course and drives things forward in the development department as well as at management level.

## In the beginning there was the concept

An important point in new developments is that a good technical concept is created. Unit tests should be taken into account in this concept. Test-driven design may be an option for developing the application. But it is also important for this that a sensitive concept is in place. Experienced people can already tell from a concept whether unit tests will be possible or not. 

## Einfach anfangen

When we encourage you to use unit testing, we recognize that this is easier said than done. If there is little experience with this technology, then this must be collected by the development team. Only if you know what prerequisites are necessary can you convince management to take the necessary measures.

But: you have to start! It's easiest with methods where you think: "It's so simple, I don't need a unit test for it!" But these are precisely the methods that make it easy to get started. Make sure that no data selections are made or user queries are made in the dialog. Maybe do the first unit test with colleagues and share your experiences.

Automated tests with the help of ABAP Unit are a very broad field. There are countless methods, techniques and areas of application. That's why we don't want to give any further recommendations or a "roadmap" at this point as to how things should proceed after your first steps. If you deal with ABAP Unit, you will get to know the weak points and the potentials. You will find a way for yourself and your team. Don't be discouraged after initial failed attempts, just keep at it. In this guide we provide you with a document that you can use to find help in many areas of automated testing. However, there is never a one-size-fits-all solution. Experience is the surest way to improve the quality of your software.

## Management

Creating and managing unit tests requires additional time. However, this is made up for by higher software quality and thus fewer user tests or even production downtimes. Developers need significantly more time to create the unit tests - especially in the early days. This must be wanted by management and must be supported. Define what you expect from management, but also what management will get in return. Find an area, application or team that is gaining experience with automated testing. Set goals for what you want to achieve within a certain period of time.

## Weiterbildung

Especially with unit tests, it is important that you continue your education and gain more and more experience. The learning curve is very steep, but after that there are an incredible number of options, variations and techniques. Attend workshops, read books and, above all, exchange ideas as a team. 

## Code - Test - Repeat

Unit tests are an important part of software development. It is important to get to grips with it and get to know this technology. Most importantly, make unit tests an indispensable part of your work. Unit tests must be maintained, documented and further developed. Don't let unit tests be forgotten.

## Fazit

As a conclusion to unit testing, we would like to close with the quote from Captain Kirk:
"The prejudices you have against each other disappear when you get to know each other."
