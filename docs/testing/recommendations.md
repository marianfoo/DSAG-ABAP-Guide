---
layout: page
title: Recommendations
permalink: /testing/recommendations/
parent: Software test with ABAP unit
nav_order: 99
---


{: .no_toc}
# Recommendations

1. TOC
{:toc}

Below, we would like to try to distill this wealth of information into a set of recommendations that will help you and your team get off to a quick and sustainable start.

## Consensus

Unit Tests and thus code quality—are not an end in themselves, but an essential component of your production-ready software products. That is why, in our view, there is no excuse for not using unit tests.

There are two different perspectives that have to fit together:
1. Developers must want to create unit tests
2. Management must support the use of unit tests

If developers are required to write unit tests but refuse to do so for various reasons,
there will be no unit tests—or they will be useless.
If management does not support the developers and does not provide the necessary resources (training, time, etc.),
there will be a few unit tests, but they will not be sufficient.

## Responsibilities

The [ABAP Unit chapters]({{ site.baseurl }}/testing/abap_unit_advanced/) explain the need for and benefits of unit tests. Each company and team must decide how and to what extent to use them. A designated owner should therefore set the direction and drive adoption within both development and management.

## It All Started with the Concept

An important consideration in new development projects is the creation of a sound
technical design. This design should incorporate unit tests. Test-driven design may
be one approach to developing the application. However, even in this case, it is essential
to have a sound design in place. Experienced professionals can often tell from the
design alone whether unit tests will be feasible or not.

## Just Get Started

When we recommend that you use unit tests, we realize that this is easier said than
done. If there is little experience with this technique, the development team will need
to gain that experience. Only by understanding what is required can you convince
management to take the necessary steps.

But: You have to start somewhere! The easiest place to begin is with methods where
you think, “This is so simple—I don’t need a unit test for this!” Yet these are precisely
the methods that make getting started easy. Make sure no data selections are made
and no user queries are performed in dialog boxes. Consider conducting your first unit
test together with colleagues and sharing your experiences.

Automated testing with ABAP Unit is a broad field with countless methods, techniques, and use cases. We therefore do not provide a detailed roadmap for what to do after your first steps. As you work with ABAP Unit, you will come to understand its strengths and limitations and find an approach that works for your team. Do not let initial setbacks discourage you. This guide offers support across many areas of automated testing, but there is no one-size-fits-all solution. Experience is the surest way to improve the quality of your software.

## Management

Creating and managing unit tests requires additional time, but higher software quality reduces later testing effort and production outages. Developers need more time for unit tests, especially at the beginning, so management must commit to and support the practice. Define both what you expect from management and what management receives in return. Select a department, application, or team to gain experience with automated testing, and set goals for a specific timeframe.

## Continuous Learning

With unit testing, continuous learning and practical experience are especially important. The learning curve is steep, but proficiency opens up a wide range of techniques and possibilities. Attend workshops, read books, and, above all, share your insights with your team.

## Code – Test – Repeat

Unit tests are an important part of software development. Learn the techniques and make unit testing an integral part of your work. Tests must be maintained, documented, and developed further; do not let them fall by the wayside.

## Conclusion

To wrap up our discussion of unit tests, we would like to conclude with a quote from
Captain Kirk: “The prejudices we hold against one another disappear once we get to
know each other.”
