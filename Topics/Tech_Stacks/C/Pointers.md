# Pointers

# Referencing and Dereferencing

Each **byte** (8 bits) in memory has a unique address to it. 

And since each variable in C is stored in a certain memory location, each variable would have an “**address**”, describing **where it is being stored**.

And since sometimes we need to know where a variable is being stored, we can declare special variables called “**pointers**”, that **store the address of a variable**.

For example:

```c
int x = 10;
int *p = &x;
```

The `int *` makes the variable `p` a **pointer that stores the address of an `int`**.

The `&` before `x` means “**the address of**”. This is called a **reference operator** (converts value to address).

Thus in the second line we are **giving the address to `x` to `p`**. Now the variable `p` now stores the address of `x`.

Now we add this line to the above code:

```c
int y = *p;
```

The `*` before `p` means “**the value of**”. This is called a **dereference operator** (converts address to value).

Thus in this line we are **giving the value of `p` (which is `x`) to `y`**. Now the variable `y` contains the same value as `x`. 

However, note that `x` and `y` are still stored in different memory locations. (i.e. They are not **aliases** of each other.)

We can also use the dereference operator actively like so:

```c
*p = 12;
```

This **modifies** **the value that `p` is pointing to**. In other words, `x` is now `12` instead of `10`.

## Null Pointer

We also can make a pointer that points to nowhere (called a “**null pointer**”), for example:

```c
int *p = NULL;
```

(`NULL` is actually a **macro** of `0` that is defined in `stdio.h`. Assigning a pointer the value `0` also makes it a null pointer.)

Null pointers are said to be “**grounded**” (like in electricity), since it doesn’t point to anything.

Dereferencing a null pointer is forbidden, and will result in a runtime error.

## Void Pointer

We can actually create a pointer of type `void`, like so:

```c
void *ptr;
```

This is called an **amorphous pointer**, and can point to **any value of any type**.

However, this kind of pointers also **cannot be dereferenced**.

## Reference and Dereference Operator Priority

The updated operator priority table is as follows:

| !, ~, (typecast), +, -, ++, --, * (dereference), & (reference), sizeof | (unary operators) |
| --- | --- |
| *, /, % | (binary arithmetic - high priority) |
| +, - | (binary arithmetic - low priority) |
| <<, >> | (bit shift operators) |
| <, <=, >, >= | (comparison operators - high priority) |
| ==, != | (comparison operators - low priority) |
| & | bitwise AND |
| | | bitwise OR |
| && | logical AND |
| || | logical OR |
| =, +=, -=, *=, /=, %=, &=, ^=, |=, <<=, >>= | (assignments and shorthands) |

## Pointers and Arrays

When we define an array, say for example:

```c
int arr[10];
```

The name of the array `arr` actually contains the **address to the first element of the array**.

In other words `arr == &arr[0]`.

# Pointer Arithmetic

The operations that we can do on pointers is very different from those we can do on integers, in that it is very reduced and contains the following only:

- **Adding an integer value to a pointer**. (`ptr = ptr + int`)
- **Subtracting an integer value from a pointer**. (`ptr = ptr - int`)
- **Subtracting a pointer from a pointer, returning an integer**. (`int = ptr - ptr`)
- **Comparing two pointers**, returns an int value of either `1` (`true`) or `0` (`false`). (`int = (ptr == ptr`) ; `int = (ptr != ptr)`)

Any other operation is not allowed.

Example:

```c
int *ptr1, *ptr2, arr[10];

ptr1 = arr;
ptr2 = &arr[0];
// Right now (ptr1 == ptr2) returns true.

ptr1 += 1;
// ptr1 is now equal to &arr[1], EVEN THOUGH an int takes up 4 bytes.

ptr2 = ptr1 + 3;  // ptr2 is now &arr[4]
ptr2 -= 1;  // ptr2 is now &arr[3]
```

Notice that adding `1` to the pointer makes it point to the **next value in the array**, even though an `int` takes up 4 bytes. This is because when we add an integer, say `n` ($n\in \mathbb{Z}$), to a pointer, the pointer’s **actual value** actually gets incremented by `n * sizeof(*p)`, or `**n` times the size of the type of value that `p` is pointing to**.

C does this with pointers **automatically**, so no need to worry about `sizeof(type)` when doing pointer addition and subtraction.

```c
int i = ptr2 - ptr1;  // i is equal to 2
// Since ptr2 == &arr[3] and ptr1 == &arr[1], the DIFFERENCE IN INDEX 
// between them is 2.

// Also, ptr1 - ptr2 is -2, and ptr1 - ptr1 is 0, by the same logic.
```

## Reality behind Indexes of Arrays: The `[]` Operator

We already know that when we define an array, say `int arr[10]`, the name of the array `arr` actually contains the **address to the first element of the array** (`arr == &arr[0]`).

When we access an element of an array with `arr[i]`, what this actually means is `***(arr + i)**`, i.e. the value at the address `arr + i`, with the pointer arithmetic defined above.

This means that we can also have **negative indexes** for this notation, for example:

```c
char str[10] = "dusk";
p = string + 2;  // p is now pointing to 's' in "dusk"

p[-1] = 'e';  // p[-1] is same as *(p - 1), which points to 'u' in "dusk"
// And now 'u' is being modified into 'e'

puts(str);  // will print "desk"
```

The newest operator priority table is thus:

| [], ++ (postfix), -- (postfix) | (postfix unary operators) |
| --- | --- |
| !, ~, (typecast), +, -, ++ (prefix), -- (prefix),
* (dereference), & (reference), sizeof | (prefix unary operators) |
| *, /, % | (binary arithmetic - high priority) |
| +, - | (binary arithmetic - low priority) |
| <<, >> | (bit shift operators) |
| <, <=, >, >= | (comparison operators - high priority) |
| ==, != | (comparison operators - low priority) |
| & | bitwise AND |
| | | bitwise OR |
| && | logical AND |
| || | logical OR |
| =, +=, -=, *=, /=, %=, &=, ^=, |=, <<=, >>= | (assignments and shorthands) |