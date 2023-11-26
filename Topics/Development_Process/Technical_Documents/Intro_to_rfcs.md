# **Introduction to RFCs**

The following is an introductory overview of RFCs based on the following 2 articles by Juan Pablo Buriticá:

1. ["A thorough team guide to RFCs"](https://leaddev.com/technical-decision-making/thorough-team-guide-rfcs)
2. ["6 Lessons I learned while implementing technical RFCs as a decision making tool"](https://buriti.ca/6-lessons-i-learned-while-implementing-technical-rfcs-as-a-management-tool-34687dbf46cb)

## **What are RFCs?**

- RFC stands for Request for Comment
- It is a document that acts as a technical proposal for a design, approach or change
- It can outline things like architecture changes, dependencies, assumptions, alternative considerations, etc.
- RFCs are meant to facilitate technical decision-making and increase visibility and collaboration within an organization
- RFCs are usually authored by a few people and then circulated around to receive feedback (hence the name “request for comments”)
- An RFC can be understood as “Here is the direction we want to go, are we missing anything?”
- There are 4 general phases in an RFC life cycle
  - Proposal stage: the RFC is drafted
  - Commenting stage: feedback and discussion ensue
  - Decision stage: ideally, the reviewers and the author align on the path forward
  - Archive stage: the RFC is archived for future reference

## **Why are RFCs useful?**

- Mitigates the risk of the decision made
  - RFCs act as a kind of code review but at the planning stage
  - Problems or considerations can be surfaced before resources have been spent
- Facilitates better technical decisions and collaboration
  - Building software is a social exercise
  - RFCs facilitates communication and decision-making between groups
- Allows for individual contribution and responsibility on all levels
  - When done right, individuals of all levels in the organization are empowered and encouraged to make impactful decisions while seeking input from others
- Creates documentation for future context
  - An archive of past RFCs act as a record of previous discussions and decisions
- Is an asynchronous process
  - Multiple RFCs can run in parallel
  - Increases the flexibility of collaborative discussions

## **When to RFC?**

If it crosses your mind that an RFC might be required to make a change or implement a design, it probably is a good idea to make one.

Additionally, an RFC is generally a good idea when:

- You are building something from scratch (new endpoint, component, system, library, application, etc.).
- You will impact more than one system or other team members.
- You would like to define a contract of interface between clients or systems.
- You are adding a new dependency.
- You are adding or replacing languages or tools to the stack.
- You are in doubt of whether to write one.

## **How to RFC?**

RFCs are a guideline, not a rigid methodology. They are usually tailored to the specific needs of teams and organizations, so multiple variations exist both in the actual document and the surrounding process.

### **Adopting RFCs in a team**

Some considerations when adopting RFCs in a team:

- Success using RFCs isn’t guaranteed – when adopting it for the first time in a team, think of it initially as a collective experiment and reflect on whether:
  - Has using RFCs led to better decisions?
  - Is your team better informed and making decisions faster?
  - Are different groups equally participating in comments?
  - Can the process be lighter while achieving similar outcomes?
- It is usually a good idea to define a time-limit on the commenting stage to avoid it lasting forever.
- The tool you use can vary – some options include collaborative docs (ex. Google Docs, Microsoft Word, etc.), markdown doc in a git repo, a slide presentation, etc.

### **Getting started: RFC templates**

[This article](https://blog.pragmaticengineer.com/rfcs-and-design-docs/) contains templates from a comprehensive list of companies including Google, Uber, SoundCloud, and more.

Additionally, here is a basic template (credit: ["A thorough team guide to RFCs" by Juan Pablo Buriticá](https://leaddev.com/technical-decision-making/thorough-team-guide-rfcs)) in the following formats:

- [Google Doc](https://docs.google.com/document/d/1EM5ORZ8sO-g678jNc2nHMAkGjX5-6DuB6EkhjsNcOXo/edit#)
- [Dropbox paper](https://paper.dropbox.com/doc/RFC-Template-Title--BJJD6B25kkYC_zRXc2q5BxB0Ag-dYS7Oe0SKA0wjqzvuaxsO)
- [Notion](https://www.notion.so/buritica/RFC-Template-Title-8df1bd0d24b0440486fe133eecdf4a5e)
- [Markdown](https://github.com/buritica/mgt/blob/master/rfc_template.md)

These are the main sections in the above template:

1. Title
2. Authors
3. Executive summary
4. Motivation
5. Proposed implementation
6. Metrics and dashboard
7. Drawbacks
8. Alternatives
9. Potential impacts and dependencies
10. Unresolved questions
11. Conclusion

## **Conclusion**

- RFCs can be an effective tool to enhance collaboration, decision-making and better software
- However, if adopted in the wrong environment or not tailored properly to a team, it can decrease productivity and add unnecessarily to people’s workload
- To read more about common pitfalls and the best way to utilize RFCs, the two articles linked at the top of this page are great sources.
