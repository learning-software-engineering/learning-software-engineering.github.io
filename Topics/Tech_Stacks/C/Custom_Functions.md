# Custom Functions

# Creating a Function

So far, we have only used C’s built-in functions to do operations on data. But we can also package sections of code up to **create our own functions**, so that we can use similar blocks of code many times in our code without writing it all our manually every time.

Creating our own functions also avoids the `main()` function from becoming so large that it’s unreadable. Thus we can **extract** out some processes to be functions. This process is also called **decomposition**.

It also helps when we have many people working on a program. We can delegate people to write out functions that have **specifications** on **what it takes as input, what it does, and what it outputs (and maybe some more details)**. And then we can piece all the functions that all the developers have written together into a single working software.

Whenever a function call is encountered, with the compiler seeing something like:

```c
x = func(y, z);
process(a, b, c);
another_process();
```

It has to make sure that:

- the function to be called is **available** (i.e. the **name** represents a function);
- the **number of parameters**, and the **type of each parameter** are correct;
- the **return type** of the function is compatible with the awaiting variable;

(If any of these information mismatches, the compiler will thrown an error at compilation.)

And all these information must be provided to the compiler, either at the function’s **declaration** or its **definition**.

As an example:

```c
int add_together(int a, int b); // declaration, before main()

int main(){
    // We use the function here.
}

int add_together(int a, int b){  // definition, usually after main()
    return a + b;
}
```

The **declaration** only contains the function’s **interface**, (name, parameters, types). It’s also called the function’s **prototype**.

The **definition** contains the **full implementation** of the function (interface & function body). If we want to write the functions after the `main()` function, we MUST have a declaration before the `main()` function.

The declaration and the interface in the definition must match.

## The Return Statement

Whenever a return statement is reached in a function, the function **terminates immediately**.

Return statements are mandatory if the function has an output. And what is being returned must match the return type of the function, for example:

```c
int add_together(int a, int b){
    return a + b;
}
```

Functions of return type `void` (i.e. returns nothing) don’t need a return statement. But if a return statement is present, it just serves to **jump out of the function early**, like so:

```c
void print_on_condition(int a, int b){
    if(a < b) return;
		printf("%d %d\n", a, b);
}
```

# Scope and Global Variables

If a variable is defined within a block (wrapped in curly brackets `{…}`, be it a function, or a loop), it can only be accessed **within that same block** (and all the blocks nested inside it of course). 

For example:

```c
int add_together(int a, int b);

int main(){
    int x, y;
		scanf("%d", &x); scanf("%d", &y);
    x = add_together(x, y);
		printf("%d\n", x);
		return 0;
}

int add_together(int a, int b){
		int x = a + b;
    return x;
}
```

In the above example, the `x` in the `main` function and the `x` in the `add_together` function are different. These are both **local variables** in their respective block.

But of course, if we want to make a variable that is accessible to all functions in the source file, we can create it **outside of and before all function definitions**. This type of variable is call a **global variable**, for example:

```c
int global;

void func(){
    global += 2;
}

int main(){
    global = 1;
    func();
    return 0;  // At the end of the program, global == 3
}
```

# Parameters

Now we are going to do a bit of further exploring in regards to parameters of functions.

Say we have this function below, that is being used:

```c
int add_together(int a, int b);

int main(){
    int x, y;
		scanf("%d", &x); scanf("%d", &y);
    x = add_together(x, y);
		printf("%d\n", x);
		return 0;
}

int add_together(int a, int b){
		int x = a + b;
    return x;
}
```

Note that the parameters are **not declared within the function**, but are **passed in** when the function is called. So that in the function’s body, we can **assume that all the parameters are initialized** and contain the correct values for us to use.

The parameters `a` and `b` in the example are used in the function as if they are local variables that are already initialized, they are called the function’s **formal parameters**.

When we call our function, we have to make sure that the **number of arguments and their types** are correct, like in the example where we passed in `x` and `y`, these are the **actual parameters**.

We can also pass in literals and expressions, given that the types of their values are correct, e.g. `add_together(100, 2 * x)`. 

All the expressions will be evaluated first, and their **values** are passed in.

Before the function body is run, **the formal parameters are assigned the value of the actual parameters**.

And since **parameters behave like local variables**, we can assume that changing their value within the function block does not affect the actual values outside the function.