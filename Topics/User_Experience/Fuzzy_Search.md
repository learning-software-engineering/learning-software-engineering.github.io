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
 
Given that the majority of applications have some use case for a search bar, **being able to implement a user-friendly search experience is essential in many software development projects**. Careful consideration should be given to any search tool you implement regardless of whether you choose fuzzy search or a more sophisticated algorithm. Moreover, the core idea behind fuzzy search - approximate string matching - is highly useful in designing many non-search tools a developer may be interested in, like autocorrect or data processors.
 
## Implementation: Levenshtein distance
In this section, we discuss the [Levenshtein distance](https://en.wikipedia.org/wiki/Levenshtein_distance) and how to use it in implementing fuzzy search.

Levenshtein is a popular distance metric to compare the similarity between a query string and a target string. Intuitively, it counts the fewest number of times a character in the query must be deleted, inserted, or replaced to reach the target. For instance, if the query is `Brian`, its Levenshtein distance to `Bryan` is 1 as it only needs to replace `i` with `y` to reach the target. Notice that this can also be done in two operations by deleting `i` and inserting `y`, but this is suboptimal. Targets with a lower Levenshtein score are considered closer to the query.

The algorithm for computing Levenshtein distance is not overly complicated and several possible implementations can be found in [this GeeksforGeeks article](https://www.geeksforgeeks.org/introduction-to-levenshtein-distance/). Coding it oneself offers the advantage of customizing the algorithm according to your specific problem domain. For instance, if you know that users are significantly more likely to mistype the wrong character rather than insert/delete a character entirely, you can increase the weight of the latter operations by making them count as multiple "replace" operations. This will naturally shorten the Levenshtein distances of candidate strings that are the same length as the query.

That being said, you can also find out-of-the-box solutions online that are likely better optimized. For applications built in JavaScript, the [js-levenshtein](https://www.npmjs.com/package/js-levenshtein) library is quite efficient and easy to use:
- Install it by running `npm install --save js-levenshtein`.
- In your code, import the module using `import { levenshtein } from 'js-levenshtein';` or `const levenshtein = require('js-levenshtein');`
- Compute Levenshtein distance using `levenshtein('queryString', 'targetString')`

The following code snippet sorts a list of names by their Levenshtein proximity to `Brian`:
```
import { levenshtein } from 'js-levenshtein';

const query = 'Brian';  // Define the query string
const names = ['Bryan', 'Brian', 'Bob', 'Bryant', 'HarrisonFord'];  // Define the list of strings to search from
names.sort((a, b) => levenshtein(query, a) - levenshtein(query, b));  // Sort the list based on Levenshtein distance

// Result: ['Brian', 'Bryan', 'Bryant', 'Bob', 'HarrisonFord'] with distances [0, 1, 2, 4, 9] respectively
```

The above strategy can be used, as an example, to take in an input query string from a search bar component and sort the list of results to display before they are rendered back to the user. Additionally, instead of just sorting by distance, you can devise a threshold so that only results below a certain distance are included, to prevent extremely distant results like `HarrisonFord` from appearing at all.

Libraries for Levenshtein distance in other languages can also be found, such as [python-Levenshtein](https://pypi.org/project/python-Levenshtein/) for Python.

And with that, you have implemented fuzzy search! If you're curious about other possible distance metrics, see below:
- [Damerau-Levenshtein](https://www.geeksforgeeks.org/damerau-levenshtein-distance/): Same as Levenshtein, but allows for the transposition of characters as an operation.
- [Soundex](https://www.geeksforgeeks.org/implement-phonetic-search-in-python-with-soundex-algorithm/): Uses the phonetic sounds of strings to determine their similarity.

## Limitations
- While fuzzy search is generally more convenient for larger queries, precision may be more important for items whose string content is less easy to mistake. For instance, if a search bar requires the user to input some country's 2-letter code ([see all codes here](https://countrycode.org/)), a user searching for `FR` (France) may find it inconvenient to have to scroll through results for `FJ` (Fiji) and `FI` (Finland) as well, despite those codes being reasonably close typographically (Levenshtein distances of 1). As always, striking the right balance between tolerance and precision is important for a friendly user experience.
- Fuzzy searching matches only on syntax (the structure of a string) rather than semantics (the meaning of a string). As a result, a fuzzy search algorithm will consider `large bike` and `big bicycle` to be distant based on their spelling (Levenshtein distance of 8), despite them being essentially synonymous in meaning. Worse, unrelated strings like `large bike` and `loud bird` will be considered closer (Levenshtein distance of 6), which can be misleading. If this is a concern, a more advanced semantic search algorithm may be required.
