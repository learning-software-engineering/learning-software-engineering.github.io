# Static Type Checking in Python

## Typing Overview

Types in a programming language define the categories of objects which helps it define the operations that can be done on or with the objects, and what sort of objects can be defined by the user.

### Type Checking

Type checking is the process of verifying and enforcing constraints of types defined in a programming language. It can perform semantics checks based on language definition as outlined as follows:
```java
1 + "1"  // checks if the type of value on lhs can be performed in the add operation with the type of value on rhs

int i = "s"  // checks if the value of the assignment matches the type of the variable

int func() {
    return "s"  // checks if the type of return value matches the one defined by the function
}
```
Static type checking allows type-related bugs to be found within the program before it is run, which can greatly reduce the chance of running into type-related errors at run time.

### Dynamically Typed Languages

There are mainly two type-systems that exist in most modern-day programming languages. The first is a dynamically typed programming language, like Python and JavaScript. These languages are usually interpreted where the interpreter only performs type checking as the code runs, thus also allowing the type of variable to change over its lifetime. For example:
```python
>>> if False:
...     1 + "two"  # This line never runs, so no TypeError is raised
... else:
...     1 + 2
...
3

>>> 1 + "two"  # Now this is type-checked, and a TypeError is raised
TypeError: unsupported operand type(s) for +: 'int' and 'str'

>>> a = 1
>>> a + 2
3
>>> a = "one"  
>>> a + "two"  # As long as the type of value in the variable at the time of execution matches the semantics of the operator, no type error will be raised
'onetwo'
```

### Statically Typed Languages

Statically typed languages are the opposite of dynamically typed languages, like C++ and Java. These languages require static type checking to be performed without running the program, and they usually require the user to define the type of their variables, functions, etc., though many modern-day statically typed languages can infer the type from the assigned value when performing static type checking.

In the next section, we will see how we can add static typing to Python to make it more like a statically typed programming language

## Typing in Python

### Type Hints

Introduced in [PEP-484](https://peps.python.org/pep-0484/), Python added type hints to the language thus making static type checking in Python possible. With this change, we can now define types for functions and variables in Python. In older versions of Python, a function that takes in a string and an integer as parameter and returns a boolean might have the following signature:
```python
def func(a, b):
    pass
```
Without any docstring or context, the types of this function are completely unknown to anyone who sees this function signature. But since Python3.5, we can now define the function as follows:
```python
def func(a: str, b: int) -> bool:
    ...
```
Now it is clear that the first argument is a string, the second argument is an integer, and the function returns a boolean.

To see more detailed usage of Python type hints, visit official Python documentation: https://docs.python.org/3/library/typing.html

### Mypy

Even though we have now defined types for the function, we still have the issue of type checking, mainly that Python on its own does not perform any static type checking, so we can pass in values of different type than the one annotated in the function signature and the code might still run just fine:
```python
# demo.py

def func(a: str, b: int) -> bool:
    return True

    func("blah", 1)  # will run fine
    func("blah", "blah")  # will also run fine as long as the operations performed using <a> and <b> are valid
```
This is where [Mypy](https://mypy-lang.org/) comes in. Mypy is an open-sourced static type-checking tool for Python that utilizes the type hints defined in the code by the users.

With the same piece of code above, we can run it through Mypy for static type checking:
```shell
$ mypy demo.py
demo.py:7: error: Argument 2 to "func" has incompatible type "str"; expected "int"  [arg-type]
```
Based on the type hints, Mypy is able to inform us that we are using the wrong type for the second function call.

Mypy documentation for more detailed usage and configuration:
- https://mypy.readthedocs.io/en/stable/
- https://mypy-lang.org/examples.html

## Pros and Cons

There are several advantages to using type hints and Mypy in Python: 
1. Eliminates type errors at runtime: this one is pretty obvious and self-explanatory. If all the code had type hints and adhered to the type rules, there simply wouldn't be any type errors occurring at runtime
2. Documents the code: instead of specifying the type in docstring, this is a much more elegant way of doing it. It also works better with modern automatic documentation generators such as Sphinx. The extra documentation also improves IDEs and linters as it can give you better error detection and suggestions (especially on more complex code structures) while coding which improves productivity.
3. Enables cleaner code: despite all the flexibility of dynamic types, it's often bad practice to use many of its features such as re-assigning values of different types as the code can become very hard to understand and unpredictable. Type hints and type-checking enforce you to write code in a more systematic way.

There are also several cons associated with using type hints and Mypy in Python:
1. Takes time for developers to add: types are complicated, especially nested ones, thus it often takes developers extra time to add these in. On existing projects, it's even more effort as you may discover code that may need to be changed due to the new type-check enforcement.
2. Type hints add overhead to program runtime: type hints aren't native to the Python interpreter so the typing module needs to be imported in for many features to work (though this has improved significantly in recent versions of Python such as 3.11 and 3.12, supporting more native Python types to be used in type hints). This adds overhead to the program start-up time.
3. Mypy is a 3rd-party tool: being a 3rd-party tool means it's not run at the same time as the python executable, so developers might forget to run it and it takes slightly more effort to add into automated pipelines.
