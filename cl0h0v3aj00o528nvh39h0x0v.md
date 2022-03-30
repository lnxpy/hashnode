## How Context Manager Works in Python

A necessary skill of being a team member is the ability of making reusable tools. As a project core developer, you need to be able to satisfy your requirements by making new implementations. You actually make a public pattern that's available for others in usage cases. You make a class that all you need is only an object from that class in your project.

As a Python developer, you've definitely worked with the I/O system and files. It all backs to whether using `with` or just keeping up with the old strategy which is a bad one. What is the secret behind `with`?

### Resource Management is Everything
In the software programs, everything is focused on resource management and optimizations. Your software won't crash anymore with a proper resource manager implemented in your project and I'm still able to set it up on my oldish PC.

### Use `with`
You might have been using the oldish style for using the file systems right? In this case, your resources are interacting with the file systems over and over even if you are done with the files.

```python
file = open('file.txt', 'w')
file.wrtie(1) # raises TypeError
file.close()
```

Here you go. You prove that you have used `file.close()` in order to release the resources after writing in the file. Imagine that there is something wrong with `file.txt`. What would happen in that case? It's easy. The interpreter has raised an exception in line 2 (it could be a simple `TypeError`) which means that the third line is still untouched and the resources are still being used. You may give it another shot with:

```python
try:
    file = open('file.txt', 'w')
    file.write('test')
except TypeError:
    # some code here..
    pass
finally:
    if file:
        file.close()
```

You gotcha. It's what `with` actually does. You've implemented the class all on your own. Let's make it easier.

```python
with open('file.txt', 'w') as file:
    file.write('test')
```

Now I feel like all Python gods are kneeling in front. In the above snippet, your file will be loaded and after the processes, it finally will be closed and resources are free now.

### Implement `with` Ability for Classes
All you need is to implement the `__enter__` and `__exit__` methods for your class to make users be able to release their resources after using your classes.

You have a class that connects to a database and executes a single query and after that, It needs to close the connection between the host and the database engine. In this example, the concept is much more important than the actual script.

```python
import database as DB

class DataBase():
    def __init__(self, host, username, password, database):
        # constructing the values...
        pass

    def __enter__(self):
        self.connect = DB.connect(self.host)
        return self

    def __exit__(self, exception_type, exception_value, traceback):
        self.close()
```

Therefore, you can define your object variable right after `as`. In this case, my object is called `db`.

```
from moduels import DataBase

configs = {
    'host': 'localhost',
    'username': 'test',
    'password': 'test123',
    'database': 'shop',
}

with DataBase(**configs) as db:
    db.execute('SELECT * FROM users;')
```

Now, after each execution inside the `with` block, it will terminate the connection.

### Conclusion
Python has provided tons of amazing built-in classes, functions, and concepts. It's so cool using stuff that makes life easier. In this article, you learned a trick to stay away from software crashes and additional resource usage.