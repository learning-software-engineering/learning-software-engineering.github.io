# Ethics in Software Engineering

## Table of Contents
1. [Introduction](#introduction)
2. [Why Should I Care?](#why-should-i-care?)
3. [PIPEDA](#pipeda)
4. [Case Studies](#case-studies)
5. [What Can I Do?](#what-can-i-do?)
6. [Works Cited](#works-cited)

## Introduction
In the age of big data collection, it has become a continuously greater challenge to maintain ethical practices when designing software. It seems as though every company which collects user data or has any form of software which users interact with has made mistakes in this field, sometimes with catastophic consequences. Hence, it is vital for any software enginner to be mindful and educated on the topic of ethics in computing, and how they can apply it to their work.

## Why Should I Care?
### Moral Incentives
An intuitive reason for taking into account ethics when designing software is general morality. Software that is designed without ethics and privacy in mind, even without the developer intending any harm, can have devastating effects for its users, as will be explored in the [Case Studies](#case-studies) section.

### Professionalism
As a software engineer, you are personally and professionally responsible for maintaining a high level of quality in your work. The same applies to the level of transparency and privacy that you provide for your users. As you work with clients, you accept both implicit and explicit terms that include maintining confidentiality and privacy in order to protect their personally identifiable information (PII) and intellectual property.

### Legal Consequences
There are great legal implications to breaking ethical laws, and being unaware of them is seldom a reasonable justification. Violating the privacy of a user or otherwise handling their information irresponsibly can lead to lawsuits from that user, or from a client company. Poor practices can also result in detrimental fines and a ruined record; in the European Union, for example, the General Data Protection Regulation (GDPR) is strongly enforced, and non-compliance can result in a fine of millions of dollars. The Canadian equivalent to the GDPR is PIPEDA.

## PIPEDA
Canada's Personal Information Protection and Electronic Documents Act (PIPEDA) is a set of laws regarding data collection and use in the context of businesses. To summarize, here is what it requires:

* Consent: Organizations must obtain consent when collecting, using, or disclosing personal information.
* Purpose Limitation: Organizations must collect personal information for a specific purpose and cannot use it for other reasons without consent.
* Limited Collection: Organizations must only collect information necessary for the identified purpose.
* Accuracy: Organizations must ensure that the collected information is accurate, complete and up-to-date.
* Safeguards: Organizations must implement security measures to protect personal information against unauthorized access, disclosure, or misuse.
* Openness: Organizations must be transparent about their policies and practices related to the handling of personal information.
* Individual Access: Individuals have the right to access their own personal information held by an organization and request corrections if necessary.
* Challenging Compliance: Individuals can challenge an organization's compliance with PIPEDA and seek recourse.

In general, when designing sofwtare that collects user data, you must ensure that you only collect data that users consent to being collected, and only use it for the reasons that they consented to. Full transparency is also required, as users have a right to know which data you are storing if it pertains to them.

## Case Studies
When evaluating the ethical quality of a service, we can typically look at three main factors: privacy, security and consent. 

## Facebook and Cambridge Analytica


## Sephora
Multi-million dollar company Sephora is an example of a company which has faced legal consequences due to poor ethical practices related to software design. The problem with their software design is a concept commonly referred to in conversations surrounding ethics - "opt in vs. opt out". What this means is that, generally, if you offer a user a product or service, or wish to gather their consent for data collection, for example, they must be opted out by default, not opted in. That is, if your website has a check box which the user needs to have selected in order for you to use their data, that check box must be unselected by default.

In 2022, Sephora was found guilty of doing the opposite, opting users in to having their data sold by default. This resulted in a $1.2 million fine as an enforcement of the California Consumer Privacy Act.

## ChatGPT
On March 24th, 2023, it was revealed that Open AI's system had an easily exploitable vulnerability, allowing users to, through an open-source library called Redis, see the chat histories of other users. This same vulnerability was also responsible for allowing users to view payment information of other users, as well as their full names, email addresses and payment addresses. 

Open AI was thankfully able to detect this issue and take ChatGPT offline before it could impact any more than 1% of their users. However, with a large user base, 1% still implies many affected people, and this raises concerns for future problems as their user base only grows.

## Works Cited
“Ethics in Software Engineering: A Key Component of Professional Practice.” Continuing Education for Professional Engineers PDHPRO, pdh-
pro.com/pe-resources/ethics-in-software-engineering/#:~:text=Ethics%20in%20software%20engineering%20is,the%20impact%20of%20unethical%20practices. 

“What If My Company/Organisation Fails to Comply with the Data Protection Rules?” European Commission, commission.europa.eu/law/law-topic/data-protection/reform/rules-business-and-organisations/enforcement-and-sanctions/sanctions/what-if-my-companyorganisation-fails-comply-data-protection-rules_en#:~:text=likely%20infringement%20%E2%80%93%20a%20warning%20may,business’s%20total%20annual%20worldwide%20turnover.

Daniels, Jodi. “CCPA Enforcement Action: A Case Study at the Intersection of Privacy and Marketing.” CCPA Enforcement Action: A Case Study at the Intersection of Privacy and Marketing, International Association of Privacy Professionals, 9 Sept. 2022, iapp.org/news/a/ccpa-enforcement-action-a-case-study-at-the-intersection-of-privacy-and-marketing/. 

“Chatgpt Confirms Data Breach, Raising Security Concerns.” Security Intelligence, 21 Nov. 2023, securityintelligence.com/articles/chatgpt-confirms-data-breach/. 
