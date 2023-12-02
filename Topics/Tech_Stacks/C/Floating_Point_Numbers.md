# Floating Point Numbers

All numbers with decimal points are considered **floating point numbers**, like `3.14`, `-2.5`, or even `3.0` and `0.0`. They are different from integers in that they **CAN contain decimal points**, since they are stored fundamentally differently in memory.

# Type Inference

C automatically infers the type of number literals.

Any number without a decimal point will be inferred as an `int`, e.g. `3`, `-10`.

Any number with a decimal point value will be inferred as a `double`, which is essentially a `float` but has more precision (and also takes up more space in memory), e.g. `4.15`, `-0.24`.

Any number with a decimal point value, and with a lower case letter `f` at the end will be inferred as a `float` value, e.g. `3.14f`, `-0.0f`.

## Scientific Notation

Say we wish to write a number in scientific notation, e.g. `3.14 * 10^8`, we can write the number `3.14E8` in C to give it to a variable. 

Note that a number in scientific notation is by default a **`double`** (this even applies when the **mantissa**, or the number part, does not contain decimals, like `3E4`). 

If we want to write a number in scientific notation of type `float`, we again have to add the letter `f` at the end of the number, e.g. `3.14E4f`.

In summary, the **mantissa** can be any decimal number, while the **exponent** can only be an integer. Negative exponents are also okay, e.g. `6.62607E-34`.

## Implicit Type Conversion

When you assign an integer to a `float` or `double` variable, it will be automatically converted to `float` or `double`, retaining the same value, like so:

```c
int i = 123;
float f = i;  // f is assigned the value 123.0f
double d = i; // d is assigned the value 123.0
```

However, when you assign a `float` or `double` number to an `int` variable, it will also be automatically converted, but the decimal part will be **simply cut off**, resulting in **loss of accuracy**.

```c
float f = 123.123f;
double d = 321.98;

int i = f;  // i is assigned 123
int i = d;  // d is assigned 321, note that there is no rounding!
```

Also, since an `int` can only store number in range $[-2^{31},~ 2^{31}-1]$ or from -2147483648 to 2147483647, if an `int` is assigned a value out of this range, the value of it will be overflow and be **erroneous**. Depending on the system, it can either be the minimum possible number, the maximum possible number, or some random number.

```c
double d = 3E20;
int i = d;  // The value of i will be erroneous!
```

This potential issue is an example of an ******implementation-dependent issue******, and can damage **software portability**.

**Other Common Implicit Type Conversions** (done automatically at run time, when evaluating expressions):

- Data of type `char` or `short int` will be converted to type `int` (this is called an **integer promotion**);
- If there is any value of type `float` in the expression, the other data will be converted to `float`;
- If there’s any value of type `double` in the expression, the other data will be converted to `double`;
- If there’s any value of type `long int` in the expression, the other data will be converted to `long int`.

# Precision

Since a `float` value in C is only stored in **4 bytes (32 bits)**, it has only **finite precision**, specifically, it can only guarantee that a number is **precise up to 8 digits**. 

And since a `double` value is stored in **8 bytes (64 bits)**, its precision is higher than `float`, specifically it can guarantee that a number is **precise up to around 16 digits**.

To demonstrate, we can use the code below:

```c
float x = 1111111111111111111.1111111111111111111;
double y = 1111111111111111111.1111111111111111111;

printf("x = %f\ny = %f\n", x, y);
// This will print out:
// x = 1111111131851653120.000000
// y = 1111111111111111168.000000
```

Thus if we add a large `float` value to a small `float` value, say for example `11111111000.00 + 0.00011111111`, the following will occur:

 

```c
float x = 11111111000.00 + 0.00011111111;
printf("%f", x);
// This will print out:
// 11111110656.000000
```

This is called a **numerical anomaly**, and is cause by the **finite precision** of floating point variables.

# Explicit Type Conversions

In contrast to implicit type conversions, which are automatic and done at run time, **explicit type conversions** are carried out **at the developer's request**. And it is done explicitly through the **typecast operator** (`(type) value`).

For example, in the following code, the float variable is being **explicitly converted** into a double:

```c
float x;
double y;

y = (double) x;
```

Typecast operators have the **same priority as other unary operators** (e.g. `++`, `--`), thus it has higher priority than all arithmetic and comparison operators.