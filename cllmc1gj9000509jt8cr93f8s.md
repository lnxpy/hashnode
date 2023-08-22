---
title: "Python3.12 is Happening..!"
datePublished: Tue Aug 22 2023 13:19:14 GMT+0000 (Coordinated Universal Time)
cuid: cllmc1gj9000509jt8cr93f8s
slug: python312-is-happening
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692704680328/48e40195-d51f-4f46-9df5-9cecf315d818.png
tags: news, python, python3, update, release-notes

---

In this quick overview, we're going to talk about Python 3.12 and its new amazing features as well as my personal thoughts on each upgrade/downgrade. My thoughts are specified with the "IMO" (In My Opinion) keyword at the beginning of the quotes.

### Nested F-Strings

In Python 3.12, you can have nested f-string phrases. Check the following example.

```python
phrase = f"Hello {f"{name}"}"
# Hello Sadra
```

> IMO: It seems to be quite hard in term of understanding a nested f-string phrase as it might not be as practical as the simple f-strings. I would personally regret using this new feature.

### Multiline F-Strings

One cool feature that's been brought to the new 3.12 version is that you can have multiline f-strings.

```python
phrase = f"Hello {
    name # User.name
}"
# Hello Sadra
```

> IMO: This is a handy one. As you can see, you can expand your f-strings as well as document your multiline them via comments. That's amazing!

### Tokenization is Re-written in C

Since Python 3.11, the tokenizer module has been in Python analyzing your Python lexical and keywords. From now on, due to the new nested and multiline f-strings, this module has been updated and re-written in C and it's almost 40% faster than before. With this huge improvement, all the linting and formatting tools that make use of this module can get a huge performance improvement over this update.

> IMO: Now I can run my CI worklfows way faster!!

### Distutils is Depricated

There's always been a struggle among the Python community members about `setuptools` against `distutils` and the reason that everyone prefers the `setuptools` (which is a fork of `distutils`) over the official `distutils`. That's actually because `setuptools` is better with lots of more features and functionalities. That's why they decided to remove the `distutils` standard library and depreciate that.

What's more, `pip` actually uses `setuptools` for building the distributions. If you make a `venv` with `python<=3.11` and `pip<=22.1` you'll see that the `setuptools` is already installed there.

```bash
$ pip list
Package    Version
---------- -------
pip        23.2.1
setuptools 68.0.0    <--
wheel      0.41.1
```

The `setuptools` package is not a standard library. It just uses `distutils`. Since `distutils` is no more available and `pip>=22.1` is not dependent on `setuptools`, we'll never have a distributing tool inside a freshly installed Python environment.

The `setuptools` package has dropped its dependency on the `virtualenv` package as well. It means even if you install the `setuptools`, you won't be able to create a virtual environment or even run the following command.

```bash
$ python -m venv venv
# ERROR: venv module is not found.
```

The `distutils` package has become another whole third-party package. In order to have access to both `virtualenv` and `setuptools`, you have to install them separately.

> IMO: This deprication has made lots of changes. You won't have acces to any distributing tool anymore. No more `distutils`, `setuptools` or `virtualenv` by default. In fact, this quick change ensures you from a real isolated `venv` and that's a positive point. From now on, if you make a virtual environment, nothing is installed there except `pip`.

### `**kwargs` Type Hinting

In the new update, lots of changes have happened to the `typing` module. I used to use `typing.Any` for type hinting the `**kwargs` of my functions and method. That was actually quite a deal but in Python 3.12, you can give it a more precise type annotation using `typing.TypedDict`.

```python
from typing import TypedDict, Unpack

class Values(TypedDict):
    name: str
    age: int

def main(**kwargs: Unpack[Values]): ...
```

> IMO: I'd prefer to keep `kwargs` un-annotated for now.

### `@override` Type Hinting

There's a new `@override` type-annotation included in the `typing` module. It actually helps you to specify the methods that are meant to be overridden in the OOP design. Using this feature helps the typing tools such as `mypy` debugging your code in another sense.

```python
from typing import override

class A:
    def greet(): ...

class B(A):
    @override
    def greet(): ...
```

For instance, in the above example, if you make a typo issue and change `B.greet` to `B.great`, your `mypy` would most likely return a non-zero output in the STDOUT meaning the method that's meant to be overridden is not defined in the base class.

> IMO: I find this little trick quite useful actually. Also including a `mypy` execution in your CI pipeline would help you catch such issues.

### New `type` Defining

There has been a new syntax added to the new Python version. This new convention helps you define the \`Type Aliases\` easier.

* Before:
    
    ```python
    from typing import TypeAlias
    
    Students: TypeAlias = list[str]
    
    def list_students(students: Students) -> None: ...
    ```
    
* After:
    
    ```python
    type Students = list[str]
    
    def list_students(students: Students) -> None: ...
    ```
    

This new convention has changed how functions and methods look in Python as you can design your function scopes as follows.

* Before:
    
    ```python
    def list_students(students: List[str], grades: List[float]) -> None: ...
    ```
    
* After:
    
    ```python
    type Students = List[str]
    type Grades = List[float]
    
    def greet[Students, Grades](students: Students, grades: Grades) -> None: ...
    ```
    

The new pattern of the function definition is like `def NAME[*TYPES](*ARGS: TYPE) -> TYPE`. Keep in mind that the types that are included in front of the name of the function are limited to the function scope.

> IMO: I think this feature just violates the readability of the new function. I'd prefer them in the old way if declaration. Highlighting tools might change my mind though. We have see how they're going to deal with these new syntaxes and keywords.

### Per-Interpreter GIL

In the new update, we'll have full control over the GIL utilization in the sub-interpreters that we make. As the official docs say..

> This (Per-Interpreter GIL) allows Python programs to take full advantage of multiple CPU cores.

We'll be talking about this new integration soon in another blog post. It seems to be a decent improvement over the performance manner.

### Conclusion

In this blog post, we talked about the major features and updates that are about to happen in Python3.12 and the new syntaxes that help us code in a cleaner way. Lots of new features are coming from the Typing module meaning the lining and formatting tools have to work harder in the incoming months to release a compatible version with the new Python patch.