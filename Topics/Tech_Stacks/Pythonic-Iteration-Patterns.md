# Pythonic Iteration Patterns

Python is a language with many built-in conveniences that can greatly improve the straightforwardness of code.
In particular, some of the simple tools that it provides for iterating over things
can make code much more readable and, in some cases, efficient.

I was inspired to write about this topic due to a thing that happened while developing my team's project.
A fellow team member used an interface of mine in an inefficient and roundabout way to get some data,
when my intended way of getting the same data was a one-liner
that makes simple use of Python's dictionary iteration methods.
Switching to the intended way of getting the data dramatically improved the performance of the code.
This was a lesson in communicating interfaces properly and not making assumptions about familiarity with certain things,
but it also serves as a nice example of how knowing Python's simple iteration tools can greatly improve one's code.



## Basics `for` data types

First off, lists, tuples, and ranges are not the only data types in Python that you can iterate over.
In particular, some other basic data types that can be iterated over are strings, dictionaries, and sets.
(There are _many, many_ other standard Python types that can also be iterated over,
and you can always define your own custom iterable types, but I'd like to just focus on these three for now.)


### Strings

Iterating over a string means iterating over the individual characters:
```python
for char in 'monad':
    print(char)  # prints 'm', then 'o', then 'n', then 'a', then 'd'
```


### Dictionaries

Iterating over a dictionary means iterating over the _keys_:
```python
for key in {'a': 3, 'b': 1, 'c': 4}:
    print(key)  # prints 'a', then 'b', then 'c'

# Alternatively:
for key in {'a': 3, 'b': 1, 'c': 4}.keys():
    print(key)
```
To iterate over the _values_, use the `dict.values` method:
```python
for value in {'a': 3, 'b': 1, 'c': 4}.values():
    print(value)  # prints '3', then '1', then '4'
```
To iterate over both keys _and_ values, use the `dict.items` method:
```python
for key, value in {'a': 3, 'b': 1, 'c': 4}.items():
    print(f'{key} -> {value}')  # prints 'a -> 3', then 'b -> 1', then 'c -> 4'
```
[Starting in Python 3.7, iterating over a dict is guaranteed to produce items in insertion order.](
https://stackoverflow.com/questions/39980323/are-dictionaries-ordered-in-python-3-6)


### Sets

Lastly, you can also iterate over a set, which produces items in an unspecified order:
```python
for element in {'a', 'b', 'c'}:
    print(element)  # prints 'a', 'b', and 'c' in some order
```



## Other tools to look out `for`

As a rule of thumb, if you find yourself writing code that looks something like this:
```python
for index in indices_of_a_collection:
    do_something_with(index, collection[index])
```
...there's probably a more idiomatic way to go about things.

Here are a few of those potential ways to go about things:


### `enumerate`
```python
lst = [3, 1, 4]

# Instead of:
for i in range(len(lst)):
    print(f'{i}: {lst[i]}')

# Write:
for i, x in enumerate(lst):
    print(f'{i}: {x}')  # prints '0: 3', then '1: 1', '2: 4'
```
`enumerate` also has an optional `start` argument that allows for counting from numbers other than 0:
```python
for i, char in enumerate('abc', start=1):
    print(f'{i}: {char}')  # prints '1: a', then '2: b', then '3: c'
```


### `zip`
```python
lst_a = [1, 5, 9]
lst_b = [2, 6, 5]
lst_c = [3, 5, 8]

# Instead of:
for i in range(len(lst_a)):
    print(f'{lst_a[i]} & {lst_b[i]} & {lst_c[i]}')

# Write:
for a, b, c in zip(lst_a, lst_b, lst_c):
    print(f'{a} & {b} & {c}')  # prints '1 & 2 & 3', then '5 & 6 & 5', then '9 & 5 & 8'

# And instead of:
for i in range(len(lst_a)):
    print(f'{i}: {lst_a[i]} & {lst_b[i]} & {lst_c[i]}')

# Write:
for i, (a, b, c) in enumerate(zip(lst_a, lst_b, lst_c)):
    print(f'{i}: {a} & {b} & {c}')  # prints '0: 1 & 2 & 3', then '1: 5 & 6 & 5', then '2: 9 & 5 & 8'
```
Note that this is only equivalent if all the arguments to `zip` have the same number of items to iterate over.
By default, iteration cuts off when any of the arguments to `zip` run out of items to iterate over.
`zip` also supports an optional `strict` keyword argument to raise an error
if the given iterables do not have the same number of items to iterate over.
Also see [`zip_longest` from the `itertools` module](
https://docs.python.org/3/library/itertools.html#itertools.zip_longest).


### `reversed`
```python
s = 'defghi'

# Instead of:
for i in range(len(s) - 1, -1, -1):
    print(s[i])

# Or (this creates a copy of the string, which can be inefficient):
for char in s[::-1]:
    print(char)

# Write:
for char in reversed(s):
    print(char)  # prints 'i', then 'h', then 'g', then 'f', then 'e', then 'd'
```


### `pairwise`
```python
s = 'monoid'

# Instead of:
for i in range(len(s) - 1):
    print(f'{s[i]}|{s[i + 1]}')

# Write:
import itertools

for char_a, char_b in itertools.pairwise(s):
    print(f'{char_a}|{char_b}')  # prints 'm|o', then 'o|n', then 'n|o', then 'o|i', then 'i|d'
```
In general, [the `itertools` module](https://docs.python.org/3/library/itertools.html)
provides quite a few functions that can be helpful when trying to iterate over things.



## Already done `for` you

Python doesn't just have tools to make it nicer to write for loops and comprehensions --
it also has a variety of functions that make it so that you don't _need_ to write those.


### Constructors: comprehension shortcuts

First off, instead of writing `[x for x in iterable]` or `{x for x in iterable}`,
you can simply write `list(iterable)` and `set(iterable)`. Similar functionality also exists for `tuple` and `dict`.


### Grabbag of convenient functions

Python comes with functions to compute the sum, product, maximum, or minimum of any iterable:
`sum`, `prod` from the `math` module, `max`, and `min`.
If you want to check if a criterion is satisfied for every item in an iterable, use the `all` function;
for at least one item in an iterable, the `any` function.


### `str.join`

I've seen some variation of the following code from more than one person in relation to my team's project:
```python
result = ''

for s in ['a', 'monad', 'is', 'a', 'monoid']:
    result += s + ' | '

# remove the trailing ' | '
# a better way to accomplish this would be the str.removesuffix method
result = result[:-3]

# result == 'a | monad | is | a | monoid'
```
Instead of writing that, simply write:
```python
result = ' | '.join(['a', 'monad', 'is', 'a', 'monoid'])
```


### Removing the square brackets

When using all of these functions, instead of giving a list comprehension as an argument, consider using a
[generator comprehension](https://stackoverflow.com/questions/364802/how-does-a-generator-comprehension-works)
instead -- instead of generating an entire list up front,
items are computed on demand, making things more memory-efficient.

For example:
```python
lst = [3, 1, 4, 1, 5, 9]

# Instead of:
sum([x * 2 for x in lst])

# Simply write:
sum(x * 2 for x in lst)
```



## Closing thoughts

As you can see, there are a lot of nice little conveniences that Python provides to make one's life a little nicer.
Not all of the things showcased here are even new concepts that need time and effort to understand --
many are simply little units of functionality that can still have an impact on the readability of your code.

My knowledge of these tools was built over time as I programmed more and more in Python.
However, there are ways to stumble upon these sooner rather than later.
The way I'd like to highlight is: whenever there's a problem to solve, do some research into the idiomatic solutions.
A solution using previously unknown tools might be far more elegant
than the one you think up yourself using only what's known to you.
