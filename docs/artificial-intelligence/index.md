---
layout: page
title: Artificial intelligence
permalink: /artificial-intelligence/
nav_order: 14
---

{: .no_toc}
# Generative artificial intelligence (genAI)

1. TOC
{:toc}

## AI in development - A topic of great importance and dynamics

The topic of generative AI (hereinafter referred to as AI for short) is currently *the* central topic that can no longer be avoided in SAP development. Products/solutions such as ChatGPT, Microsoft Copilot, Google GEMINI and of course SAP itself with Joule are discussed everywhere and will (in the future) find their practical application in numerous solutions. These solutions are also used in software development; there are even corresponding AI support options in ABAP development. 

Development in this area is happening rapidly and newer features and options are becoming available in short cycles - the results are getting better and better. It is very difficult to make a concrete forecast as to what will happen over the next (not years but) weeks. 

A prominent example of this is the recently announced integration option for MCP servers (including for the SAP documentation and ABAP context), the potential of which seems high, but is still rather difficult to grasp. Vibe Coding was also surprisingly well represented at SAP TechEd 2025 - another glimpse into a possible future (also for ABAP?).

Despite all the uncertainties, in this chapter we want to try to give you (as of today, SAP TechEd 2025) assistance in making decisions regarding the use/application of AI in software development with SAP. We therefore deliberately do not present all available software solutions or go into detail. As a guide, we want to show you general information and possible application scenarios.  

AI provides tools that help develop better software faster. Even though AI is developing rapidly, AI will not be able to replace human developers. As a basis for good development, good knowledge of modern software development is essential, even with AI. AI can support development in the various phases of software development. We will give you a few examples in which the use of AI brings efficiency gains.


## Full responsibility for the AI ​​result, but also the area of ​​application for the developer

First of all, there are a few fundamental aspects that are very important to us as authors and that we would like to point out. 

Based on current knowledge, we as authors are firmly convinced that AI will not replace human developers. As a basis for good development, in-depth knowledge of modern software development is essential, even with AI. AI can *assist* in development in the various phases of software development. To this end, in later chapters we will show concrete application scenarios with examples in which the use of AI can bring about efficiency gains.

Another very important aspect lies in the specific use of potential AI support for the developer. The craft of programming and software development is complex. Even with years (decades) of experience, hardly a day goes by without us learning something new. Regardless of whether you see your focus as development, architecture or design - the approach and implementation with individual tools to solve a problem is very individual. In other words: Every (ABAP) developer has their own preferences and develops/analyses in a personal way based on their own experience. 

Why is this important? It will not work to roll out AI support with the motivation that everyone in the company *must* use it in order to achieve an increase in efficiency of xy% (and in the worst case, to plan for it). The majority of developers will not allow this to be dictated to them (and rightly so, in our opinion). So what can work? It is important to create awareness among colleagues about the new possibilities - to point out useful use cases that can potentially help the developer. AI will only become truly relevant in a developer's everyday work if the developer is convinced of its benefits and personally recognizes the added value.  

Closely related to this point is the last aspect that we would like to point out in advance: responsibility. If the developer uses AI to generate something (e.g. code, unit tests, RAP objects, etc.), responsibility for the generated artifact remains with the developer. Potential errors, underperforming requests, security gaps, etc. ultimately fall back on the developer - "that was (AI) generated" doesn't absolve anyone of guilt. From this perspective alone, we would like to point out again that, in our view, every colleague should (be allowed to) decide individually whether and to what extent AI support should be used for their individual task.   


## Support for decision-making on the use of AI and AI tools

Before AI can be used in the area of ​​​​development, important questions must be illuminated, clarified and used for decision-making. This point varies greatly from company to company - below you will find a few potentially important questions: 

- What security requirements are placed on the AI?
  - Private Space vs. Public Space
    - Private Space: AI models and data are protected and secured against unauthorized access
    - Public Space: AI systems and data are accessible to the general public. Where is the data storage here - in the EU?

- Which models are used?
  - LLM Large Language Model
    - ML Machine Learning
    - Deep Learning
    - Neuronale Netze
    - Others, if so which ones?

- Are third-party AI products used, yes which ones?
- Which database was/is used for training?
- Is your own company data used to train the models and how is it ensured that the data “remains with the company”?
- Does the solution meet applicable regulations/legal requirements (e.g. EU AI Act, DSGVO/GDPR, ...)  
- How is the AI ​​solution classified according to the [EU criticality levels](https://www.trail-ml.com/blog/eu-ai-act-how-risk-is-classified) (Minimal/No Risk, Limited, High, Unacceptable)?
- Is it ensured that the solution does not use copyrighted data or content? How is this ensured?
- Can prompt storage be disabled? Where are the prompts stored?
- Does the company that developed/sells the solution have an “AI ethics foundation”, for example the SAP called “[KI Ethik Handbuch](https://www.sap.com/germany/products/artificial-intelligence/ai-ethics.html)”
- What is the content? How does this fit with your own corporate culture or even with your own AI ethics foundation?

In addition to these questions, the use of AI also raises issues and problem areas such as how to deal with ethical concerns about the “bias” of AI models adopted from the training data (keyword here is the so-called BIAS) or how to counter/counter them.  

An important aspect when using AI is the issue of checking results. Results produced by AI may contain algorithmic biases (“hallucinations”) and/or be incorrect. It is important that such results are verified by knowledgeable and experienced developers. This is not trivial - e.g. the result of a [Study by Purdue University, West Lafayette, USA](https://dl.acm.org/doi/pdf/10.1145/3613904.3642596) as part of the CHI 2024 conference shows that 39% of the errors in the results of an AI remained undetected because the questions were answered “politely”. We therefore recommend checking and validating the results objectively and prudently.

## SAP AI roadmaps and tools for development

{: .note }
As already mentioned, the environment and the available features in the context of AI are developing rapidly. For this reason, we would like to recommend Joule for Developers [the SAP roadmap](https://roadmaps.sap.com/board?PRODUCT=73554900100800006341&range=CURRENT-LAST) to check recent and future developments.  


### Current status (SAP TechEd 2025) AI support in the SAP environment

With *SAP Joule for Developers*, SAP provides a central offering for the entire SAP build portfolio. 

![SAP Joule for Developers add-on](./img/joule_for_developers_addon.png)

Quelle SAP TechEd 2025 – AD104 – Boost your ABAP development with SAP Joule for Developers
{: .img-caption}

For ABAP, the corresponding component is officially called "SAP Joule for Developers, ABAP AI capabilities" and is natively integrated into Eclipse via ADT. From the authors' point of view, this is a fundamental advantage over alternative tools, as the context (e.g. a concrete RAP object) can be better integrated.

At SAP Joule for Developers, SAP distinguishes between three primary areas of AI support in the ABAP development environment. Below you will find a definition and explanation of the features as well as information about their availability. Please note that the issue of licensing also needs to be clarified. Check material 8019124 for customers and 8019541 for partners.

- **Accelerate**
  - The target group for this area is the ABAP developer and increasing their efficiency during their daily work. SAP supports the developer, for example, by:
    - Interact with AI via the "Joule Copilot" window
    - Generation of RAP business objects (BO's) and services
    - Generation of unit tests for ABAP classes and Core data services
    - Explanation of existing (legacy) code
    - Help with code snippets, code analysis, documentation, existing help content and code predictions (“predective code completion”)
  - Features in the Accelerate context are available on SAP BTP ABAP Environment, SAP Cloud ERP and SAP Cloud ERP private 2025 (formerly SAP S/4HANA, private Cloud). Previous releases of SAP Cloud ERP private [can consume the features side-by-side](https://community.sap.com/t5/enterprise-resource-planning-blog-posts-by-sap/abap-ai-chapter-2/ba-p/14210568). According to the current status, the features are not available on-premise and this is not planned by SAP.   

- **Transform**
  - The ABAP developer should be supported in migrating customer-owned code to ABAP Cloud and a Clean Core. Both existing code and messages from the ATC check are explained. In addition, the AI ​​offers suggestions for adapting/transferring existing coding. 
  - According to current knowledge regarding SAP Cloud ERP private, the availability of the Transform use case is analogous to the Accelerate features. 

- **Empower**
  - This main area deals with the integration of AI into applications. This means that the target group for AI is the end user. The ABAP developer has the task of implementing this into the application. SAP provides the ABAP AI SDK using “ISLM” (Intelligent scenario lifecycle management). It enables standardized access to the generative AI hub within the SAP AI Core on the SAP BTP.  
  - The Empower area is available on both SAP BTP ABAP Environment, SAP ERP Cloud (incl. private) and S/4HANA On-Premise via downport until release 2021 (for more information, see SAP Note 3513374).

You can find an overview of the current roadmap as of today (SAP TechEd 2025) on the following slide: 
![Roadmap](./img/joule_for_developers_road_map.png)

Aktuelle Roadmap
{: .img-caption}


## Support with ABAP development through alternative AI tools

The use of official SAP tools such as "Joule for Developers" requires, as indicated in the previous chapter, the use of Cloud systems such as BTP or at least system operation in the private Cloud in conjunction with appropriate contracts. If you are on a different SAP system, there are potential alternatives. 

### Using GitHub Copilot

For example, in March 2025 it was announced that GitHub Copilot is available in Eclipse and therefore ABAP also supports [Introducing ABAP Support in GitHub Copilot for Eclipse](https://devblogs.microsoft.com/java/introducing-abap-support-in-github-copilot-for-eclipse/).  
You can find a good overview of this in the SAP community [Getting Started with ABAP Support in GitHub Copilot](https://community.sap.com/t5/technology-blog-posts-by-members/getting-started-with-abap-support-in-github-copilot-for-eclipse-ide/ba-p/14086717).  

However, compared to Joule's native SAP integration, the full SAP context is currently not automatically available to the AI. The context must be explicitly defined here via the Copilot chat window in ADT and is therefore particularly suitable for analyzing one or more classes of an application. The GitHub Copilot offers the following options:  

- **Code Completion**.
As of the end of 2025, this feature can be used particularly helpfully for creating comments or as a somewhat smarter code completion. In any case, the proposed code fragments must be checked intensively for meaningfulness and correctness. Here, the quality of the results depends heavily on the use of Clean code. The more understandable and readable the code is and the more explanatory line comments are, the more likely the AI ​​​​is to understand the context and the more useful the suggestions can be generated. Therefore, this function primarily increases the efficiency of very experienced developers who can immediately recognize the usefulness of suggestions and whose code has the necessary quality properties.

- **Code Explanation / Code Review**
Code artifacts listed in context can be explained by Copilot to gain a better understanding of the function. As an extension, Copilot can carry out a review of one or more code artifacts and thus take on a quality assurance task, which in turn relieves the developer's workload. The success factors here lie in good “prompt engineering” by the user. The knowledge gained can be used to identify deficits and weak points in the code, to determine its quality level and finally to derive measures for training and further education of the developers.

- **Improvement of code**
 While the review focuses on the understanding and quality level of the application or individual classes, Copilot can also be used to improve individual parts of the code. An example here is the optimization of a complex If-Else-Endif section with replacement by new statements or summary of error handling in try-catch blocks. A check of the improvement can then be carried out through prompting. In addition to the syntax check, Copilot not only provides statements about correctness but also an explanation as to why the correctness is given.

- **Other aspects**
In addition to the points mentioned, Copilot offers further support in creating unit tests or troubleshooting. In addition to chat, which does not make any changes to the code, there is also an agent mode that creates or changes code, similar to Joule. Since ongoing changes and improvements are to be expected here, we refer you to the official documentation at this point.

- **Custom Instructions**
An important function is the custom instructions. A prompt can be stored here in the Copilot settings, which contains basic definitions and instructions that are part of every prompt transmitted in the chat window. In this way, specifications for reviews, analyzes etc. can be simplified because generally applicable specifications are defined in the “Custom instruction prompt”.

Although GitHub Copilot does not have the deep integration of Joule, it is a potentially useful tool to make good developers faster and better and, most importantly, to enable quality assurance people such as lead developers to gain better insight into applications in less time. Based on this, targeted measures such as code corrections or training in the development team can be derived.

### More alternatives

We would like to mention at this point that GitHub Copilot represents *a" possible alternative to SAP Joule for Developers - other options exist and are continually being created, including Amazon Q Developer. We as authors make no claim to completeness at this point and have selected Github Copilot to show you another option in more detail.  

{: .important }
As with “Joule for Developers”, all AI results must be validated by the developer. The responsibility for accuracy lies with the user of the AI ​​tool. Therefore, on the one hand, it must be ensured that employees have been appropriately trained and sensitized. In addition, potential processes can be established to ensure that AI-generated results cannot be used unchecked (keyword “human-in-command” or “human-in-the-loop”).


## Further use cases for generative AI in software development

In addition to the described options for increasing efficiency during the implementation phase, AI can also be used in further phases of software development. Using a few examples, we would like to explain to you in which areas generative AI can already be used to support today and what benefits you can gain from it. Since there are a wide variety of tools and the above-mentioned questions in companies can lead to different solutions and providers, we do not name any specific tools here, but would like to describe the use case and give you inspiration to also use chat-based tools in development.

### AI for creating, checking and preparing customer requirements

AI is particularly suitable for text creation, checking and preparation. Good applications are based on well-defined requirements. In order to obtain good requirements, you can analyze requirements created by specialist users that exist or are to be created in a structured form using AI tools, check them for logic and consistency and, if necessary, have them prepared and structured. The power of AI can help you here, even without SAP integration, to put the basis for software development on a stable foundation.  

### AI as a tool for documentation creation

One application scenario is the supporting creation of documentation for in-house developments. Currently available chat-based tools can be used by the developer or the employee responsible for development to create the technical documentation of the application. To do this, the generative AI must be told the task (i.e. the desired result: create technical documentation), the context and purpose of the application. For the technical details, the code of the most important classes, which contains the business logic and additional information, is transferred to the chat tool. The concerns of data protection and, if necessary, an examination of the confidentiality of the application must be taken into account.

If explanatory information is already included in the development as a comment or, in the best case, as a ABAP Doc, this can be used by the generative AI for the documentation. This automated documentation creation produces better results if the Clean code principles were used when developing the application. Clean, readable and human-understandable code can also be better analyzed by artificial intelligence.

The result of the described procedure is a description of the AI-based evaluation of the information from the code. Here it quickly becomes obvious to what extent the code implements the desired logic in an explainable manner and where manual corrections and additions are necessary. 
With good prompt engineering and "iterative prompting" or fine-tuning of the created documentation, you get a good basis on which you can finally complete the documentation through manual revision. The result can then be checked by the AI, which in turn allows you to draw further conclusions about the quality of the documentation.  
The goal is not primarily to receive documentation fully automatically. Rather, this process helps to create a draft version or revise or finalize the documentation, which increases the quality and saves extensive typing. The success and efficiency factors here are the code base and its structure, experience in prompt engineering and an understanding of the application to be documented.

## AI development on the SAP BTP beyond ABAP

Finally, it should be mentioned in the AI ​​chapter that there is also a lot of movement in terms of AI development in the SAP ecosystem beyond ABAP. For example, in the context of SAP Fiori (SAPUI5) or the CAP model, SAP enables numerous functions to be seamlessly integrated using VSCode. With the official availability of ABAP in VSCode in the second half of 2026, we expect equally exciting developments in the context of AI integration for ABAP. 

Regardless of the implementation tools surrounding the established technologies, SAP with Joule Studio in the BTP brings the possibility of implementing Joule skills and bundling them into powerful tools within agents. These Joule skills in turn often use API's from the backend, which in turn can be implemented with ABAP. In this context too, ABAP will continue to accompany us, at least indirectly.  


## Zusammenfassung (KI assistiert)
AI will permanently change application development in the SAP world - it will not replace developers, but will specifically support their strengths and reduce routine work.
Anyone who uses the opportunities and possibilities of generative AI responsibly gains efficiency and quality without losing their own competence. Sound specialist knowledge, good architecture, clean design and critical thinking remain the basis of every development - even and especially in the age of AI. What is crucial is that people retain control over the result and take responsibility for it.

{: .note }
> This summary was created with the support of a generative AI - of course carefully checked, revised, finalized by the author and linguistically rounded off by the AI.