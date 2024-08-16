---
title: "Python 3.13 - New Features & Deprecations"
datePublished: Fri Aug 16 2024 01:24:48 GMT+0000 (Coordinated Universal Time)
cuid: clzw11d8q00000akzbjzv38dj
slug: python-313-new-features-deprecations
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723555843235/a2ef4e78-aea9-4318-ab42-de2b71c4ca30.png
tags: python, features, python3, versioning, update, python-beginner, python-projects, newrelease, deprecation, python-313, 313, 312, python-312

---

We introduced several cool typing and interactive interpreting features in Python 3.12. I discussed all of them here:

%[https://blog.imsadra.me/python312-is-happening] 

Before we go ahead, [this](https://docs.python.org/3.13/whatsnew/3.13.html) is the full patch note about this new release.  
*The biggest change* introduced in the early 3.13 patch notes is that the Global Interpreter Lock (GIL) is now droppable, and you can disable it in certain cases!

### 1\. GIL & JIT

CPython will run with the GIL disabled when configured using the `--disable-gil` option at build time. To check if the current interpreter is configured with `--disable-gil`, run the following command:

```bash
... -c "import sys; sysconfig.get_config_var('Py_GIL_DISABLED')"
```

What's more, there will be an experimental version of a just-in-time compiler (JIT) that is disabled by default. You can use as easy as passing an option or by creating your own specific build of CPython 3.13.

It's been quite a while since PyPy introduced its high-performance garbage collector along a JIT compiler. These features have shown great promises.

All of this leads us to realize that CPython 3.14 will be a significant performance improvement, not only for users but also for all frameworks built on top of Python.

Now, without further ado, let's talk about some of the changes.

### 2\. A Better Interactive Interpreter

The new interpreter provides more detailed error messages and tracebacks, helping you catch bugs and issues even faster. They are more colorful. You can disable this behavior by setting `PYTHON_COLORS` and `NO_COLOR` environment variables.

```bash
PYTHON_COLORS=0 python3.13 main.py
```

If you write a script inside a `.py` file with a file name similar to one of the standard library names, such as `random`, you would typically get a circular import error.

```bash
$ python3.12 random.py
Traceback (most recent call last):
  File "/home/random.py", line 1, in <module>
    import random; print(random.randint(5))
    ^^^^^^^^^^^^^
  File "/home/random.py", line 1, in <module>
    import random; print(random.randint(5))
                         ^^^^^^^^^^^^^^
AttributeError: partially initialized module 'random' has no attribute 'randint' (most likely due to a circular import)
```

But now, you get a more precise exception.

```bash
$ python3.13 random.py
Traceback (most recent call last):
  File "/home/random.py", line 1, in <module>
    import random; print(random.randint(5))
    ^^^^^^^^^^^^^
  File "/home/random.py", line 1, in <module>
    import random; print(random.randint(5))
                        ^^^^^^^^^^^^^^
AttributeError: module 'random' has no attribute 'randint' (consider renaming '/home/random.py' since it has the same name as the standard library module named 'random' and the import system gives it precedence)
```

The same rule applies to third-party packages.

If you call a function with an incorrect parameter name, the interpreter will guess what you meant and suggest the correct name.

```python-repl
>>> "better error messages!".split(max_split=1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
    "better error messages!".split(max_split=1)
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~^^^^^^^^^^^^^
TypeError: split() got an unexpected keyword argument 'max_split'. Did you mean 'maxsplit'?
```

### 3\. No More Functions in REPL

Now, you can call `help()`, `exit()`, and `quit()` commands without the parentheses.

### 4\. Deprecation Warnings

The `warning` standard library is used to alert developers about deprecations, future removals, and similar issues. In Python 3.13, there is a `@deprecation` decorator that allows you to add deprecation warning messages to any of your components.

```python
from warnings import deprecated

@deprecated("Use PayPalPaymentProcessor instead")
class PaymentProcessor:
    ...

class PayPalPaymentProcessor:
    ...
```

Once a user tries to use any of the deprecated components, a warning will appear in the prompt. For functions, that happens on calls; for classes, on instantiation and on creation of subclasses.

### 5\. New Typing Features

We all know that Python itself doesn't enforce types. You can define a function that takes a parameter `name: str` and still pass an integer to that function. So, working on the `typing` module means improving static type checkers even more, and you should use them.

#### `ReadOnly` type

In Python 3.13, we have `typing.ReadOnly`, which can be applied to items of a `TypedDict` to make them read-only. If you try to change the item value, you can, but your type checker should raise an error.

```python
class Student(TypedDict):
   idn: ReadOnly[str]
   gpa: float

def modify_student(s: Student) -> None:
   s["gpa"] = 4.0  # allowed
   s["idn"] = "24315"  # typechecker error
```

#### `TypeIs` type

This type is assigned to the return value of callables (like functions) that return booleans, indicating whether a variable is an object of a specific type or not.

Consider the following simple function.

```python
def is_student(s: Student):
    return isinstance(s, Student)
```

Similar to `typing.List` and `typing.Union`, it accepts any generic or custom types, so you should use it like `TypeIs[SomeType]`. Now, let's add a type hint to the return value of that function using `TypeIs`.

```python
from typing import TypeIs

def is_student(s: Student) -> TypeIs[Student]:
    return isinstance(s, Student)
```

Now, if `is_student(val)` returns `True`, the type checker knows that `val` is of type `Student`. If it returns `False`, the type checker knows that `val` is not of type `Student`.

Generally speaking, you should use it when..

* The function returns a boolean value.
    
* The function checks an object's type using `isinstance()` or any other mechanism.
    

### 6\. Official Support for iOS & Android

Python 3.13 is going to have a separate official release for the iOS platform. The team is working on the Android one as well, but not planned for the 3.13 release.

### 7\. Version Support

* Python 3.9 - 3.12 have one and a half years of full support, followed by three and a half years of security fixes.
    
* Python 3.13 and later have two years of full support, followed by three years of security fixes.
    

### Python 3.14, 3.15, and 3.16 Expected Removals

We're going to see many removals as some components in the standard library are deprecated. Here, I've listed the libraries most affected by these future component removals.

* `argparse`
    
* `asyncio`
    
* `pathlib`
    
* `importlib`
    

### Conclusion

GIL has been both a blessing and a mess, in my opinion. It's great to see the community moving forward, considering alternatives and solutions for allowing users to optionally use the components. I'm confident that the JIT compiler will make Python even faster in the next few releases. There will be significant performance improvements in high-scale web frameworks like Django. I hope this article has given you a clear insight into the upcoming Python 3.13 release.