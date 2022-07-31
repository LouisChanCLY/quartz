---
tag: medium-idea
date: 2022-07-24
---

## Metadata
- Association:
- Domain: [[Domain Root - Python]]

## Python Trick How to call function by its name

Welcome to a series of short posts each with handy Python tricks that can help you up your game. In this blog, we will look into how to call a function by its name.

## Calling Functions

Say you have a function `def f(): pass`.

Can you call the function using just `"f"`?

Or in a more complicated case, if you have `f1()`, `f2()`, and `f3()`, and users will be choosing which function by typing in a string, how can that be done?

## Solution 1: Locals & Globals

Before we dive into `locals` and `globals`, it is important to have some understanding on what [[Namespace]] is. In a Python runtime, all the defined object (class, function, variable, etc.) are mapped and stored in a dictionary, a.k.a. the namespace.

`locals()` returns the namespace at a local level - say local variables defined in a function, which will then be part of the [[Local Namespace]] within the function.

`globals()` returns the namespace at a global level - say modules imported globally or objects defined globally, which will then be part of the [[Global Namespace]], be it within or outside the function.

Let's say there is a function named `my_function`. 

```python
def my_function(a, b, c):
		pass
```

To call the function with `"my_function"` using `locals` and `globals`:

```python
s = "my_function"

# calling the function from local namespace
function = locals()[s]
function(a=1, b=2, c=3)

# calling the function from global namespace
function = globals()[s]
function(a=1, b=2, c=3)
```

This method with globals/locals is good if the method you need to call is defined in the same namespace you are calling from.

dictionary that represents the current symbol table of the given source code
difference in namespace

https://docs.python.org/3/library/functions.html#locals
return dictionary of local namespace i.e. with local objects

```python
locals()["myfunction"]()
```

https://docs.python.org/3/library/functions.html#globals
return dictionary of global namespace i.e. with global objects

```python
globals()["myfunction"]()
```

## Solution 2: Eval

The next option is the well-known `eval`, a built-in python function that evaluates an arbitrary string expression/compiled code and execute if it is a legal Python expression.

```python
eval(expression[, globals[, locals]])
```

To use `eval`, you only need up to three arguments:
- Expression: the string expression/compiled code that you wan it to evaluate
- Globals: optional dictionary that provides a global namespace to `eval`
- Locals: optional dictionary that provides a local namespace to `eval`

> When globals and locals are provided, they are the namespaces of which `eval` will run based on. Otherwise, `eval` will use the global and local namespaces that your current code is based on 

```python
s = "my_function"

# calling the function using eval
function = eval(s)
function(a=1, b=2, c=3)

# you can also run the function directly
result = eval(s)(a=1, b=2, c=3)
```

## Solution 3: Method Caller

Another method (no pun intended) for doing so is in one of Python's standard library - `operator.methodcaller`. Unlike the above options, `methodcaller` fetch you a callable from an object provided. Hence, the following would not work:

```python
from operator import methodcaller
bar = methodcaller("myfunction")
bar()
```

Instead, the callable needs to be part of an object:

```python
from operator import methodcaller
foo = "bar"

# upper is a method of a string object
foo_method = methodcaller("upper")
foo_method(foo)

>>> 'BAR'
```

Another key difference between `methodcaller` and other options is that any arguments would need to be provided in advance. For example:

```python
from operator import methodcaller
import random

# This doesn't work
foo_method = methodcaller("randint")
foo_method(random)

>>> TypeError: randint() missing 2 required positional arguments: 'a' and 'b'

# This doesn't work either
foo_method = methodcaller("randint")
foo_method(random, a=1, b=2)

>>> TypeError: methodcaller() takes no keyword arguments

# This works!
foo_method = methodcaller("randint", a=1, b=2)
foo_method(random)

>>> 1
```

Therefore, to use `methodcaller`, you would need to first be mindful of:
- the location of the method (e.g. which module/class is the method under)
- whether arguments are required to use that method

## Solution 4: Get Attribute

Just like `operator.methodcaller`, `getattr` is another option that requires prior knowledge of where the method reside. That being said, there are two major differences between the two options:
1. `getattr` does not restrict to getting a callable. When using it, do be mindful of whether the object returned is callable or not.
2. `getattr` allows you to pass arguments to the returned method while `methodcaller` requires you to provide it in advance.

```python
import random
bar = getattr(random, 'randint')
result = bar(1, 2)
>>> 2
```

## Closing Thoughts

Just because you can do it doesn't mean that you should do it.

Allowing users of a script to dictate the behaviour it using a user-provided string can lead to some undesirable security loophole. Some other infamous security loopholes stemmed from treating unparameterised data as code includes XSS and SQL injection. That being said, Python itself being an interpreted language means there are lower level changes that one can make to create even bigger vulnerability.

In short, in this tutorial, we have walked through four ways that you can call a method using a string. As a quick revision, here is a table that summarises their behaviours:

| Method                | Requires knowledge of location of method      | Return type | Ability to set argument in advance | Ability to set argument after returning |
| --------------------- | --------------------------------------------- | ----------- | ---------------------------------- | --------------------------------------- |
| `locals` or `globals` | Not as long as the method is in the namespace | Any         | No                                 | Yes                                     |
| `eval`                | Not as long as the method is in the namespace | Any         | Yes (as arbitrary string)          | Yes                                     |
| `methodcaller`        | Yes                                           | Callable    | Yes                                | No                                      |
| `getattr`             | Yes                                           | Any         | No                                 | Yes                                     | 

That’s about it for this blog post! I hope you have found this useful. If you have enjoyed the read, don't forget to leave some claps or even join Medium using my referral link (at **NO** additional cost to you).

https://louis-chan.medium.com/membership

If you are interested in other Python tricks, I have put together a list of these short blogs for you:

- [Python Tricks: Unpacking Iterables](https://pub.towardsai.net/python-tricks-unpacking-iterables-a1acf8a658a6)
- [Python Tricks: Flattening Lists](https://towardsdatascience.com/python-tricks-flattening-lists-75aeb1102337)
- [Python Tricks: How to Check Table Merging with Pandas](https://towardsdatascience.com/python-tricks-how-to-check-table-merging-with-pandas-cae6b9b1d540)
- [Python Tricks: Simplifying If Statements & Boolean Evaluation](https://towardsdatascience.com/python-tricks-simplifying-if-statements-boolean-evaluation-4e10cc7c1e71)
- [Python Tricks: Check Multiple Variables against Single Value](https://towardsdatascience.com/python-tricks-check-multiple-variables-against-single-value-18a4d98d79f4)

If you would like to read more about how to apply machine learning to trading & investing, here are some other posts that may be of interest:

- [Genetic Algorithm for Trading Strategy Optimization in Python](https://pub.towardsai.net/genetic-algorithm-for-trading-strategy-optimization-in-python-614eb660990d)
- [Genetic Algorithm — Stop Overfitting Trading Strategies](https://medium.com/towards-artificial-intelligence/genetic-algorithm-stop-overfitting-trading-strategies-5df671d5cde1)
- [ANN Recommendation System for Stock Selection](https://pub.towardsai.net/ann-recommendation-system-for-stock-selection-c9751a3a0520)

https://www.linkedin.com/in/louis-chan-b55b9287