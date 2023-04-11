---
title: "Ellipsis in Python: The Mysterious Three Dots"
datePublished: Tue Apr 11 2023 15:04:38 GMT+0000 (Coordinated Universal Time)
cuid: clgce8p7a000q09jv8f3d8p9a
slug: ellipsis-in-python-the-mysterious-three-dots
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1680869095997/19b948ea-0d8a-4cb8-8a15-58059344da89.png
tags: python, python3, best-practices, numpy, intermediate

---

This article might seem quite interesting, especially to those who don't write codes in Python natively. Python is somehow popular for not forcing you to use semicolons at the end of each line. In fact, you can still use semicolons in Python for separating each line just in case your Python interpreter knows where each line ends.

```python
print("Hi there."); print('Never stop dreaming!'); print('Bye!')
```

Additionally, lots of code compression algorithms and tools use the same technique for reducing the size of Python file source codes.

Let me get you straight to the point. What if I tell you that there is a mysterious symbol that has meanings based on different cases in Python?!

In this article, we're going to talk about Ellipses (...) \[three trailing dots\] in Python. To begin with, a quick overview of this symbol in English literature might seem quite handy. You've probably seen or used this symbol through your text messages with your friends, chats, and writings before.

Hope this short introduction helps you get into the Pythonic use of `Ellipsis` easier.

### Ellipsis in Literature and Language

In terms of punctuation, Ellipses have special meanings and you have to make sure of the way you use them. There are some points you need to be careful about. By the way, Ellipses is the plural form of ellipsis.

#### Indicating a pause in speech

You might've seen this type of Ellipses usage so many times through books and novels. Check the following examples.

* Hmm.. not really. She used to be a successful manager back in the day. \[pause due to thinking\]
    
* It feels... it feels amazing when you think of your rises and falls! \[pause due to controlling the emotions\]
    

As you can see, we have pauses throughout our sentences meaning the speaker had a short stop before he ends his sentence. This pause might happen for some reason. Either when you get emotional about something and you want to recover quickly in order to finish your sentence ASAP or you need to think about something before completing your sentence.

#### Showing a part of someone's exact quotation

Another famous use case of Ellipses backs to when we want to mention a part of someone's speech and we don't need to or have to write down his whole speech. It's more of putting attention to a phrase from the speech which relates more to the topic.

* The greatest glory in living lies not in never falling... \[we don't need the second part of the quote\]
    
* ...it's something you practice daily. \[we just need the second part of the quote\]
    

Make sure not to change the meaning of the quotes via ellipsis. The following use of ellipsis is nothing but a huge mistake and misuse.

* Ever since Sam started working at the company, meeting that guy got his career life ruined. \[it looks like we have to blame that friendship\]
    
* Sam started working at the company... got his career life ruined. \[it looks like we have to blame the company\]
    

As you can see here, the ellipsis changed the meaning of the sentence entirely. The reason for his fall wasn't that company but it looks so in the sentence with the ellipsis.

Don't use Ellipses for chopping and sticking different parts of a sentence together. It changes the meaning as you noticed from the earlier example.

Now, it's time for the Pythonic side. Hopefully, this short literature introduction has given you a proper insight into Ellipses.

### Ellipsis in Python

In Python, `Ellipsis` is a reserved keyword. That's quite obvious that you can't name your variables, classes, functions, or methods with the same exact name. `Ellipsis` is a built-in singleton in Python just like other keywords like `pass`, `True`, `False`, etc.

You can assign `Ellipsis` to a variable in two ways. Either using `...` or `Ellipsis` just as follows.

```python
>>> ... == Ellipsis
True
>>> var = ...
>>> print(var)
Ellipsis
>>> var = Ellipsis
>>> print(var)
Ellipsis
```

Ellipses might not look beneficial enough in variable assignments. I'm not talking about arguments or type-hinting situations yet.

In the function bodies though, Ellipses work just like `pass`.

```python
>>> def greet(name: str) -> str:
...     ... # works just like `pass`
...
>>> greet('Sadra') # nothing returns
>>>
```

Just like `pass`, using `...` as a function body means that the function is not implemented yet and when you run it, nothing happens.

Follow the next section and learn more about certain use cases of these magic three dots in Python.

### The Use Cases

There are a few major use cases of ellipsis in Python. In this section, we're going to get our hands on each use case and make use of them through our daily work.

#### Ellipsis for readability in reviewing

We sometimes use `...` to cut out a block of code for more readability and to put attention to a specific part of the code for better reviewing purposes. By doing this, we're indicating the functions and what they do by their names.

In the following example, we need to focus on the initializer method so that we cut out the other bodies for the sake of more readability in reviewing. Both `to_rgb()` and `to_hex()` methods don't actually work in action.

```python
class Color:
    def __init__(self, color: Tuple):
        self.rgb = Color.to_rgb(color)
        self.hex = Color.to_hex(color)

    @staticmethod
    def to_rgb(color: Tuple) -> str:
        ...

    @staticmethod
    def to_hex(color: Tuple) -> str:
        ...
```

#### Ellipsis in annotations

A common use of Ellipses in Python is in annotations and type hinting which is fully described in [PEP484](https://peps.python.org/pep-0484/). Ellipsis is mainly used for annotating `Tuple` and `Callable` typed arguments or returning value.

The following annotation for `calc_average` shows that the function takes an argument called `numbers` which is meant to be a Tuple of *only* three integer values.

The next function `calc_sum` has the same argument but a different annotation type. It now takes an arbitrary length of items. It might either be one item or thousands of items.

```python
from typing import Tuple

def calc_average(numbers: Tuple[int, int, int]):  # <-- focus here
    """
    Args:
        numbers: meant to be a tuple filled with only three integers
    """
    ...

def calc_sum(numbers: Tuple[int, ...]):  # <-- focus here
    """
    Args:
        numbers: meant to be a tuple full of only integers
    """
    ...
```

In the above example, `...` means *Any Much* item of a type.

Now, imagine a function that takes another function with an arbitrary amount of arguments as its argument. To annotate such an argument we simply use ellipsis just as follows.

```python
def calc_sum(func: Callable[..., float]): ...

# an example call
calc_sum(sum)
```

The `Callable` type has `Callable[[<parameters>], <return type>]` pattern. First, you specify the parameters' types and end up with the return type. The default Python `sum()` function almost does the same thing. It takes an arbitrary amount of numbers and returns back another numeric-typed value.

#### Ellipsis as function bodies

As you might've already noticed, we used ellipses to summarize the body of the functions in the previous example. We mainly use `...` for a function's body when we don't need to implement the function yet. It makes a lot of sense when it comes to writing unit tests that we'll see later on.

#### Stub files

Python is a dynamically-typed language meaning you don't need to specify the types of variables and entities. It deals with them on its own. There are some cases in which we need to have a quick template file about the structures used in our source code. A stub file collects all the components (variables, classes, methods, functions, attributes) from a source code, tries to annotate them, and puts them into a `.pyi` file. Stub file auto-generators usually use ellipses for indicating the body of functions, classes, and methods.

```python
class Car:
    def __init__(self):
        self.horiz = 0
        self.vert = 0

    def move_forward(self, miles):
        return [self.horiz, self.vert + miles]

    def move_backward(self, miles):
        return [self.horiz, self.vert - miles]

    def move_left(self, miles):
        return [self.horiz + miles, self.vert]

    def move_right(self, miles):
        return [self.horiz - miles, self.vert]
```

I'm using [stubgen](https://mypy.readthedocs.io/en/stable/stubgen.html) to generate a stub file from the above class and here we have it.

```python
class Car:
    horiz: int
    vert: int
    def __init__(self) -> None: ...
    def move_forward(self, miles): ...
    def move_backward(self, miles): ...
    def move_left(self, miles): ...
    def move_right(self, miles): ...
```

#### Ellipsis as unit test bodies

Another interesting use case of ellipsis in Python is that you can use them as the body of your unfinished unit tests just in case they don't break the whole testing system. Overall, it's fine to use Ellipses for your function's body if it's an isolated function and not related to or required by other components.

The main criterion for a unit test function is that it has to be isolated so feel free to use ellipses as their bodies.

```python
import unittest

class TestCase(unittest.TestCase):

    def test_if_values_are_valid(self):
        ...
    
    def test_if_numbers_are_included(self):
        ...

    def test_if_equality_works(self):
        self.assertEqual(self.object.sum(1,2,3), 6)
    
    def test_object_attributes(self):
        pass
```

And you'll see...

```python
$ python file.py 
....
----------------------------------------------------------------------
Ran 4 tests in 0.000s

OK
```

### Handle Ellipsis in Python

In Python, if you declare a list variable with a bunch of values, you can access each item by catching them by their indices number.

```python
>>> names = ['sam', 'jose', 'elef', 'robbin']
>>> names[2]
'elef'
```

As we described earlier, in an annotation pattern like `Tuple[..., str]`, an ellipsis means *Any Much Item* of `str` type. That said, `names[...]` must return every item from the list, doesn't it?!

```python
>>> names[...]
TypeError: list indices must be integers or slices, not ellipsis
```

Python does not support `Ellipsis` as a valid sushi operator. Thus, it does not make any sense in pure Python to have ellipsis in brackets. To be honest, there are third-party packages that deal with this kind of usage.

Numpy is a popular Python package that provides arithmetic and mathematic functionalities for arrays in Python. In Numpy, you can simply use an ellipsis for slicing.

```python
import numpy as np

np_names = np.array(['sam', 'jose', 'elef', 'robbin'])
names = [_ for _ in np_names]

print(names[...])    # Error
print(np_names[...]) # ['sam', 'jose', 'elef', 'robbin']
```

This might seem a bit confusing but `np.array` has some implementation for dealing with `...` as a slicing operation.

Now, in order to understand this concept easier, I want to inherit from the actual Python's list type and make it ellipsis-friendly and whenever we call the list with ellipsis, it returns the full items of the list.

```python
from typing import Union, Any

class MyList(list):

    def __init__(self, values: list) -> None:
        self.values = values

    def __getitem__(self, no) -> Union[list[Any], Any]:
        if no == Ellipsis:
            return self.values
        
        for i, j in enumerate(self.values):
            if i == no:
                return j

        raise IndexError('Index out of range.')

names = MyList(['sam', 'jose', 'elef', 'robbin'])
print(names[3])   # --> robbin
print(names[4])   # --> <IndexError>
print(names[...]) # --> ['sam', 'jose', 'elef', 'robbin']
```

### Ellipsis in Python2.X

In Python 2, the `Ellipsis` use cases were so limited as there were no keywords reserved as `Ellipsis`. You could access it through the `__getitem__` method.

### Conclusion

In conclusion, Ellipsis in Python is a reserved keyword that has various use cases. It can be used for readability in reviewing, annotations, function bodies, stub files, and unit test bodies. It is important to note that ellipses have special meanings in literature and language, and care must be taken when using them to avoid changing the meaning of sentences. Overall, understanding the use cases of ellipsis in Python can help improve code readability and organization.