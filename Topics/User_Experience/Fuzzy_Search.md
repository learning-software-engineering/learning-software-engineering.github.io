# Fuzzy Search

## Introduction
Fuzzy search is a type of search algorithm that uses **approximate string matching** to retrieve results relevant to the user's query. Rather than selecting only results whose string content exactly matches the search term, a fuzzy search includes all results that are reasonably close according to some distance metric.

As an example, suppose a user is on a social networking app and looking to add a friend named `Bryan`, but mistakenly remembers their name as `Brian`. With fuzzy search, profiles of people named `Brian` or `Bryan` would both be retrieved (among other similar names, like `Ryan`), while a more naive exact-match algorithm would only return those named `Brian`, leaving the user unable to find their friend.

Any implementation of fuzzy search is only as good as the underlying distance metric used by the algorithm to estimate the degree of closeness between two strings and thereby select results. Below, we will explore one of the most commonly used distance metrics for this task: **Levenshtein distance**.

## Motivation: How does this affect UX?
For applications that require the user to perform a lot of searching (e.g. social networks, data analysis tools, library catalogues, e-Commerce platforms), the usability of the search bar can significantly impact the overall user experience. Using the [7 Principles of Universal Design](https://universaldesign.ie/what-is-universal-design/the-7-principles) as a guiding framework, we can see that fuzzy search improves on exact-match search in the following ways:
- [3: Simple and Intuitive Use](https://universaldesign.ie/what-is-universal-design/the-7-principles/#p3)
  - Requiring the user to know the exact string of their target result - including spelling and possible punctuation - is needlessly complex and may even be unintuitive given the prevalence of fuzzy matching in search engines and other similar tools. It may also impact equitable use, as exact-match searching cannot easily accommodate users with lower literacy and language skills.
- [5: Tolerance for Error](https://universaldesign.ie/what-is-universal-design/the-7-principles/#p5)
  - Typos are inevitable! This is true both when users are querying some collection of data, and also when they are adding new entries for others to search (e.g. a seller mistakenly listing a new `pencil caes` on Amazon). The more accommodating result selection afforded by fuzzy search reduces the likelihood that users are unable to find their desired result and draw incorrect conclusions from it.
- [6: Low Physical Effort](https://universaldesign.ie/what-is-universal-design/the-7-principles/#p6)
  - For users that may be hazy on what they are searching for, an exact-match algorithm will likely require multiple, repetitive searches from them to find their target result. This can not only lead to fatigue while using the application, but also exacerbate accessibility issues for users who cannot input text as comfortably.
 
Given that the majority of applications have some use case for a search bar, being able to implement a user-friendly search experience can be quite essential in any software development project.
 
## Implementation: Levenshtein distance
In this section, we 

## Limitations
- While fuzzy search is generally more convenient for larger queries, precision may be more important for items whose string content is less easy to mistake. For instance, if a search bar requires the user to input some country's 2-letter code ([see all codes here](https://countrycode.org/)), a user searching for `FR` (France) may find it inconvenient to have to scroll through results for `FJ` (Fiji) and `FI` (Finland) as well, despite those codes being reasonably close typographically. As always, striking the right balance between tolerance and precision is important for a friendly user experience.
- Fuzzy searching matches only on syntax (the structure of a string) rather than semantics (the meaning of a string). As a result, a fuzzy search algorithm will consider `large bike` and `big bicycle` to be distant based on their spelling, despite them being essentially synonymous in meaning. If this is a concern, a more advanced semantic search algorithm may be required.
