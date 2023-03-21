## Resources for Product Management

## User Stories

### Introduction

A user story is an informal description of a new feature or task in a software project. The purpose of a user story is to gauge how the particular feature will provide value from the perspective of the user. These stories generally exist within a larger set, and ultimately allow teams to organize their workflow in a user-centric manner.

User stories all follow a general structure and are accompanied by their associated "Acceptance Criteria" and some additional details. Each section retains the customer-focused philosophy of the user story and consists of a few non-technical descriptive sentences. By combining these sections, user stories are able to effectively scope the entirety of their task.

### Story Structure

The majority of user stories are written to follow a general outline or pattern. The most commonly used format is the [Connextra Template](https://www.mountaingoatsoftware.com/agile/user-stories), as outlined below:
```
As a <type of user>, I want <some goal>, so that <some reason>
```
There are many other popular formats that are derivations of the one above. However, other non-standard formats can also be used, such as the W5 example below:
```
As <who> <when> <where>, I want <what> because <why>
```
Each format has its own advantages and disadvantages. Teams will generally use the format that fits their goals best and delivers the most value.

### Acceptance Criteria

Acceptance criteria refers to a set of requirements that must be accomplished for a user story to be completed and closed. The purpose of acceptance criteria is to fully scope user stories. This is important so that developers exactly what they need to output, and so that all stakeholders are satisfied.

Like with the story itself, there are various ways to commonly organize acceptance criteria. The most common organizational strategy is the "Given/When/Then" method. This works similarly to the user story outlines, and can be utilized as follows:
```
Given <some condition>, when <some action is carried out>, the <a set of observable outcomes should occur>
```

The "Verifications List" methodology is another commonly used approach for organizing acceptance criteria. This includes a list of concise and testable criteria for ensuring that everything outlined in the user story has been properly implemented. These criteria can take the form of "yes/no" or "pass/fail", and must all be successful for the story to be considered as complete.

Beyond the conditions that are explicitly outlined in the acceptance criteria, there is an additional layer of rules that must be met before a story can be completed. These conditions are generally referred to as the "Definition of Done", and are created and agreed upon by an entire team before being used. This acts as a quality control for a teams entire codebase and ensures that developers maintain their proper implementation practices at all times.

### Story Points

Story points are a numerical estimation of the amount of effort that is required to complete a user story. Teams will generally vote and discuss the given task so that they can align themselves and agree on a score. This system works so that the team can quantify the task at hand and appropriately assign it to one or multiple developers. 

When deciding the necessary points to allocate to a story, the following 3 factors are most commonly taken into consideration:

- Complexity: The overall difficulty of the task
- Risk: The margin for possible error or hidden tasks arising in the future
- Repetition: The team's past experience with this line of work

It is not absolutely necessary for teams to follow these exact considerations. These are only common examples that have proven to be effective across various organizations.

### User Story Template

By combining all of the sections above, we can create the following user story template:

---

**Title:** Example User Story

**Assignee:** Name(s)

**Points:** (Numerical Value)

**User Story:** As a \<type of user\>, I want \<some goal\>, so that \<some reason\>

**Acceptance Criteria:** Given \<some condition\>, when \<some action is carried out\>, the \<a set of observable outcomes should occur\>

---