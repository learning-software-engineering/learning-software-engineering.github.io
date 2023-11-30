# Ethics in Software Engineering

## Table of Contents
1. [Introduction](#introduction)
2. [Why Should I Care?](#why-should-i-care?)
3. [PIPEDA](#pipeda)
4. [Case Studies](#case-studies)
5. [Software Engineering Code of Ethics](#software-engineering-code-of-ethics)
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

In general, when designing software that collects user data, you must ensure that you only collect data that users consent to being collected, and only use it for the reasons that they consented to. Full transparency is also required, as users have a right to know which data you are storing if it pertains to them.

## Case Studies
When evaluating the ethical quality of a service, we can look at three main factors: privacy, consent and security. 

### Facebook and Cambridge Analytica
**Violation of Privacy**

Leading social media platform Facebook allowed third-party developers to access its API, enabling them to collect Facebook users' data to fuel the functionalities of their own applications. In 2014, a researcher from Cambridge University created an app that used this API to collect such information not only from its users but also from their friends. This data included personal information like psychological profiles. 

Cambridge Analytica, a political consulting firm, gained access to the data used by this app, containing personal psychological information about 87 million users without their knowledge. This data was used for targeted political advertising during the 2016 US federal elections.

Although the infringement was made by Cambridge Analytica, it could have been avoided through better, more ethical design on Facebook's part. If they had stricter rules regarding how this API can be used, the issue could have been mitigated, as Cambridge Analytica would have been forced to get users' consent prior to utilizing their information.

### Sephora
**Violation of Consent**

The problem with the software design of multi-million dollar company Sephora was a concept commonly referred to in conversations surrounding ethics: "opt in vs. opt out". What this means is that, generally, if you offer a user a product or service, or wish to gather their consent for data collection, for example, they must be opted out by default, not opted in. That is, if your website has a check box which the user needs to have selected in order for you to use their data, that check box must be unselected by default.

In 2022, Sephora was found guilty of doing the opposite, opting users in to having their data sold by default. This resulted in a $1.2 million fine as an enforcement of the California Consumer Privacy Act.

### ChatGPT
**Violation of Security**

On March 24th, 2023, it was revealed that Open AI's system had an easily exploitable vulnerability, allowing users to, through an open-source library called Redis, see the chat histories of other users. This same vulnerability was also responsible for allowing users to view payment information of other users, as well as their full names, email addresses and payment addresses. 

Open AI was thankfully able to detect this issue and take ChatGPT offline before it could impact any more than 1% of their users. However, with a large user base, 1% still implies many affected people, and this raises concerns for future problems as their user base continues to grow.

### Amazon
**Biased Algorithm**

Another case of unethical computing comes from a hiring algorithm scrapped by Amazon in 2015. Initially created to remove bias that recruiters may have towards candidates, Amazon's algorithm was unfortunatley proved to be just as biased if not more so. Specifically, the algorithm was revealed to have a negative bias towards female candidates, flagging words like "women's" when reveiwing resumes. The reason this happened was because Amazon used a biased dataset to train the algorithm - it was trained using a set of the past 10 years' worth of Amazon resumes, most of the approved ones being from male candidates. Hence, the algorithm "learned" that the ideal Amazon candidate must be male. 

Amazon should have hand-picked the data they trained the algorithm with. Although this would take more time, providing the algorithm with unbiased data, in which the only differences between acceptable and unacceptable resumes are in their merit, would have reduced the likelihood of such discimination occurring. 

## Software Engineering Code of Ethics
Now that you have some insights into what you shouldn't do, the Software Enginnering Code of Ethics details how you should act when making decisions regarding the ethical designs of your work.

The 8 principles of this code of ethics are as follows:
* Public: Software engineers shall act consistently with the public interest.
* Client and employer: Software engineers shall act in a manner that is in the best interests of their client and employer consistent with the public interest.
* Product: Software engineers shall ensure that their products and related modifications meet the highest professional standards possible.
* Judgment: Software engineers shall maintain integrity and independence in their professional judgment.
* Management: Software engineering managers and leaders shall subscribe to and promote an ethical approach to the management of software development and maintenance.
* Profession: Software engineers shall advance the integrity and reputation of the profession consistent with the public interest.
* Colleagues: Software engineers shall be fair to and supportive of their colleagues.
* Self: Software engineers shall participate in lifelong learning regarding the practice of their profession and shall promote an ethical approach to the practice of the profession.

These principles can be applied in many ways. Below are some examples of questions you should ask yourself when designing software.

### How can my software be misused?
As noted in the Facebook / Cambridge Analytica case, an engineer should always think about the loopholes in their design, and how their work could be abused or exploited. 

### How can I improve?
Take accountability for your work. Seek out criticism for your work and implement it - it is far better to take a long time ideating than to publish an application which ends up committing ethical offenses.

### Does my design ensure informed consent on my users' part?
As seen in the Sephora case, it is not enough to have accidental agreement from your user; they must actively consent to you using their data, and you must do everything in your power to ensure that they understand what they are consenting to.

### What biases may be present in this system?
As seen in the Amazon case study, it is a common misconception that an algorithm is incapable of holding bias. An AI algorithm can only generate information based on what it is trained with, and so an engineer must ensure that they train the algorithm with care, ensuring that no biases are introduced in the process. This doesn't only apply to AI algorithms, however - all software designs must take into account concepts such as accessibility and globalability to ensure that they can be used by all users. 

As some very common examples, the colour of the text you use on a web page should contrast greatly with the background colour, in order to ensure that those with colour-blindness or who are otherwise visually impaired can still easily read it. Additionally, when working on an enterprise project, ensuring that your product is being accurately translated into other languages when being used by users around the world is also crucial.

## Works Cited
“Chatgpt Confirms Data Breach, Raising Security Concerns.” Security Intelligence, 21 Nov. 2023, securityintelligence.com/articles/chatgpt-confirms-data-breach/. 

Cook, Brier. “Everything to Know about Software Engineering Ethics.” Fellow.App, 3 Feb. 2023, fellow.app/blog/engineering/engineering-everything-you-need-to-know-about-software-engineering-ethics/#1. 

Daniels, Jodi. “CCPA Enforcement Action: A Case Study at the Intersection of Privacy and Marketing.” CCPA Enforcement Action: A Case Study at the Intersection of Privacy and Marketing, International Association of Privacy Professionals, 9 Sept. 2022, iapp.org/news/a/ccpa-enforcement-action-a-case-study-at-the-intersection-of-privacy-and-marketing/. 

Dastin, Jeffrey. “Insight - Amazon Scraps Secret AI Recruiting Tool That Showed Bias against Women.” Reuters, Thomson Reuters, 11 Oct. 2018, www.reuters.com/article/us-amazon-com-jobs-automation-insight/amazon-scraps-secret-ai-recruiting-tool-that-showed-bias-against-women-idUSKCN1MK08G/. 

“Ethics in Software Engineering: A Key Component of Professional Practice.” Continuing Education for Professional Engineers PDHPRO, pdh-
pro.com/pe-resources/ethics-in-software-engineering/#:~:text=Ethics%20in%20software%20engineering%20is,the%20impact%20of%20unethical%20practices. 

“What If My Company/Organisation Fails to Comply with the Data Protection Rules?” European Commission, commission.europa.eu/law/law-topic/data-protection/reform/rules-business-and-organisations/enforcement-and-sanctions/sanctions/what-if-my-companyorganisation-fails-comply-data-protection-rules_en#:~:text=likely%20infringement%20%E2%80%93%20a%20warning%20may,business’s%20total%20annual%20worldwide%20turnover.
