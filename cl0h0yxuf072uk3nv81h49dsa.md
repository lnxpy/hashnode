## The Power of Django ORM

Object Relational Mapping functions and methods help you to interact with the database in an optimized way. Here, we are going to take a look at its features and things that you better know as a Django developer.

### What is ORM
Object Relational Mapping (ORM) allows developers to progress their projects and interact with the database in an OOP-like style. In this case, you do not need to have any knowledge about the SQL or NoSQL syntax. As a professional, You need to know OOP in order to work with ORMs and make reusable applications integrated with them.

In this article, I'll show you how to use Django ORM in an efficient way, what's more, you'll figure out the ways you can optimize your queries and connections. So, it's going to be a simple piece of cheat that you can refer to anytime.

### Use Exceptions in `get()`
One of the most important keys in pulling or pushing something from/to the database, is using exceptions to show the proper output.

```python
try:
    query = Users.objects.get(id=10)
except Users.DoesNotExist:
    # some code here..
except Users.MultipleObjectsReturned:
    # some code here..
else:
    # some code here as well..
```
Using the proper exceptions is the key to being a genius in ORMs. It's the way that you can interact with users or maybe even devs.

### Django `connection`
`connection` is one of the most extraordinary built-in Django modules out there. It allows you to optimize your ORM query as well as its complexity. It stores the last query SQL syntax and shows the run time in a JSON-like format in order to give you more information about the querysets. You can either test your modules or write them through the prompt shell.

```python
>>> from django.db import connection
>>> from app.models import Author
>>> connection.queries
[]
>>> Author.objects.all()
<QuerySet [<Author: Author object>]>
>>> connection.queries
[{u'time': u'0.002', u'sql': u'SELECT "library_author"."id", "library_author"."name" FROM "library_author" LIMIT 21'}]
```

You can also use `--print-sql` flag in order to use Django Connection automatically when you want to run into the Django shell. (In this case, every time you run a query, your prompt shows you the created query SQL syntax + its response time)

### Iterators
A queryset typically caches its results when evaluation happens and for any further operations with that QuerySet, it first checks for cached results. But when you use `itarator()` it ignores the cached data and it will read the results directly from the database. It also doesn't update the cache data with the iterated data. This technique avoids resource-consuming in most cases.

```python
# Without Iterators
users = Users.objects.all()
for user in users:
    # some code here..

# With Iterators
users = Users.objects.all().iterator()
for user in users:
    # some core here..
```

### Set The Timeout
Typically you need to keep the connections open for better performance otherwise, you have to work with several connections during your tasks with the database which is very time-consuming. Use `CONN_MAX_AGE` in settings to set how much time (ms) you want a connection to stay open. (Default is set to 0ms)

### ORM Best Tricks
Let's learn some of the most effective tricks that developers should know about the ORM in Django.

#### F() Function
You can assign a new value to a specific field from all records instead of looping into the story. Using `f()` function prevents time-consuming. SO GOOD..!

```python
# Don't
for user in Users.objects.all():
    user.claps += 1
    user.save()

# Do
Users.objects.update(claps=F('claps') + 1)
```

#### Aggregations
NEVER loop through the query results. It brings tons of timing, resource, and technical issues to your project you may not notice. Do queries in one line outside the loops. This technique is FIRE. That's how I count my `Post.likes` so far.

```python
# Don't
most_claps = 0
for user in Users.objects.all():
    if user.claps > most_claps:
        most_claps = user.claps

# Do
most_claps = Users.objects.all().aggregate(Max('claps'))['claps__max']
```

#### `len()` or `count()`
So simple, If you don't need the contents of your queryset, never use `len()` in order to get the count of your objects.

```python
# Don't
all_users = len(Users.objects.all())

# Do
all_users = Users.objects.count()
```

Also, use `exists()` method whenever you want to check an object's existence status.

```python
# Don't
all_users = Users.objects.all()
if all_users:
    # some code here..

# Do
if Users.objects.exists():
    # some code here..
```

#### `bulk()` For Ever
This method is highly effective throughout your works. Imagine that you need to create 100 records on your database. So, you start creating your loop and other stuff which is BRUH. Use `bulk()` to create thousands of record at once!

It's not a big deal for Python to append 100 defined objects to a list, but it's a huge deal to run 100 queries. So, let's love Python. 

```python
# Never do
for i in range(100):
    Users.objects.create(...)

# Do
User_objects = []
for i in range(100):
    User_objects.append(Users(...))
Users.objects.bulk_create(User_objects)
```

Just see how it affects on the latency. I've already created two simple unit tests here to prove the priority of `bulk` method.

```bash
(.venv)$ python manage.py test docs.tests.DocsTestCase.query
Creating test database for alias 'default'...
System check identified no issues (0 silenced).
----------------------------------------------------------------------
OK. Ran 1 test in 0.055s
```

```bash
(.venv)$ python manage.py test docs.tests.DocsTestCase.query2
Creating test database for alias 'default'...
System check identified no issues (0 silenced).
----------------------------------------------------------------------
OK. Ran 1 test in 0.010s
```

As you can see, the `bulk` method is a lot faster than the previous traditional method. All these tools have been built to make the life much easier. What they do is they optimize the performance which is huge in a word.