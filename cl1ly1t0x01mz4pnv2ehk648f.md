## setUp() & tearDown() in Python Unit Testing

I'm pretty sure you've already used/seen unit tests in the projects before. Have you ever wondered about how Django actually prepares you an isolated environment for testing your project without affecting other resources like your database? Before we jump into the actual `django.test.TestCase`, I'm going to talk about some unit test's magics in Python.

### Unit Testing
As a developer, you should always have your testing tools and be familiar with them. Testing tools allow you to validate any changes in your projects. You can maintain your open-source project easier with the help of tests.

Frankly, in some cases, **you don't need tests**. Imagine a personal private-source-code weblog. You are the only maintainer and there is no contributor but you. You have designed your project wisely so there is no dependency from each section/app to another like a Django project with tens of apps instead of an all-in-one app. In that case, since you know your project's functionality and features, although there is no point in taking time and writing tests for your project, you have to make sure no one else will contribute to your project in the future, otherwise, It'll be a huge mess. So from both sides, writing tests is a considerable task.

### `unittest` Library
In Python, we have a few popular testing tools. [`unittest`](https://docs.python.org/3/library/unittest.html) is unit testing standard library being used in most popular Python tools and frameworks. In this article, we are *not* going to learn the actual unit testing. However, we'll discover two most phenomenon `TestCase()` methods.

In the following snippet, we have a test case that needs some improvements.

```python
from unittest import TestCase
from module import School


class SchoolTestCase(TestCase):

    def test_add_course(self):
        school = School()
        school.addCourse('Math')
        self.assertTrue(school.course('Math').exists())

    def test_add_student(self):
        school = School()
        school.addStudent(
            first='John',
            last='Doe',
        )
        self.assertTrue(school.student(first='John').exists())

    def test_add_teacher(self):
        school = School()
        school.addTeacher(
            first='Alex',
            last='Hanks',
        )
        self.assertTrue(school.teacher(last='Hanks').exists())
```

As you may feel, we are repeating our selves. Don't we? We are creating the `School` object in multiple lines. That's awkward. `unittest.TestCase` has an implementation that you can define a method in your testcase and this method will be executed before each tasks. This method is called `setUp()` method.

```python
class SchoolTestCase(TestCase):

   def setUp(self):    # new
      print('setUp method called!!')

    def test_add_course(self):
      school = School()
      school.addCourse('Math')
      print('add course test')    # new
      self.assertTrue(school.course('Math').exists())

    def test_add_student(self):
      school = School()
      school.addStudent(
          first='John',
          last='Doe',
      )
      print('add student test')    # new
      self.assertTrue(school.student(first='John').exists())

    def test_add_teacher(self):
      school = School()
      school.addTeacher(
          first='Alex',
          last='Hanks',
      )
      print('add teacher test')    # new
      self.assertTrue(school.teacher(last='Hanks').exists())
```
So if we print something in this method, when you run your tests, you'll see something like what I got here. (Tests might not execute in order)

```shell
$ python -m unittest
...
setUp method called!!
add course test
setUp method called!!
add student test
setUp method called!!
add teacher test
...
```
With that being said, we can create the `School` object in the `setUp()` method and avoid repeating ourselves.

```python
class SchoolTestCase(TestCase):

   def setUp(self):
      self.school = School()    # new

    def test_add_course(self):
      self.school.addCourse('Math')
      self.assertTrue(self.school.course('Math').exists())

    def test_add_student(self):
      self.school.addStudent(
          first='John',
          last='Doe',
      )
      self.assertTrue(self.school.student(first='John').exists())

    def test_add_teacher(self):
      self.school.addTeacher(
          first='Alex',
          last='Hanks',
      )
      self.assertTrue(self.school.teacher(last='Hanks').exists())
```

Brilliant! Now, when we execute each test, we have a brand new fresh `School` object. We want to see the execution time of each test. Now, we have crafted a method being executed before each test execution. What if there was a method that was being executed after each test execution? Like one after and one before each test. Actually, there is and it's called `tearDown()` method. 

```python
class SchoolTestCase(TestCase):

    def setUp(self):
       self.school = School()

    def tearDown(self):    # new
        print('tearDown method called!!')

    def test_add_course(self):
      self.school.addCourse('Math')
      print('add course test')
      self.assertTrue(self.school.course('Math').exists())

    def test_add_student(self):
      self.school.addStudent(
          first='John',
          last='Doe',
      )
      print('add student test')
      self.assertTrue(self.school.student(first='John').exists())

    def test_add_teacher(self):
      self.school.addTeacher(
          first='Alex',
          last='Hanks',
      )
      print('add teacher test')
      self.assertTrue(self.school.teacher(last='Hanks').exists())
```

And what we get as the output.

```shell
$ python -m unittest
...
add course test
tearDown method called!!
add student test
tearDown method called!!
add teacher test
tearDown method called!!
...
```

Now we can simply measure each time execution of our tests as follow.

```python
from unittest import TestCase
from module import School
from time    # new


class SchoolTestCase(TestCase):

   def setUp(self):
      self.school = School()
      self.start = time.time()    # new
   
   def tearDown(self):
      self.end = time.time()    # new

    def test_add_course(self):
      self.school.addCourse('Math')
      print(self.start - self.end)    # new
      self.assertTrue(self.school.course('Math').exists())

    def test_add_student(self):
      self.school.addStudent(
          first='John',
          last='Doe',
      )
      print(self.start - self.end)    # new
      self.assertTrue(self.school.student(first='John').exists())

    def test_add_teacher(self):
      self.school.addTeacher(
          first='Alex',
          last='Hanks',
      )
      print(self.start - self.end)    # new
      self.assertTrue(self.school.teacher(last='Hanks').exists())
```

In the next section, we'll talk about `setUpClass` and `tearDownClass` class methods and the way that Django takes benefit of them.

### Database Caching in `setUpClass` and `tearDownClass`

Imagine the `School()` class we had previously. You want to test multiple functionalities of a single object from the class `School()`. In that case, you don't need to recreate a brand new object again and again. Just one object for the entire test. You can simply use the `setUpClass()` class method. This method gets executed once, right before your first test method gets executed. On the other hand, you want one of your object's methods to get executed at the end of the testing process. You can simply implement it using the `tearDownClass()` class method.

```python
class SchoolTestCase(TestCase):

    @classmethod    # new
    def setUpClass(cls):
       print('setUpClass method called!!')
       cls.school = School()
    
    @classmethod    # new
    def tearDownClass(cls):
        print('tearDownClass method called!!')
        cls.school.terminate()

    def test_add_course(self):
      self.school.addCourse('Math')
      print('add course test')
      self.assertTrue(self.school.course('Math').exists())

    def test_add_student(self):
      self.school.addStudent(
          first='John',
          last='Doe',
      )
      print('add student test')
      self.assertTrue(self.school.student(first='John').exists())

    def test_add_teacher(self):
      self.school.addTeacher(
          first='Alex',
          last='Hanks',
      )
      print('add teacher test')
      self.assertTrue(self.school.teacher(last='Hanks').exists())
```

When you run your tests, this output will be shown.

```shell

$ python -m unittest
...
setUpClass method called!!
add course test
add student test
add teacher test
tearDownClass method called!!
...
```

Django web framework uses the same technique to cache a new database based on the models. Then it migrates all changes to the tables and gets the environment ready for running tests.

> [Tests that require a database (namely, model tests) will not use your “real” (production) database. Separate, blank databases are created for the tests](https://docs.djangoproject.com/en/4.0/topics/testing/overview/#the-test-database-1).

Basically, as you might guess, all these steps and tasks happen in the `setUpClass()` method. Finally, Django terminates the database in the `tearDownClass()`.

> Regardless of whether the tests pass or fail, the test databases are destroyed when all the tests have been executed.

Here you see a simple conception mechanism that Django does like that in the case of database caching for running tests.

```python
class TestCase(unittest.TestCase):
    '''
    Sadra's Mini Django TestCase Concept :)
    '''

    @classmethod
    def setUpClass(cls):
        with DataBase('cache.db') as connection:
            cls.db = connection.start()

        from django.migrations.files import migration
        
        cls.db.migrate(migration.lastMigration())

    @classmethod
    def tearDownClass(cls, do_save):
        if do_save:
            # import data to the original db
            pass
        cls.db.terminate()

    ...
```

You can refer to the [Django Official Repository](https://github.com/django/django) for more information about the implementations.

### Conclusion
Having tests in our products allows other developers to contribute to the product much easier and the maintenance would be a lot easier for us. Therefore, knowing the tricks and techniques in terms of working with tests would be a crucial point.