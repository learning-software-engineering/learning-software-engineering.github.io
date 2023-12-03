# Basic Operators

An **operator** is a symbol of the programming language that does **operations** and is used to **operate on values *(including variables and literals)*.** 

For example, we know that the **assignment operator** is `=` . It assigns values to variables.

# Arithmetic Operations

Arithmetic operators are operators that do operations on numbers to achieve calculations that are common in mathematics.

## Multiplication

In order to multiply 2 values, we use the **multiplication operator**, which is `*`.

Note that `int * int` results in an `int`. 

However, if any of the operands is a `float` or a `double`, the result will be of type **`double`**. 

This means that the result of `10 * 3.2f` will also have type `double`, even though none of the operands are doubles. (i.e. `int * float` → `double` ; `float * float` → `double`)

```c
int i = 10 * 12;  // i has value 120
float x = 10.3 * 2;  // x has value 20.6f
double d = i * s;  // d has value of 2742.0
```

## Division

In order to divide one value by another, we use the **division operator**, which is `/`. 

(`**dividend** **/** **divisor**` → `result`)

If we divide an `int` with an `int` (`int / int`), the result will be the **integer division** of the two values, not the normal division. For example, `11 / 2` will evaluate to `5`. 

However, if any of the operands are `float` or `double`, the result will be of normal division. For example, `11.0 / 2` and `11 / 2.0` both return `5.5`.

```c
int i = 11 / 2;  // i has value 5
float x = 11 / 4.0;  // x has value 2.75f
double d = 11.0f / 4;  // d has value 2.75
```

Division by 0 is **forbidden**. If we divide by 0 (or by 0.0) in code (i.e. we hard-coded a statement such as `x = x / 0.0`), the compiler will throw a **compilation error**. 

If we didn’t hard-code a zero division, but one of the seemingly correct divisions has 0 as its divisor (e.g. `x = x / y` looks correct, but it just so happens that `y = 0`), then the program will either **terminate abnormally** and throw a **runtime error**, or the value of `x` will be unreliable.

## Addition

In order to add one value with another, we use the **addition operator**, which is `+`.

Note that the rules of implicit type conversions still apply.

```c
int i = 10 + 2;  // i has value 12
float x = 10 + 2.2;  // x has value 12.2f
double d = 12 + 10;  // d has value 22.0
```

## Subtraction

In order to subtract one number with another, we use the **subtraction operator**, which is `-`.

(`**minuend - subtrahend**` → `result`)

Note that the rules of implicit type conversions still apply.

```c
int i = 10 - 2;  // i has value 8
float x = 10 - 2.2;  // x has value 7.8f
double d = 12.0 - 10;  // d has value 2.0
```

The subtraction operator can also be used to invert the sign of a number, like so:

```c
int i = -100;  // i has value -100
float x = -i;  // x has value -100.0f
double d = -x;  // d has value -100.0
```

This type of operator is called a **unary** **operator**, because it only has one operand. Other operators like `/` in `x / y` is called a **binary operator**, because it takes 2 operands.

## Remainder

In order to get the **remainder** of an integer division, we use the **remainder** or **modulo operator**, which is `%`.

Note that both operands of the remainder operator must be `int`. No floats this time!

```c
int i = 17 % 5;  // i has value 2, because 17 = 3 * 5 + 2
```

# Operator Precedence

When we have multiple operators in one expression, e.g. `2 + 4 * 5 % 3 - 10`, we would have to determine **in which order** do we evaluate this expression.

In math, we know that multiplication and division **precedes** addition and subtraction, thus `*` and `/` should be evaluated first. This phenomenon of some operators being evaluated before others is called the **hierarchy of priorities**.

The **binding** of the operator determines the order of the computations performed by operators with **equal priority**. In math and in C, operators with equal priority are evaluated **from left to right** (this is called a **left-sided binding**). For example in the expression `3 * 5 / 3`, `3 * 5` is being evaluated first to 15, and then `15 / 3` is evaluated to 5. 

## Arithmetic Operator Precedence

In order from highest to lowest **priority**.

| +, - | (unary operator) |
| --- | --- |
| *, /, % |  |
| +, - | (binary operator) |

## Parentheses

In mathematics, parentheses allow us to override the natural order of calculation, and evaluate the expression in the parentheses first. The same goes in C.

For example, in the expression `5 * (3 + 2)`, despite `+` having lower priority, `(3 + 2)` is evaluated first because it is **enclosed in parentheses** `( … )`, and then `5 * 5`.

We can also have **parentheses nested inside of parenthesis**, in this case, **the expressions in the inner-most parentheses** are evaluated first.

For example, in the expression `k * ((i + j) / (i1 - j1))`, the two expressions `(i + j)` and `(i1 - j1)` are evaluated first.

# Postfix and Prefix Operators

In C, we often have to increment or decrement variables by 1. 

The operators `++` (**increment operator**) and `--` (**decrement operator**) can either be attached before or after a variable to **increment or decrement a variable by 1**.

When we use these operators as **statements**:

`x++;` (or `++x;`) is shorthand for `x = x + 1;`

`x--;` (or `--x;`) is shorthand for `x = x - 1;`

The only difference between `x++` and `++x` (same goes for `x--` and `--x`) is when we are using them as **expressions** and not statements.

For example in `func(x++)` (where `func()` is a function, or it can be substituted with any operation): `**func(x)` gets called first** and then `x` is incremented. This means `x` has the original value when `func(x)` is called. (**Use first, then modify**.)

However, in `func(++x)`, `**x` is incremented first** and after which `func(x)` is called. This means `x` has the original value +1 upon the function call. (**Modify first, then use**.)

These 2 operators have the same priority as unary operators.

Our updated priority table now looks like so:

| +, -, ++, -- | (unary operator) |
| --- | --- |
| *, /, % |  |
| +, - | (binary operator) |
| = | (assignment) |

# Shortcut Operators

Whenever we want to do operations like `x = x + y` or `x = x % 2` or other operations where we operate on a single variable, we would have to type the variable name twice. This gets really inconvenient when the variable name is long.

C provides shortcut operators for this kind of operations (`var = var [op] [expr];`). The rule is `var = var [op] [expr];` → `var [op]= [expr]`. Some examples:

`x += y;` is shorthand for `x = x + y;`

`x -= y;` is shorthand for `x = x - y;`

`x *= y;` is shorthand for `x = x * y;`

`x /= y;` is shorthand for `x = x / y;`

`x %= y;` is shorthand for `x = x % y;`

Our updated priority table now looks like so:

| +, -, ++, -- | (unary operator) |
| --- | --- |
| *, /, % |  |
| +, - | (binary operator) |
| =, +=, -=, *=, /=, %= | (assignments) |