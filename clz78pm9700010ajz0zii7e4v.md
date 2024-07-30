---
title: "10 Python Easter Eggs"
datePublished: Mon Jul 29 2024 17:05:23 GMT+0000 (Coordinated Universal Time)
cuid: clz78pm9700010ajz0zii7e4v
slug: 10-python-easter-eggs
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1722274117791/2a0c192a-ac8a-4dd4-9f17-3a87b4f5d572.png
tags: software, python, python3, fun, best-practices, easter-eggs

---

Python, the versatile and widely used programming language, is known for its readability and simplicity. However, beneath its surface lies a whimsical side, with numerous Easter eggs that reflect the playful nature of its developers. These Easter eggs range from humorous references to historical nods and clever tricks, each adding a touch of personality to the language. In this article, we'll dive into ten fascinating Python Easter eggs, complete with code snippets to illustrate these hidden gems.

### 1\. The Zen of Python

One of the most famous Easter eggs in Python is the "Zen of Python," a collection of guiding principles for writing computer programs. These aphorisms were written by Tim Peters and can be displayed by importing the `this` module.

```python
import this
```

Upon executing this code, you'll be greeted with the Zen of Python:

```plaintext
The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
```

Devs are sometimes good philosophers. Check this out.

```python
>>> import this
>>> love = this
>>> this is love
True
>>> love is True
False
>>> love is False
False
>>> love is not True or False
True
>>> love is not True or False; love is love
True
```

Poetic. Isn't it?!

### 2\. Importing Antigravity

Python takes you on a literal journey when you import the `antigravity` module. This Easter egg references a famous XKCD comic strip about Python.

```python
import antigravity
```

Executing this code opens your web browser and takes you to the XKCD comic about Python:

![XKCD Python](https://imgs.xkcd.com/comics/python.png align="center")

### 3\. The Walrus Operator

Introduced in Python 3.8, the walrus operator (`:=`) allows assignment expressions. The fun part is that it's named after it resembles the eyes and tusks of a walrus.

```python
if (n := len('walrus')) > 5:
    print(f"The length of 'walrus' is {n}")
```

Output:

```plaintext
The length of 'walrus' is 6
```

### 4\. Barry's Eggs

There's a quirky Easter egg that references Barry Warsaw, one of Python's developers. By using the `from __future__ import barry_as_FLUFL` statement, you can enable an alternative form of assignment using the `<>` operator, reminiscent of the older days of Python.

```python
from __future__ import barry_as_FLUFL

# This will work with the import above
2 <> 3
```

Output:

```plaintext
True
```

But if you do this, it'll raise an exception.

```python
2 != 3
# SyntaxError: with Barry as BDFL, use '<>' instead of '!='
```

### 5\. Hello, World!

The classic "Hello, World!" program has a playful twist when using the `__hello__` module.

```python
import __hello__
```

Output:

```plaintext
Hello world!
```

Whenever you install Python in a fresh environment, you can also do this to ensure your Python setup process is successful.

```bash
$ python -c "import __hello__; __hello__.main()"
Hello world!
```

### 6\. Braces in Python

Python's design philosophy famously excludes the use of braces (`{}`) for code blocks, preferring indentation instead. However, there's an Easter egg that humorously acknowledges this design choice.

```python
from __future__ import braces
```

Instead of enabling braces, this code raises a `SyntaxError` with the message "not a chance."

Output:

```plaintext
  File "<stdin>", line 1
    from __future__ import braces
                                  ^
SyntaxError: not a chance
```

I guess we'll never see anyone using braces in Python ever.

### 7\. Time Travel with `timeit`

The `timeit` module is used for timing the execution of small code snippets. But did you know it also contains a cheeky reference to "time travel"?

```python
import timeit

timeit.timeit('"-".join(str(n) for n in range(100))', number=10000)
```

Output:

```plaintext
0.28043669999999996
```

While this example shows the normal use of `timeit`, the module's documentation contains whimsical references to time travel, such as "If you can time travel, then you're doing it wrong."

### 8\. Python Philosophy

Python's `import this` reveals the Zen of Python, but there's also another philosophical Easter egg when you try to import `__phello__`.

```python
import __phello__.world
```

Output:

```plaintext
Hello world!
```

This playful module echoes the traditional "Hello, World!" while embedding it in a mysterious, underscore-laden package name. Somehow similar to `import __hello__`.

### 9\. Swapping Values

Python allows for elegant value swapping without a temporary variable. While not strictly an Easter egg, this feature often surprises newcomers.

```python
a, b = 1, 2
a, b = b, a
print(a, b)
```

Output:

```plaintext
2 1
```

### 10\. Exception Thrower

In Python 3.9, `__peg_parser__` would throw a syntax error with a certain message of "You found it!".

```plaintext
>>> __peg_parser__
  File "<stdin>", line 1
    __peg_parser__
    ^
SyntaxError: You found it!
```

## Conclusion

Python's Easter eggs add a layer of charm and character to the language, reminding us that programming can be both a serious and fun endeavor. These hidden gems not only showcase the creativity of Python's developers but also invite us to explore and enjoy the lighter side of coding. Whether you're a seasoned Pythonista or a curious newcomer, these Easter eggs are sure to bring a smile to your face and a deeper appreciation for the delightful intricacies of Python. Happy coding!