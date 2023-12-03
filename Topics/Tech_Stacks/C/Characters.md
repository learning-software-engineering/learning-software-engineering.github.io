# Characters

In order to do word processing, we have to find a way to represent words. In C, words (and phrases and even sentences and paragraphs) are represented as **arrays of characters**, or **strings of characters**. 

This is where we get the term “**string**” from.

For example: “I love coding.” is represented as an array consisting of characters:

`['I', ' ', 'l', 'o', 'v', 'e', ' ', 'c', 'o', 'd', 'i', 'n', 'g', '.', '\0']`

Notice how spaces and punctuation are also represented as characters. 

And there’s a **special character** `\0` at the end, indicating it’s the **end of a string**.

# ASCII Code

In order to store a single character using some sort of numerical value (since we can only store numerical values in a computer’s memory). We need some sort of **encoding**. 

The **ASCII** encoding (American Standard Code for Information Interchange) allows us to store common characters (alphanumerical characters, symbols, and even **control characters** like backspaces and tabs) in a single **byte**, by encoding characters to numbers from **0 to 127**. 

[ASCII - Wikipedia](https://en.wikipedia.org/wiki/ASCII)

Thus behind each character is actually a numerical value, but since it is of type “character”, it will be interpreted as one by the computer.

# Character Variables

To declare a variable that stores a single character, we use the `char` keyword, like so:

```c
char c;
```

To give it a character to store, we can give it a character enclosed in **single quotes** `''`, like so:

```c
char c = 'A';
```

We can also give a character a number (within $[0, 127]$) directly, in this case it will interpret it using ASCII.

```c
char c = 97;  // c has value 'a'
```

But keep in mind that this method not only makes the code **illegible** (i.e. we have to consult the ASCII table to see which character we are assigning), it is also risky because some computers don’t use the ASCII encoding. (e.g. There’s another popular encoding system called **EBCDIC**.)

# The Escape Character

We know a character literal in C are enclosed in single quotes. But what if we want to represent the single quote `'` as a character?

the answer is we type a backslash `\` before the single quote. This backslash is the **escape character**, and allows us to type other special characters that are unavailable to represent in coding.

(And to store the backslash itself, we use the **escape character followed by the backslash**. Since the backslash is a reserved character.)

```c
// Note that < char c = '''; > is illegal,
char c = '\'';  // c now contains a single quote

char c = '\\';  // c now contains a backslash
```

Other special characters include:

`\n` : the **new line character**, or **line feed character** (**LF**), opens a new line for display, like what the “return” key does in text editing

`\r` : the **carriage return** (**CR**), returns the cursor to the beginning of the line without opening a new line

`\a` : the **alarm** or the **bell** (**BEL**), printing this makes the computer beep 

`\0` : the **null character**, does not represent any actual characters, used for the “end of string” character in an character array to signal the end of a string

**Another Use**: We can use the escape character in other ways, such as entering ASCII codes in **octal** and **hexadecimal** form:

```c
char c = '\101';  // 0101 octal is 65 decimal, thus c is 'A'
char c = '\x41';  // 0x41 octal is 65 decimal, thus c is 'A'
```

# Int Operations on Characters

Since behind a `char` is an `int` value, this means that:

- You can always assign a `char` value to an `int` variable
- You can always assign an `int` value to a `char` variable, given the number is in range
- The value of the `char` type can be subject to the same **operations** as data of type `int`. (e.g. `+` `-`). And the `char` and its respective ASCII `int` during these operations are **interchangeable**.

As an example:

```c
char c = 65;  // c is 'A'
c += 32;  // c is now 'a', since 65 + 32 = 97, and 'a' has ASCII code 97
c -= ' ';  // c is 'A' again, since ' ' (space) has ASCII code 32: 97 - 32 = 65

// The following statements are equivalent:
c = 'A' + ' ';
c = 65 + ' ';
c = 'A' + 32;
c = 65 + 32;

int i = 'c' - 'a';  // i is 2, since 'c' is 99 and 'a' is 97: 99 - 97 = 2
i = 97 - 'A';  // i is 32, since 'A' has ASCII code 65: 97 - 65 = 32
```