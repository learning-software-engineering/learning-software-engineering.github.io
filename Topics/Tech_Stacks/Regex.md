# Introduction to Regular Expressions (Regex)

## Table of contents
### [Introduction](#introduction)
### [Language Support](#language-support)
### [Basic Regular Expressions](#basic-regular-expressions)
### [Common Case Uses](#common-case-uses)
### [Extra Resources](#extra-resources)
### [Greedy vs. Lazy Quantifiers](#greedy-vs-lazy-quantifiers)

## Introduction
Regular expressions, also known as regex or regexp, are a sequence of characters that define pattern matching within strings. It is a powerful tool used in a variety of text and string processing tasks, such as data valdidation, data scraping, simple parsing, and more.

With regular expressions, one can: 
- Search: Look for specific patterns within strings
- Validate: Check if a string matches a pattern
- Replace: Change parts of a string that match a pattern
- Extract: Take specific parts of a string that match a pattern

Regular expressions are made up of characters (matching themselves), metacharacters (matches with groups of characters such as digits, letters, and whitespace), quantifiers (amount of times a character or group appears), and much more that allow for complex pattern matching! 

## Language Support
Many languages support the use of regex whether it is through libraries or natively. Some common languages and their supports include:
- **Python:** `re` module 
- **JavaScript:** native support through `RegExp` object
- **Java:** `java.util.regex` package
- **Ruby:** built-in support
- **PHP:** `preg` functions
- **C#:** .NET languages like C# have `System.Text.RegularExpressions`
- **Go:** `regexp` package
- **R:** `grep` and `grepl` functions
- **Shell scripting:** many Unix shells (ex. Bash) support regex for pattern matching.

## Basic Regular Expressions
### Characters
Any character will match itself, this includes alphabet letters, digits, and any symbols.
> `hi` matches on `hi`, `hi123`, `5hi`

### Digits
`\d` matches any digit character
> `hi\d` matches on `hi0`, `hi1hi`

<br />`\D` matches any non-digit character
>  `hi\D` matches on `hi`, `hia`, `hi%$d`

### Anything
`.` matches any character
> `.` matches on `a`, `abc`, `1`, `%`

<br />`\.` matches period (as period alone matches everything)
>  `hi\.` matches on `hi.`, `hi.23`

### Specific Characters
`[...]` matches specific characters within the brackets
>  `[abc]` matches on `hat`, `bowl`, `coffee`

<br />`[^...]` excludes specific characters within the brackets and hat
>  `[^abc]` matches on `hi`, `dog`, `xylophone`

### Character Ranges
`[0-9]` matches sequential numbers from 0 to 9 using the dash to indicate range
> `[2-4]` matches on `2`, `3`, `4`, `234`, `hi2`, `h3llo`

<br />`[a-z]` matches sequential letters from a to z using the dash to indicate range and is also case-sensitive
> `[A-C]` matches on `hAt`, `Bowl`, `Coffee`

<br />`\w` matches any alphanumeric character
> `hi\w` matches on `hiA`, `hiya`, `hi123`

<br />`\W` matches any non-alphanumeric character
> `hi\W` matches on `hi$`, `hi*a`

### Repetitions
All of these are used after an expression of character to signify their amount of occurences
`{m}` represents m repetitions of a character
> `i{3}` matches on `hiii`, `hiiiiiii`, `hiiiiiiiiiii`

<br />`{m, n}` represents m to n repetitions of a character
> `i{2, 4}` matches on `hii`, `hiii`, `hiiii` 

<br />`*` represents 0 or more repetitions of a character
> `hi*` matches on `h`, `hi`, `hiiii`

<br />`+` represents 1 or more repetitions of a character 
> `hi*` matches on `hi`, `hiii`, `hiiii`

### Optional
`?` denotes optionality, meaning it will match on zero or one of the preceding characters or groups
> `hi?` matches on `h`, `hi`, `hey`

<br />`\?` matches question mark
> `hi\?` matches on `hi?`, `hi?1`

### Whitespaces
`\s` matches any whitespace, including space, tab, new line, or return
> `hi\sthere` matches on `hi there`, <code>hi&nbsp;&nbsp;&nbsp;&nbsp;there</code>

<br />`\S` matches any non-whitespace
> `hi\S` matches on `hiya`, `hi1`, `hi1 there`

### Starts and ends
`^...$` matches the start and end of a line
> `^hi there$` matches with `hi there`

> `^hi` matches with `hi everyone`, `hi`, `hi there`

> `there$` matches with `hey there`, `over there`, `there`

### Capturing
`(...)` captures group of characters
> `(hi)` matches on `hi`, `while`, `hill`

<br />`(a(bc))` captures sub-group of characters 
> `(hi(\d+))` matches on `hi1`, `hi1932`, `hi123123hi`

<br />`(.*)` captures all
> `hi.*` matches on `hi`, `hi1231232hehusadasjlj`, `hi#$@W@!`

### Boolean "or"
`(a|b)` matches characters on the left or right of the pipe
> `(h|i)` matches on `hi`, `hello`, `igloo`

## Greedy vs. Lazy Quantifiers
Quantifiers (`*`, `+`, `?`, `{m}`, `{m, n}`) at first can seem simple to use, but they can be tricky in many cases! Given this example:
> What does `“.+”` match on for this string: `She said “Hello!” and “How are you?” today.`

Will this match on `“Hello!“` or `“Hello!” and “How are you?”`? Let’s introduce greedy and lazy quantifiers to find out!
- Greedy Quantifiers:
    - Using the example above, the regex will match on `“Hello!” and “How are you?”`. This is because the quantifier is considered greedy, as it will go to the end of the string because the dot matches all characters. Once it has reached the end of the entire string, the regex engine backtracks and until it finds the last `”`. 
- Lazy Quantifiers:
    - On the other hand, if we want to match on just `“Hello!”`, we use the regex `/".+?"/g`. Notice that we added the ‘?’ quantifier after the `+` quantifier! When adding a `?` after another quantifier, it switches from the greedy to lazy matching mode. This mean it will stop as soon as it matches the pattern!


## Common Case Uses
There are many uses for regex as the world of strings is endless, but some common ones include validation for emails, passwords, usernames, URLs, and more! These can be especially useful when your program needs has user accounts, where a user needs to sign up and login. Here are sample regex of the above:
- Email: `/^([a-zA-Z0-9._%-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6})*$/`
    -   Has a username which can include letters, numbers, dots, underscores, percentage signs, and hyphens
    -   Requires the "@" symbol
    -   Validates the domain name, which includes letters, numbers, dots, and hyphens
    -   Has a top-level domain (TLD) consisting of 2 to 6 letters
- Password: `/(?=(.*[0-9]))(?=.*[\!@#$%^&*()\\[\]{}\-_+=~'|:;"'<>,./?])(?=.*[a-z])(?=(.*[A-Z]))(?=(.*)).{8,}/`
    - Requires at least one digit
    - Requires at least one special character
    - Requires at least one upper-case letter
    - Requires at least one lower-case letter
    - Has at least 8 characters
- Username: `/^[a-z0-9_-]{3,16}$/`
    - Has length of 3 to 16 characters
    - Can include _ and -

Something to note is that a lot of common regex that can be found online may not match certain cases. For example, the email regex provided above could not work with some emails that have newer or less common top-level domains. Some emails could also contain special characters, but this is not in this specified regex. There are also some libraries in different languages that handle pattern matching, for example phone numbers can be tricky to handle, so using a library such as Google Library's [libphonenumber](https://github.com/google/libphonenumber) is better and convenient.

## Extra Resources
[RegexOne](https://regexone.com/) - Practice the basic regular expressions<br />
[regex101](https://regex101.com/) - Build, test, and debug regex<br />
[Regexper](https://regexper.com/) - Railroad diagram to illustrate an inputted regex
