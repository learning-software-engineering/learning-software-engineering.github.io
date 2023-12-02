# Control Flow & Bitwise

# Comparison Operators & The Boolean Type

In order to have our code behave differently depending on the conditions during runtime, we need to be able to **represent and answer “yes no” questions** in our code.

Some of the questions that we might ask are, for example:

- Are the variables `x` and `y` equal to each other in value?
- Is `x` greater than `y` in value?
- Is `i` greater than or equal to `j`?

To compare values, we can use **comparison operators**, like so:

- `x == y` this **expression** evaluates to the result of: whether `x` and `y` are equal in value
- `x != y` whether `x` is not equal to `y` in value
- `x > y` whether `x` is greater than `y`
- `x < y` whether `x` is less than `y`
- `x >= y` whether `x` is greater than or equal to `y`
- `x <= y` whether `x` is less than or equal to `y`

Yet we still need a way to store the answer to these questions (the results of these expressions). Thus we have another data type called the “**boolean**” type in C. 

Booleans can only have two values: `true` (`1`) or `false` (`0`).

To declare a boolean variable, we use the `bool` keyword. 

(**Note**: We also need to do `#include <stdbool.h>` to enable `bool` type in C.)

```c
int a = 4, b = 7;
bool x;
x = (a < b);  // x has value **true**
x = (a >= b);  // x now has value **false**

// Important Note: Boolean values are also represented with integers,
// where true is 1 and false is 0.
int x; 
x = (a < b);  // x has value 1
****x = (a >= b);  // x now has value 0
```

Comparison operators have **lower priority than arithmetic operators**, for example:

For the expression `x == 2 * y`, “`2 * y`” is evaluated first, then `==` is evaluated.

Our now updated operator precedence table would be:

| +, -, ++, -- | (unary operator) |
| --- | --- |
| *, /, % |  |
| +, - | (binary operator) |
| <, <=, >, >= | (comparison) |
| ==, != | (comparison) |
| =, +=, -=, *=, /=, %= | (assignments) |

# Conditional Execution

C has special instructions that allow us to execute code **only upon certain conditions**. These instructions are called **conditional instructions** or **conditional statements**.

## Simple If Statement

The simple `if` statement takes the form:

```c
if(bool_expression){
    ...  // Do this if bool_expression evaluates to true.
}

// If bool_expression is false, then the instructions inside the parentheses
// will be skipped.
```

We can put many instructions inside the brackets, and if `bool_expression` is `true`, then the instructions inside will be **conditionally executed**. These instructions are called a **compound statement** or a **block**, and they are seen as 1 statement by the compiler. 

If we have multiple instructions inside an `if` statement, they must be **indented** by 1 level from the code outside the brackets, like so:

```c
if(x > y){
    x = x + y;
    y = y + x;
}
x = y;
```

This style of writing code is called the **K & R Style**, named after the creators of C.

Note that we can also omit the brackets whenever there’s only one statement inside the `if` statement, like so:

```c
if(bool_expression)
    doSomething();
```

## If-Else Statement

The `if ... else` statement takes the form:

```c
if(bool_expression){
    ...  // Do this IF AND ONLY IF bool_expression is true.
}else{
    ...  // Do this IF AND ONLY IF bool_expression is false.
}
```

Note that we can also nest `if` statements inside of `if` statements, this is called **nesting**. For example:

```c
if(condition){
    if(another_condition){
        ...
		}
}else{
    if(a_third_condition){
        ...
    }else{
        ...
    }
}
```

### Else If

The `else if` statement is a bit complex, it takes the form:

```c
if(first_condition){
    ... // Do this if first_condition is true, then SKIP all remaining conditions.
}else if(second_condition){
    ... // Do this if first_condition is false, but second_condition is true.
}else if(third_condition){
    ... // Do this if both conditions above are false, but third_condition is true.
}
```

We can also add a condition to handle the case when all conditions are false, like so:

```c
if(first_condition){
    ...
}else if(second_condition){
    ...
}else if(third_condition){
    ...
}else{
    ... // Do this when ALL conditions above are false.
}
```

Note that the program will examine the conditions **sequentially**. Whenever a condition is met, the corresponding code block will be run, and afterwards the rest of the conditions will be **skipped**.

So say for example if `first_condition` and `third_condition` are both true, then only the block corresponding to `first_condition` will be run, and the block corresponding to `third_condition` will be skipped. 

# Boolean Logic

- **Conjunction (AND)** - **Test if both things are true** (“**`A && B`**”): 
Takes 2 **boolean** inputs, gives 1 **boolean** output.
Given bool variables or expressions `A` and `B`, the expression “`A && B`” returns a bool variable. It evaluates to **true** if and only if `A` and `B` are **both true**. Otherwise it evaluates to **false**.
    
    
    | A | B | A && B |
    | --- | --- | --- |
    | True | True | True |
    | True | False | False |
    | False | True | False |
    | False | False | False |
- **Disjunction (OR)** - **Test if at lease one of both things is true** (“**`A || B`**”): 
Takes 2 **boolean** inputs, gives 1 **boolean** output.
Given bool variables or expressions `A` and `B`, the expression “`A || B`” returns a bool variable. It evaluates to **true** when **at least one** of the two is true. It evaluates to **false** if and only if both `A` and `B` are **false**.
    
    
    | A | B | A \|\| B |
    | --- | --- | --- |
    | True | True | True |
    | True | False | True |
    | False | True | True |
    | False | False | False |
- **Negation** **(NOT)** - **Test if a thing is false** or **Flip a bool value (from true to false, or from false to true)** (“**`!A`**”): 
Takes 1 **boolean** input, gives 1 **boolean** output.
Given a single bool variable or expression `A`, the expression “`!A`” returns a bool variable. It evaluates to **true** when `A` is **false**; and it evaluates to **false** when `A` is **true**.
From this we know that, for any bool expression `A`, when we use `!` on it (**negate** it) 2 times, the result is equal to the original value, i.e. `!(!A) == A`.
***Important Note***: When negating an expression (which is not a single variable), remember to “protect the expression” by **enclosing it in parentheses**, because `!` takes priority over other operators like `&&` or `||`, and will often times mess up the expression that you are trying to negate. 
For example, `!(A && B)` is not the same as `!A && B` (because `!A` is evaluated first), thus we need to write `!(A && B)` when we need to negate `A && B`. In short, it’s good practice to write `!(...)` instead of `!...` for safety when negating any bool expression.
    
    
    | A | !A |
    | --- | --- |
    | True | False |
    | False | True |

# Bitwise Operations

Bitwise operations treat values (integer values like `int`, `short`, `char`) as arrays of binary digits (e.g. `short x = 126;` would be `00000000 11111110`), and then do **logical operations** on them **bit by bit**.

- **Bitwise Conjunction (Bitwise AND)** - (”`x & y`”): 
Does the AND operation on **each corresponding bit** of `x` and `y`.
Say for example `x = 7` (`00000111`) and `y = 28` (`00011100`), `x & y` would be `00000100` in binary, or `4`.
- **Bitwise Disjunction (Bitwise OR)** - (”`x | y`”)
Does the OR operation on **each corresponding bit** of `x` and `y`.
Say for example `x = 7` (`00000111`) and `y = 28` (`00011100`), `x | y` would be `00011111` in binary, or `31`.
- **Bitwise Negation (Bitwise NOT)** - (”`~x`”)
Does the NOT operation on **each single bit** of `x`.
Say for example `x = 7` (`00000111`), then `~x` would be `11111000` in binary.
And if `x` is a **signed number**, then `x = -8`; if `x` is an **unsigned number**, then `x = 120`. (Very important to take the sign into account.)
- **Bitwise Exclusive Disjunction (Bitwise XOR)** - (”`^`”):
Does the XOR operation on **each corresponding bit** of `x` and `y`.
Say for example `x = 7` (`00000111`) and `y = 28` (`00011100`), `x ^ y` would be `00011011` in binary, or `27`.

# Bit Shifting

Bit shifting treat values (integer values like `int`, `short`, `char`) as arrays of binary digits (e.g. `short x = 126;` would be `00000000 11111110`), and then shift the bits **either left or right**.

- **Bitwise Left-Shift** - (”`x << y`” where `y` is an integer):
Shifts the binary value of `x` towards the left by `y` bits. The news spaces are filled with 0’s.
For example `x = 7` (`00000111`), then `x << 2` would be `00011100`, or `28`.
- **Bitwise Right-Shift** - (”`x >> y`” where `y` is an integer):
Shifts the binary value of `x` towards the right by `y` bits. 
However, depending on **whether the number is signed or unsigned**, and **whether the number is positive or negative if signed**, the spaces will be filled with either 1 or 0:
    - If the number is **unsigned**, the empty spaces are filled with 0’s.
    For example `x = 7` (`00000111`), then `x >> 2` would be `00000001`, or `1`.
    - If the number is **signed and positive**, the empty spaces are filled with 0’s.
    For example `x = 7` (`00000111`), then `x >> 2` would be `00000001`, or `1`.
    - If the number is **signed and negative**, the empty spaces are filled with 1’s.
    For example `x = -7` (`11111001`), then `x >> 2` would be `11111110`, or `-2`.
    
    In other words, if the number is **signed**, then when we right shift it, the empty spaces will be filled with the **rightmost bit** of the original value.
    

Thus the up-to-date operator precedence table would be:

| !, ~, (typecast), +, -, ++, -- | (unary operators) |
| --- | --- |
| *, /, % | (binary arithmetic - high priority) |
| +, - | (binary arithmetic - low priority) |
| <<, >> | (bit shift operators) |
| <, <=, >, >= | (comparison operators - high priority) |
| ==, != | (comparison operators - low priority) |
| & | bitwise AND |
| \| | bitwise OR |
| && | logical AND |
| \|\| | logical OR |
| =, +=, -=, *=, /=, %=, &=, ^=, |=, <<=, >>= | (assignments and shorthands) |

# Switch-Case

A `switch … case` statement takes the form:

```c
switch(expression){
    case LITERAL_1:
        ...  // Runs if expression == LITERAL_1
        break;  // After running, skip to the end
    case LITERAL_2:
				...  // Runs if expression == LITERAL_2
				break;  // skip to end

		case LITERAL_3:
				...  // Runs only when expression is LITERAL_3
		case LITERAL_4:
				...  // Runs when expression is LITERAL_3 or LITERAL_4,
				     // since there's not break statement at the end of LITERAL_3's case
				break;

		default:
				...  // Runs if expression is not equal to any of the above literals.

}
```

Each of the cases are scanned **sequentially**, just like in `if ... else if` statements.

Note that unlike `if ... else if` statements, after running instructions inside a `case`, the program does not skip to the end, and **keeps on running**, unless there’s a `break;` statement at the end of a `case` block.