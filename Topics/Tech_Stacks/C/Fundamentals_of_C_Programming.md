# Fundamentals of C Programming

# Basic Concepts of Programming

**Lexicon**: The set of all symbols (letters, words, numbers, punctuation marks, etc.) that could be used in a language is called a language’s **lexicon**.

**Syntax**: The set of rules that determine the correct ways to arrange symbols to form a valid meaning in a language is called a language’s **syntax**.

**Semantics**: And the meaning that comes from arranging elements from the lexicon of a language according to its syntax is called a language’s **semantics**.

**Portability**: The feature of **high-level languages** that allows it to be compiled and run on almost any processor architecture is called **portability**.

**Compilation**: Normally, a **compiler** translates the **source code** (in the **source** **file**) to machine code that the processor can understand (as an **executable file**). This process is called **compilation**.

**Linking**: When we have multiple source files as part of one program, the compiler will first compile them into executables, and then the **linker** will join (or glue) the executable files together into a single unified product. This process is called **linking**.

**General-Purpose Programming Language**: C is a **general-purpose programming language**, meaning that it is suitable for almost any programming project, while not being tailored to any specific usage.

**Algorithm**: The finite sequence of instructions for a calculation in a program is called an **algorithm**.

# Structure of a C Program

Take a simple C program for an example.

```c
#include <stdio.h>

int main(void){
    puts("It's me, your first program.");
    return 0;
}
```

## Preprocessor Directives

The lines of code at the beginning of a source file that begin with `#` are called **preprocessor directives** (e.g. `#include <stdio.h>`). These lines are read by the compiler **before the compilation of the code**, to make internal modifications to the code, such as importing libraries (e.g. `stdio.h`) or macro replacements (e.g. replacing all `MAX_NUM` with `10000`). But of course, preprocessor directives do not change the source file itself.

In our example, the `puts()` function (which displays a string of characters in a single line) is undefined in our source code. So in order to use it, we would have to import it from the **header file** `stdio.h`, which contains preliminary information for the compiler to use the functions within the “`stdio`” or “standard IO” library.

## Functions

One of the fundamental building blocks of a program is a **function**. A function takes in a number of inputs called “**arguments**” or “**parameters**”, performs a sequence of actions on them, and then returns an output or a number of outputs (”**results**”). 

Note that a function can also take no inputs, and can also return no outputs. 

In order to define a function we start by the **return type** of the function (e.g. `int` for “**integer**”), followed by the **name** of the function (e.g. `multiply`), then followed by the **arguments** in parentheses, with each argument being in the format: **[type] [name]**. (These information are called the function’s **prototype**.) Then what follows is the **implementation** (**body**) of the function in brackets, like so:

```c
int multiply(int a, int b){
    return a * b;
}
```

If the function does have an output, then we must have a `return` statement in the function to return the result back to the function user. (Note that after the return statement, the function immediately terminates.)

If a function gives out no outputs, then it’s output type would be `void`, and no return statement is present in the function, like so:

```c
void displayInteger(int a){
    printf("%d", a);  // This displays an integer to the terminal.
}
```

**The Semicolon**: As we can now see from the code examples above, every line of code that does something (every **statement**) in C must end with a semicolon `;`. This is the way the compiler distinguishes each line from another.

**The Main Function**: All C programs must have a **main function** called `main`, and it’s prototype is `int main()` or `int main(void)`. This is where the code will start running in the executable.

The main function should do `return 0;` if it’s a normal exit of the program. And it should do `return 1;` if something has gone wrong in the program, and it needs to inform the operating system.

**The Function Call (Function Invocation)**: To call a function, we simply have to write the name of the function, then give it the parameters that it requires within the parentheses after the name. Like so: (when the function does not return anything)

```c
puts("Hello World!");  // This will run on its own. Since it's a statement.
```

If the return value is not `void`, then we would have to put the return value somewhere, such as in a variable, like so:

```c
int a = 4;
int x = multiply(a, 2);  
// Now we are required to put return value somewhere. 
// Since the function call is now an expression, and not a statement.
```

## Comments

Comments are essential to good code writing, to be able to explain what a piece of code does to other readers (or the future you).

```c
// This is a single-line comment

/*
	This is also a comment.
  But it spans multiple lines. It's a multi-line comment.
*/

/**
 * This is also a multi-line comment.
 * But it's used before functions for documentation purposes.
 * @param par1 explains what parameter 1 is
 * @return explains what the return value does
 */
```

Nested comments, like this: `/* abc /* def */ g */` are forbidden!

# Numbers and Variables

In C, there are 2 types of numbers: **integers** (whole numbers), and **floating** **point** **numbers** (numbers that have decimal point values). These two must be distinguished from each other, since they are stored differently inside memory.

The type signature of an integer is `int`, and the type signature of a floating point number can be `float` or `double` (a double stores more digits but takes up more space).

In C, a simple number, e.g. `123`, is always in decimal form. 123 means 123.

However, if you want to write **octal** numbers (0 to 7 carry at 8), then you add an extra `0` at the beginning of the number, e.g. `0123` is an octal number is equal to 83 in decimal.

If you want to write numbers in **hexadecimal**, then you add `0x` before the number, e.g. `0x123` is equal to 291 in decimal.

## Variables

A **variable** is a **container** that has a name, that stores a value of some type. 

The name of a variable must **start with a letter** (or an underscore character), and can only contain **letters, numbers, and underscores**. 

Variable names are **case-sensitive**, meaning that upper and lower case counterparts are treated as different characters.

Variable names also **must not be reserved keywords** by the C language (e.g. `int`, `if`, `while`).

To use a variable, we must **declare** it first. This tells the system to allocate space in memory for this variable.

To declare a variable, start with the **type signature** of the data that the variable is designed to store (e.g. `int`, `float`, `double`, `char` (characters), `bool` (boolean values, either true or false) ), then the **name** of the variable, like so:

```c
int firstVariable;
float secondVar;

double aDouble, anotherDouble;  // Declaring 2 doubles at the same time.
// Put a comma in between variable names to declare them together.
```

We give a variable a value (or “**assigning** it a value”) by using the operator `=`, like so:

```c
firstVariable = 4;  // Now firstVariable has a value of 4.
secondVar = 3.14;  // Now secondVar has a value of 3.14.

firstVariable = 1 + 2;  // firstVariable is given the RESULT of 1 + 2, which is 3.

firstVariable = firstVariable + 1;
// firstVariable is 'updated' to where it now contains its PREVIOUS value plus 1,
// which is 4.
```

We can also assign a variable a value at the same time as declaring it, this is called “initializing” a variable, and it is done like so:

```c
float thirdOne = 10.123;  // Now thirdOne is created and given the value 10.123.
```

### Type Modifiers

Normally, an `int` value is stored in **4 bytes (32 bits)**, and has range $\mathbb{Z}\cap [-2^{31}, 2^{31}-1]$, which is: $\mathbb{Z}\cap [-2147483648, 2147483647]$. 

**Long Long Modifier**: Now, if we need to store an integer that is outside of this range, we can add the modifier `long long` before the `int` when declaring, this will store the value in **8 bytes (64 bits)**, and has range $\mathbb{Z}\cap [-2^{63}, 2^{63}-1]$, which is $\mathbb{Z}\cap [-9223372036854775808, 9223372036854775807]$.

```c
long long int x;
long long y;  // We can also omit the "int" when declaring

x = 99999999999; // This number is auto-recognized as long,
// since it's outside the range of normal int.
```

If we want to specifically tell the compiler to recognize a number literal as long, then we have to add the letter `l` or `L` at the end of the number, like so: `123l`, `123L`

**Short Modifier**: We can also add modifier `short` before the `int` when declaring, this will store the value in 2 bytes (16 bits), and has range $\mathbb{Z}\cap [-2^{15}, 2^{15}-1]$, which is $\mathbb{Z}\cap [-32768, 32767]$.

```c
short int x = 128;
short y;  // We can also omit the "int" when declaring
```

**Unsigned Modifier**: If we add `unsigned` before a declaration of an `int` (or `char`), this will only allow **non-negative numbers** in the variable, allowing double the range on the positive side.

For example, `unsigned short` has range $\mathbb{Z}\cap [0, 2^{16}]$ instead of $\mathbb{Z}\cap [-2^{15}, 2^{15}-1]$.

```c
unsigned short x;
unsigned long long y;
unsigned int z;
```

# Basics of `Printf`

The `printf()` (”**print formatted**”) function prints things to the terminal (or console) in a certain format. It takes at least 1 parameters, where:

The first parameter is always a string (a series of characters enclosed in double quotes, e.g. `“abc”`), this determines the **format** of what is being displayed, including what is constant.

Within the string, you can insert `%d` to display an integer, `%f` to display a float, `%lf` to display a double (or “long float”), `%s` to display a string, and `%c` to display a character. These are called **specifiers**.

(In addition, `%x` displays an int in hexadecimal form, and `%o` displays an int in octal form.)

(To display the percentage sign (%) itself, use `%%`. )

**Important Note**: The number of arguments following the format argument MUST be equal to the number of specifiers!

```c
printf("This is a message.");  // Will display: This is a message.
printf("The number is: %d", 4);  // This number is: 4
printf("The numbers are: $d, %f, %d", 1, 2.3, 4);  // The numbers are: 1, 2.3, 4
printf("The message: %s\n", "Hello!");  // The message: Hello!
// Note: "\n" goes to a new line.
```

Within the string, `\n` means a “new line” character (enter key), and `\t` means a tab character. We can use this for some basic formatting.

Note that if we want to switch to new lines, we have to do it manually by adding `\n`, since printf prints **character by character**.

# Basics of `Scanf`

The `scanf` (”**scan formatted**”) function is the **input** counterpart of `printf`.

Similarly, the first parameter is a string, denoting the **format** of the input, so that the program knows how to interpret the inputs.

For example, if we want to read an integer and put it inside variable `x`:

```c
int x;
scanf("%d", &x);

float a, b;
scanf("%f %f", &a, &b);
```

The `&` next to the variable name means “**the address of**”. If we remove the `&`, then we are only providing a value, and not **where** to store the input. Hence the necessity `&`.