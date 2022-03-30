## Python Closures; Also Known as Small Classes

Are you an OOP guy? Always using OOP to solve the problems even if you don't actually need it? Well, it was at this moment that Python Closures was released!

We are somehow familiar with OOP styles, their structures, and how they actually work. In most cases, we don't need the Object-Oriented structure, but we still use it and believe that everything is fine as clean. You are right as I totally agree with you. Everything is working. You make it a little bit complicated. Let's prove with examples.

### Python Classes

Imagine that you have to make a connection between your host and your database and you need to pass the QuerySet every time and get the result as well. You try to implement it using classes like this.

```python
import mysql.connector

class Database:

    def __init__(self, host, username, password, database):
        try:
            self.connection = mysql.connector.connect(
                host=host,
                user=username,
                password=password,
                database=database,
            )

            self.cursor = self.connection.cursor()
        except:
            print('something went wrong')

    def execute(self, query):
        try:
            self.cursor.execute(qurey)
            result = self.cursor.fetchall()
            return result
        except:
            print('something went wrong')

my_db = Database(
    host='localhost',
    username='alireza',
    password='testpass123',
    database='shop',
)

result = my_db.execute('select * from users')
```

This piece of code works well. What is the purpose of using OOP in this case? Are you keeping the metadata as a parameter? Like implementing the caching structure using OOP? I'm not sure if you are. You have just created a shortcut for using the `mysql.connector` module via classes which is a bit complicated and not recommended at all. So what? You better head to the next section.

### Nested Functions
Closure functions are one of the most brilliant use cases of inner functions or nested functions. They do act like a small piece of class, but they are way understandable, small, and useful. In order to understand the closures, you better take a short look at what a nested function is.

A function that is described in another function is called an Inner Function and the whole function is called Nested Function. As amazing nested functions use cases, we can point out the Decorators, Closure Functions, and Encapsulation. In the following script, you can find the simplest nested function ever.

```python
def printer():
    def say_hello():
        print('Hello, world')
    return say_hello

var = printer()
var() # >>> Hello, world
```

Why don't we run the `say_hello()` function directly? I don't have access. I must create a `printer` object first in order to be able to call the `say_hello()` function. This part might be a little bit tricky until you believe that everything is an object in Python; which means that you can do whatever you want with functions, classes, variables, and so on. Pass them as an argument, store them in a list, or etc.

### Closures

Let's back to our database example. Now, I'm trying to implement this scenario using a closure function.

```python
import mysql.connector

def Database(host, username, password, database):

    try:
        connection = mysql.connector.connect(
            host=host,
            user=username,
            password=password,
            database=database,
        )

        cursor = connection.cursor()
    except:
        print('something went wrong')

    def execute(qurey):
        cursor.execute(qurey)
        result = cursor.fetchall()
        return result

    return execute

my_db = Database(
    host='localhost',
    username='alireza',
    password='testpass123',
    database='shop',
)

result = my_db('select * from users')
```

Brilliant yea? Now, what just happened there? Well, the inner function has access to the outer function arguments and declared variables, but you need to make sure that there is something that might take you a lot of time in some cases and that's "Immutability".

### Change Immutables in Closure Functions
We are going to create a closure function that inputs numbers and returns the overall average every time we pass a new number.

```python
def calc():
    total = 0
    count = 0

    def appender(number):
        count += 1
        total += number
        return total / count
    return appender


points = calc()

for i in [points(5), points(10), points(12)]:
    print(i)
```

Does everything look fine? Hack no. In Python, integers, tuples, strings, floats, decimals, ranges, and booleans are immutable which means that you can't change their values after the deceleration. You should use the `nonlocal` keyword in order to make the variables free for the inner function so that the inner function would be able to make changes and reevaluate the variables. In this case, the variable is no longer private and would be accessible from the inner function. This topic backs to the variable declaration.

```python
def calc():
    total = 0
    count = 0

    def appender(number):
        nonlocal total      # new
        nonlocal count    # new

        count += 1
        total += number
        return total / count
    return appender


points = calc()

for i in [points(5), points(10), points(12)]:
    print(i)
```

### Conclusion
Always learn the best practices. Do rely on them. They always help you to get out of the troubles in the best easiest way.