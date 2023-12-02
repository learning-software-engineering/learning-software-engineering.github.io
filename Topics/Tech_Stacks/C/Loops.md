# Loops

If we wish to do the same thing, or similar things for many times, we can use **loops** to achieve that.

# While Loop

A `while` loop takes the form:

```c
while(bool_expression){
    ...  // Loop body
}
```

The **loop body** is the statements inside the loop. 

In a while loop, as long as `bool_expression` is true, the loop body will keep running, once cycle after another.

If `bool_expression` is not true before the loop begins, the loop body is not run, and the loop is skipped.

If `bool_expression` is always true, then the loop body will run infinite times, resulting in an **infinite loop**. We don’t want this to happen.

Thus `bool_expression` has to be closely related to what the loop is doing, in order to make the loop body run **a finite number of times**.

# Do-While Loop

A `do … while` loop takes the form:

```c
do{
    ...  // Loop body
}while(bool_expression);
```

This is similar to the `while` loop, but the loop body will get run **at least once**. And then the loop condition is checked to see if there should be another cycle, etc.

# For Loop

We often find ourselves wanting to run a piece of code **a set number of times**. We can achieve this using a `while` loop by doing so: 

```c
int n = 100;  // Say for example, we want to run something 100 times.
int i = 0;  // INITIALIZING the COUNTER

while(i < n){  // CONDITION CHECK
    ...  // Loop body
    i++; // MODIFYING the COUNTER
}
```

Now notice that since this type of loop will always have these 3 components: 

- Initialization of the **counter** (the counter is also called the **control variable**)
- Checking the condition (**before** running the loop body)
- Modifying the counter (**after** running the loop body)

We can create a shorthand for this type of loop, the `for` loop:

```c
int n = 100;

for(int i = 0; i < n; i++){  // Initialization ; Condition ; Modification
    ...  // Loop body
}
```

(We can also omit any of the three components, in that case the compiler will assume that there’s a 1 there, i.e. the condition is presumed to be met.)

# Break and Continue

So far, the body of the loop is an **indivisible** and **inseparable** sequence of instructions that are performed completely at every turn of the loop. However, sometimes:

- It appears that it’s **unnecessary to continue the loop as a whole**, and we should **refrain from executing the loop’s body and go further**.
- It appears that we need to **start the condition testing** without completing the execution of the current turn.

## Break

The `break;` statement **exits the loop immediately** and unconditionally ends the loop’s operation. The program will continue with the instructions below the loop.

## Continue

The `continue;` statement behaves as if the program has **suddenly reached the end of the body (skips the rest of the instructions of the current loop body)**. 

If it’s a `for` loop, then the control variable is also modified before the next condition testing.