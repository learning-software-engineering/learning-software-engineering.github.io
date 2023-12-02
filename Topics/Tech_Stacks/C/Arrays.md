# Arrays

# Array Declaration

Oftentimes we have to store hundreds or even thousands of values at the same time. Of course defining one variable for each of them would be extremely inconvenient. Thus C provides **multi-value variables** to store many values with a single variable (name reference).

One type of such multi-value variables are called **arrays**, where we declare a variable that can store a finite amount of values. To declare an array, for example:

```c
int numbers[4];
```

We now have an array that can hold 4 numbers.

Each number in an array is given an **index** so that we can access it (**from 0 to 3 in this case**), like so:

```c
numbers[0] = 1;
numbers[1] = 12;
numbers[2] = 123;
numbers[3] = 1234;

int i = 1;
int x = numbers[i + 1];  // Here we are accessing numbers[2]
```

Note that if an array can contain $n$ numbers, its range of valid indexes would be $\mathbb{Z}\cap[0,~n-1]$.

Also note that all elements in an array **have the same type**. 

Arrays can contain all primitive types, for example:

```c
float arrayOfFloats[10];
double arrayOfDoubles[100];

char str[300];  // An array of characters is called a "string".
```

**Side Note**: To **input a string**, say we want to input into `char str[20];`, we should use `scanf(”%s”, str);` and **NOT** `scanf(”%s”, &str);`. 

This is because `str` is **already a pointer** to the first element of the array. We don’t need to use the `&` operator (or “address of” operator) to make it into an address.

# Array Initialization

We can initialize our array when we declare it, like so:

```c
int vec[5] = {1, 2, 3, 4, 5};
```

This is fairly intuitive in that the array will contain values like so:

| Element | vec[0] | vec[1] | vec[2] | vec[3] | vec[4] |
| --- | --- | --- | --- | --- | --- |
| Value | 1 | 2 | 3 | 4 | 5 |

We can also initialize an array like this without giving it a size, like so:

```c
int vec[] = {1, 2, 3, 4, 5, 6, 7};
```

In this case the array will have a **length** of 7, which is **inferred** from its initialization.

If we hard-code the length of the array, and give **fewer elements than the length of the array**, the values will be filled from index `0`, and the remaining spaces are filled with `0`:

```c
int vec[5] = {1, 2};
```

In this case the array will contain:

| Element | vec[0] | vec[1] | vec[2] | vec[3] | vec[4] |
| --- | --- | --- | --- | --- | --- |
| Value | 1 | 2 | 0 | 0 | 0 |

Using this feature, we can **initialize an array to contain all zeros** by doing so:

```c
int vec[10] = {0};
```

However, giving more elements than the length of the array will result in an error.

# The `Sizeof` Function (Preview)

We can use the `sizeof()` function to get **how many bytes** a literal, a variable, or a value of a certain type takes up in memory.

Note that `sizeof` is a **keyword**, it is also considered a **unary operator**.

```c
int i;
i = sizeof(char);  // i is now 1, since a char takes up 1 byte in memory
i = sizeof(int);  // is is now 4, since an int takes up 4 bytes in memory

int vec[20];
i = sizeof(vec[0]);  // vec[0] is an int, thus i is now 4
i = sizeof(vec);  // i is now 80, since there are 20 ints in vec[]
i = sizeof(vec) / sizeof(vec[0]);  // i == 80 / 4 == 20
// Notice how this is equal to the length of the array, which is 20.

double arr[5];
i = sizeof(arr[0]);  // arr[0] is a double, thus i is now 8
i = sizeof(arr);  // i is now 40, since there are 5 floats in arr[]
i = sizeof(arr) / sizeof(arr[0]);  // i == 40 / 8 == 5
// Notice how this is also equal to the length of the array, which is 5.
```

Thus to get the **length of an array** (e.g. `arr`), we can just do `sizeof(arr) / sizeof(arr[0])`.