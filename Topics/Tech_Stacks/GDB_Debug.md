# Introduction how to debug by GDB

## Table of contents

#### [What is GDB]
#### [What can do by GDB]
#### [How to use GDB]


## What is GDB?
GDB (GNU Debugger) is a powerful open-source debugger commonly used in the field of computer science and software development, especially in the context of programming and debugging. 

It is a command-line tool that allows developers to inspect and debug programs written in various programming languages, including C, C++, and even some other languages.

Source: [GDB: The GNU Project Debugger](https://www.sourceware.org/gdb/)


## What can do by GDB?

1. **Start Your Program:**
    GDB can start your program, specifying anything that might affect its behavior. This allows you to control the program's execution from the beginning.

2. **Stop on Specified Conditions:**
    You can set breakpoints in your code to make your program stop at specific conditions or events. Breakpoints can be set at particular line numbers, function names, or even based on variable values.

2. **Examine Program State:**
    While your program is paused at a breakpoint, GDB allows you to examine what has happened. You can inspect the values of variables, explore the call stack with a backtrace, and view the source code surrounding the current point of execution.

3. **Modify Program State:**
    GDB enables you to change things in your program, which is particularly useful for experimenting with bug fixes. You can modify variable values, continue program execution to observe different outcomes, and learn about multiple issues within your code.

These features make GDB an essential tool for understanding and debugging programs, whether they are executing on the same machine as GDB (native), on another machine (remote), or on a simulator. GDB is compatible with most popular UNIX and Microsoft Windows variants, as well as macOS.



## How to use GDB?

1. **Install GDB:**
    1. [Linux]: 
        Debian-based systems like Ubuntu:`sudo apt-get install gdb`

        Red Hat-based systems like Fedora: `sudo dnf install gdb`

    2. [macOS]: `brew install gdb`

2. **Compile Your Program:**
    Before you can debug a program with GDB, you need to compile it with debugging symbols enabled. This ensures that GDB can associate source code lines with machine code instructions.

    `gcc -g -o <<program>> <<program.c>>`

3. **Start GDB:**
    `gdb program` and you will see:

    `GNU gdb (Ubuntu 12.1-0ubuntu1~22.04) 12.1
    Copyright (C) 2022 Free Software Foundation, Inc.
    License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
    This is free software: you are free to change and redistribute it.
    There is NO WARRANTY, to the extent permitted by law.
    Type "show copying" and "show warranty" for details.
    This GDB was configured as "x86_64-linux-gnu".
    Type "show configuration" for configuration details.
    For bug reporting instructions, please see:
    --Type <RET> for more, q to quit, c to continue without paging--`

    and you can type `q` to quit and `c` to continue.

4. **Set Breakpoints:**
    GDB provides various ways to set breakpoints, allowing you to control where your program stops during debugging. 

    1. [Line Number Breakpoint]: 
        This is the most common type of breakpoint. It stops program execution at a specific line of source code.
        
        Example: `break 10`
        
    2. [Function Name Breakpoint]: 
        This breakpoint stops the program when it enters or exits a specified function.
        
        Example: `break my_function`

    3. [File and Line Number Breakpoint]: 
        This breakpoint stops the program when it enters or exits a specified function.
        
        Example: `break <<myfile.c>>:20`

    4. [Address Breakpoint]: 
        You can set a breakpoint at a specific memory address, which is useful for debugging assembly code or low-level programming.
        
        Example: `break *0x0804835c`

    5. [Condition Breakpoint]: 
         This type of breakpoint stops the program only if a specified condition is true when the breakpoint is hit.
         
         Example: To set a breakpoint at line 15 and break only if the variable `x` is greater than 10, use `break 15 if x > 10`.

5. **Run Your Program:**
    `run`

6. **Interact with Your Program:**
    1. `step`: Execute the current line and stop at the first possible occasion, even if it's inside a function.

    2. `next`: Execute the current line and stop at the next line in the same function.

    3. `continue`: Resume program execution until the next breakpoint is hit.

    4.`print`: Display the value of a variable or expression.

    5.`backtrace`: Display a backtrace of the function call stack.

7. **Exit GDB:**
    `quit`

