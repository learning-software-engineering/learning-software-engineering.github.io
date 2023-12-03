# Basic COBOL Syntax Guide

## Variable Declaration

In COBOL, variables are declared in the `DATA DIVISION` section of the program.
A typical declaration specifies the variable's level number, name, and type.

```cobol
DATA DIVISION.
WORKING-STORAGE SECTION.
01 NUM-A PIC 9(3).     -- Declares an integer variable with 3 digits
01 NUM-B PIC 9(3).
01 RESULT PIC 9(4).
```

## Basic Math Operations
COBOL supports basic arithmetic operations like addition, subtraction, multiplication, and division.
These operations are performed using the COMPUTE statement.

```cobol
COMPUTE RESULT = NUM-A + NUM-B.    -- Addition
COMPUTE RESULT = NUM-A - NUM-B.    -- Subtraction
COMPUTE RESULT = NUM-A * NUM-B.    -- Multiplication
COMPUTE RESULT = NUM-A / NUM-B.    -- Division
```

## Function Calls
In COBOL, a function call is made using the CALL statement,
where you specify the function name and pass any required parameters.

```cobol
CALL 'FUNCTION-NAME' USING PARAM1 PARAM2.
```

## Loops
Loops in COBOL can be implemented using the PERFORM statement.
The PERFORM ... TIMES loop executes a set number of times,
whereas PERFORM UNTIL executes until a condition is met.

## Fixed Number of Iterations
```cobol
PERFORM VARYING COUNTER FROM 1 BY 1 UNTIL COUNTER > 10
    -- Loop body goes here
END-PERFORM.
```

## Condition-Based Loop

```cobol
PERFORM UNTIL CONDITION
    -- Loop body goes here
END-PERFORM.
```

# Coding examples
## Displaying "Hello World" in COBOL

To display the phrase "Hello World" in a COBOL program, 
you can use the `DISPLAY` statement within the `PROCEDURE DIVISION` of your COBOL code. 
Just like print functions in many languages.

```cobol
000100 IDENTIFICATION DIVISION.
000200 PROGRAM-ID. HELLO-WORLD.
000300 PROCEDURE DIVISION.
000400    DISPLAY "Hello World".
000500 STOP RUN.
```

## Basic Arithmetic in COBOL

Performing arithmetic in COBOL involves using the `COMPUTE` statement within the `PROCEDURE DIVISION`.
The example below demonstrates how to add two numbers and display the result:

```cobol
000100 IDENTIFICATION DIVISION.
000200 PROGRAM-ID. ADDITION-EXAMPLE.
000300 DATA DIVISION.
000400 WORKING-STORAGE SECTION.
000500 01 NUM-A PIC 9(4) VALUE 1234.
000600 01 NUM-B PIC 9(4) VALUE 5678.
000700 01 RESULT PIC 9(5).
000800
000900 PROCEDURE DIVISION.
001000    COMPUTE RESULT = NUM-A + NUM-B.
001100    DISPLAY "The result of adding " NUM-A " and " NUM-B " is: " RESULT.
001200 STOP RUN.
```

## Understanding the Initial Lines of a COBOL Program

The first several lines of a COBOL program are part of the program's structure,
just like include <stdio.h> in C or import numpy in python,
providing essential information about the program itself.


1. **IDENTIFICATION DIVISION**:
This is also a mandatory entry which uniquely identifies the program within a system or environment.
```cobol
000100 IDENTIFICATION DIVISION.
```
There are alternatives including INSTALLATION, DATE-WRITTEN, DATE-COMPILED, SECURITY, etc. 
These are optional and provide additional metadata about the program.
```cobol
000200 PROGRAM-ID. YOUR-PROGRAM-NAME.
```

```cobol
000300 AUTHOR. YOUR-NAME.           -- Optional
```

The IDENTIFICATION DIVISION tells the computer where the program starts, which is mandatory.
and the PROGRAM-ID names the program.
```cobol
IDENTIFICATION DIVISION.            -- Marks the start of the identification section.
PROGRAM-ID. YOUR-PROGRAM-NAME.      -- Declares the program's name for identification.
AUTHOR. YOUR-NAME.                  -- Optional
```

You may ask: Why every line starts with a set of numbers like 000100, 000200, 000300.
These numbers aren't required; they're mostly there to help find and organize the code,
or for use in old-fashioned computer systems where they needed these numbers to
work with programs on punch cards or to keep track of the line order.
PROGRAM-ID: This line follows within the IDENTIFICATION DIVISION and
is used to declare the name of the program.
