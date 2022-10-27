# Python 3.11 - Five Cool Features!

This is a quick walk-through of the newly added features in Python 3.11. Of course, you can find many more other features and improvements during the migration from 3.10 to 3.11 but I tried to note five handy features and improvements that I think would be perfect for you to observe while coding along in Python.

### `tomllib` Is Added to the Standard Library
The `tomllib` library used to be a third-party package for your Python<3.11 projects. Now, they've decided to add this handy package to the official standard library so that you won't need any further installation to access the utilities this library provides for you.

```python
import tomllib

with open('setup.toml', 'rb') as f:
    data = tomllib.load(f)
    print(data) # -> {...}
```

> `TOML` stands for Tom's Obvious, Minimal Language. It's a powerful config file data type that is compatible with other Python components such as `setuptools`. It's also more human-readable compared to JSON, YAML, and some other structures.

###  `add_note` Method Is Added to `Exception` Base-Class

```python
try:
    email, message = input('to: '), input('message: ')
    send_email(email, message)
except ConnectionError as e:
    e.add_note('Make sure the mail server is up and running')
    raise
```

### Tracebacks Are More Detailed
It shows the exact place that caused the error with "~" followed by "^".

```sh
Traceback (most recent call last):
    File "query.py", line 32, in query_user
        return 1 + query_count(db, response[e][b][user, retry=True)
                                   ~~~~~~~~~~~~~~~^^^^
TypeError: NoneType object is not subscriptable 
```
### `Self` Type Class Is Here
For all the methods you have, you can annotate the `args` with `Self` other than the name of your class. It helps you in a case when you have multiple methods that have arguments annotated to the class and you decide to change the class name. ([There is a difference between `self` and `Self` in Python from now on. `self` refers to the object whereas `Self` refers to the class for annotations](https://docs.python.org/3.11/library/typing.html#typing.Self))

```python
class Student:
    @classmethod
    def give_info(cls) -> Self:
        ...
```

### Use `StrEnum` Over `Enum` For Your Strings
If you need a class of strings, then use `StrEnum`. They make your code readable and you won't need any additional writing. Just use `auto()` for the values. Both following enums work as same as the other.

```python
from enum import Enum, StrEnum, auto

class Colors(Enum):
    RED = 'red'
    BLUE = 'blue'
    WHITE = 'white'

class Colors(StrEnum):
    RED = auto()
    BLUE = auto()
    WHITE = auto()
```

We also have `ReprEnum` which changes the return value of `__repr__` of each object.

### Final Words
We have so many typing improvements in 3.11 so far. That's awesome! Now all our annotations are more accurate and detailed.