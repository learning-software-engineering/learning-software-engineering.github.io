# Strings

# Introduction

In order to do word processing, we have to find a way to represent words. In C, words (and phrases and even sentences and paragraphs) are represented as **arrays of characters**, or **strings of characters**. This is where we get the term “**string**” from.

For example: “I love coding.” is represented as an array consisting of characters:

`['I', ' ', 'l', 'o', 'v', 'e', ' ', 'c', 'o', 'd', 'i', 'n', 'g', '.', '\0']`

Notice how spaces and punctuation are also represented as characters. 

And there’s a **special character** `\0` at the end, indicating it’s the **end of a string**.

To create a string, for the above example:

```c
char example[100] = "I love coding.";
```

The `\0` null character is automatically added at the end.

Note that in this case we cannot use `sizeof()` here to get the size of our `example` string, since it will return `100`, the number of **spaces available** for storage, **NOT 14**, the number of meaningful characters inside the array.

To do this, C provides the `**strlen()**` ”**string length**” function in the `string.h` library.

`**strlen()`** basically counts from the beginning of the array to see how many non-null characters there are until it reaches the `\0` null character.

Since `example[]` is an array, `example` is also a **pointer to the first character** of the string (`example == &example[0]` where `example` is of type `char *`). 

We can also create a string like this:

```c
char str[] = "a string";
```

In this case, the size of `str` would be **9**, the number of meaningful characters **PLUS 1** (to store the `\0` null character at the end).

This method is similar to doing:

```c
char *str = "a string";
// The space for the string is reserved first, along with its value,
// then the location of the first character is assigned to str.

// However, this is a string CONSTANT, and is immutable.
// Because the string is not put in the stack.
```

# Operations with Strings

## The `strcpy` Function : Assigning and Copying Strings

Say we have a string: `char str[100] = "a string"`. 

We **CANNOT reassign its value as if it’s a normal variable**: `str = “another one”`, since `str` is of type `char *` (a **pointer**) that is **fixed to that location in memory**. 

**The C compiler does not allow array name pointers to be overwritten**. Otherwise the location `str` is pointing to is completely lost.

Instead, we should use the **`strcpy`** (”**string copy**”) function from the `string.h` library.

```c
char str[100] = "a string";
strcpy(str, "another one");  
// This copys the value of the second argument into the first.
```

This also works with copying the value of one string into another:

```c
char s1[100];
char s2[] = "a string";
strcpy(s1, s2);
// The VALUE of s2 gets copied into s1.

// But note that since s1 and s2 are still POINTERS that point to different
// locations in memory, s1 != s2 still.
```

**Important Note**: Before we copy one string into another, we have to make sure that there’s enough room (enough available character spaces) for the new string to fit in.

If we do `s1 = s2`, the compiler will **throw an error**, since we would be making `s1` and `s2` point to the same string in memory (`s2`’s location); and the original location of `s1` would lost. **The C compiler does not allow that**. 

### An Exception:

However, if we created our string **not with arrays, but with pointers**, the following is possible:

```c
char *str_p = "a string";
str_p = "another";
```

This is because `str_p` is **not an array name pointer**, it’s just **a normal `char *` pointer**. Thus C allows it to be overwritten. 

Of course, `"a string"` is still somewhere in memory, its location is just overwritten by the location of a new string (`"another"`).

In summary, just keep in mind that the **variable names of strings are `char *` pointers**. And that:

- **Array name pointers cannot be reassigned.**
- **Normal pointers can be reassigned.**

## The `strncpy` Function

The `**strncpy()**` function is similar to `strcpy()`, except there’s a third integer parameter that stands for the **maximum number of characters to copy** from the source into the destination.

For example:

```c
char str[20];
strncpy(str, "ABCDEFG", 4);  // str is now "ABCD"
strncpy(str, "Computer", 3);  // str is now "Com"
```

**Important Note**: In real-world applications, **it is better to use `strncpy()` whenever possible instead of `strcpy()`**. This is because `strcpy()` is considered “unsafe” due to it being much more susceptible to overwriting unwanted memory locations.

## The `strcat` Function: Append One String to Another

The `**strcat()**` function **appends a copy of the source string to the destination string**. Only the destination string is modified.

How it works: The function looks for the current string’s `\0` character, removes it, and adds the source string to the end of the destination string.

From this we know that **the destination string MUST BE INITIALIZED** beforehand, i.e. it must contain a `\0` character.

For example:

```c
char str[100] = "";
strcat(str, "Hello");  // str is now "Hello"
strcat(str, " world,");  // str is now "Hello world,"
strcat(str, " yall!");  // str is now "Hello world, yall!"
```

# Printing a String

To print a string on a single line, we can use the **`puts()`** function, like so:

```c
char str[] = "a string";
puts(str);
```

The statement `puts(str);` does the same thing as `printf("%s\n", str);`, printing the string **with a new-line character added at the end**.

(Note: `puts()` also returns `-1` if there’s an error, otherwise it returns a non-negative number. We don’t have to put the result anywhere in most cases, but we can use it for debugging.)

# Mistakes when Using Pointers

## Mistake 1: Using Uninitialized Pointers

When we create a string using `char *` instead of `char[]`, we **must initialize it** in some way. 

Or else the pointer would pointing to somewhere we don’t know, and if we try to modify the string with functions like `strcpy()`, then it will modify values in address we don’t want.

For example:

```c
char *str;
strcpy(str, "a string");  // THIS IS WRONG!!!
```

We **cannot dereference an uninitialized pointer** either, for example:

```c
char *str; 
*str = 'c';  // THIS IS WRONG!!!
```

Instead, we can initialize it by giving it an address to a string, like so:

```c
char *str = "initialized";  // This is okay.
```

## Mistake 2: Exceeding the Size of the Array

We have to make sure that if we were to modify a string (e.g. `strcat()` and `strcpy()`), we have to make sure that we have space to put it. Or else it will modify values in unallocated memory space, cause a memory violation error. 

For example:

```c
char str[10];
strcpy(str, "a very very very long string");  // THIS IS WRONG!!!
```

## Mistake 3: Non-Terminated Strings

In C, all strings must end with a `\0` character to mark the end thereof. 

Thus if we use a function like `strcat()`, whose functionality depends on the `\0` character, on a non-initialized string, there will be problems.

For example:

```c
char str[10];  // An uninitialized string, has no value.
strcat(str,"a string");  // THIS IS WRONG!!!
// The strcat() function doesn't know where to add the string. 
```