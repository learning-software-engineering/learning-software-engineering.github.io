# Regular Expressions (Regex)

## Table of contents
### [Introduction](#introduction)
### [Basic Regular Expressions](#basic-regular-expressions)
### [Extra Resources](#extra-resources)

## Introduction
Regular expressions, also known as regex or regexp, are a sequence of characters that define pattern matching within strings. It is a powerful tool used in a variety of text and string processing tasks, such as data valdidation, data scraping, simple parsing, and more.

With regular expressions, one can: 
- Search: Look for specific patterns within strings
- Validate: Check if a string matches a pattern
- Replace: Change parts of a string that match a pattern
- Extract: Take specific parts of a string that match a pattern

Regular expressions are made up of characters (matching themselves), metacharacters (matches with groups of characters such as digits, letters, and whitespace), quantifiers (amount of times a character or group appears), and much more that allow for complex pattern matching! 

## Basic Regular Expressions
### Characters
Any character will match itself, this includes alphabet letters, digits, and any symbols.
### Digits
`\d` matches any digit character
`\D` matches any non-digit character

### Anything
`.` matches any character
`\.` matches period (as period alone matches everything)
### Specific Characters
`[abc]` matches specific characters within the brackets, in this case, only a, b, or c
`[^abc]` excludes specific characters within the brackets and hat, in this case, a, b, or c

### Character Ranges
`[0-9]` matches sequential numbers from 0 to 9 using the dash to indicate range
`[a-z]` matches sequential letters from a to z using the dash to indicate range and is also case-sensitive
`\w` matches any alphanumeric character
`\W` matches any non-alphanumeric character

### Repetitions
All of these are used after an expression of character to signify their amount of occurences
`{m}` represents m repetitions of a character
`{m, n}` represents m to n repetitions of a character
`*` represents 0 or more repetitions of a character
`+` represents 1 or more repetitions of a character 

### Optional
`?` denotes optionality, meaning it will match on zero or one of the preceding characters or groups
`\?` matches question mark

### Whitespaces
`\s` matches any whitespace, including space, tab, new line, or return
`\S` matches any non-whitespace

### Starts and ends
`^...$` matches the start and end of a line

### Capturing
`(...)` captures group of characters
`(a(bc))` captures sub-group of characters 
`(.*)` captures all

### Boolean "or"
`(a|b)` matches characters on the left or right of the pipe

## Extra Resources
[RegexOne](https://regexone.com/) - Practice the basic regular expressions
[regex101](https://regex101.com/) - Build, test, and debug regex
