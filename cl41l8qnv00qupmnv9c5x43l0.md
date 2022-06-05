## Unit Testing in Python & Best Practices

In this article, I'll help you to understand the basics of unit testing in Python and then, we'll talk about the awesome practices that make your tests way more understandable and maintainable. If you are looking for a point to start writing tests for your Python projects, here we are. Without further ado, let's see some magic.

### 1. Software Testing & Unit Tests
Software testing is a stage where we test our project to make sure it raises the proper exceptions, returns the expected values, evaluates the entities properly, and so on. We can test our project in different ways. That's why we have multiple testing solutions. One of those solutions is called Unit Testing.

In a car, we have multiple electrical control units. We have the radio unit, lights, battery, battery charger, different systematic modules, etc. Whenever you face an issue in the electric system, you can simply check each unit to find the issue. This approach is more useful when your units are related to each other like when the radio needs the power coming from the battery. When the radio is not working as expected, you need to check both the battery unit and the radio one to find the issue. Imagine there was a software that was testing every single unit of your car and preparing you a report out of the tests! I would bye that.

We know what units are like for now. Every project is made up of different units. The integrity between these units makes an integration system that has its own testing solution called Integration Testing. Let's get back to the units and testing itself.

### 2. Why Testing
Many developers are struggling when it comes to writing tests like your project might still work well without having any tests, but is it still easy to maintain? Do other developers enjoy working on your project? Do new contributors pass the onboarding phase so quickly?

- __Increase the coverage and maintainability__. Most projects are being judged by their coverage status. Higher code coverage, happier developers.

- __With tests, fix bugs before implementing__. In Test-driven Development, developers try to design tests before they get their hands dirty with the actual implementation. They test a feature before they even add it to the project. Once it passed the tests statistically and logically, they merge it.

- __Tests are like documents__. With clean tests, you'll increase the maintainability of your project and the new developers can easily understand the different parts of the project by reading the tests and finding each part's requirements. When someone reads the tests, he/she understands what that unit is supposed to do. That's where Guido Van Rossum says:

> Code is read more often than it is written.

### 3. Isolate Your Tests
When it comes to isolation in Python, it reminds me of virtual environments there. They are actually the same but in fact, we have them in case of writing unit tests. So what is an isolated test?

Each test you write should be kept and run isolated which means, none of your tests should affect any other part of your project or any other tests living in the same file or project. Your tests are not supposed to change the real things such as data in the databases. That's the actual meaning of isolation where your tests only do their jobs and delete all their footsteps. Your tests should not depend on any other test.

Isolation makes your tests much easier to read. We are always afraid of dependent stuff and finding the issues in such a situation is so painful. An isolated test shows that any failure that we are having in the result will be solved in that specific test block and nowhere else. When you are running the entire project's tests and you have a failure on test number two, with isolated tests, it means that you can solve the issue in that test function and there is no chance for test number two to depend on any other test.

### 4. Let's Do Some Code
Enough talking. In Python, we have different powerful testing tools. The one we are using today is the [unittest](https://docs.python.org/3/library/unittest.html) standard library which provides different features without installing any additional library or package. You can use [PyTest](https://docs.pytest.org/) as well. Simply open a `tests.py` file and import the requirements.

```python
import unittest
from math import sqrt, power, pi
```

Notice we've imported some math functions as well. In the following simple test case, we are testing these functions from the math standard library to check if it still gives us the right answer.

```python
class TestMathLib(unittest.TestCase):

    def test_if_sqrt_still_works(self):
        self.assertEqual(sqrt(25), 5)

    def to_test_if_pi_still_starts_with_three(self):
        self.assertEqual(pi // 1, 3)

    def test_if_power_still_works(self):
        self.assertEqual(pow(2, 3), 8)
```

We got three tests so far. Let's run them. At the end of the file, to make it executable from the shell, we add the following line.

```python
if __name__ == '__main__': unittest.main()
```

Using the `python` command for running our tests is not recommended at all. What if you need to run a specific app's tests?! Then Python can not help anymore. Simply use the `unittest` command-line tool for more options and stability.

Now, open a fresh terminal tab and change your directory and run the following command.

```shell
python -m unittest
```

Here is the result.

```shell
..
----------------------------------------------------------------------
Ran 2 tests in 0.010s

OK
```

It looks like we got something! Since running the `unittest` command with no flags runs all tests, why did it run only two of them? What are those two dots up there?!

The `unittest` library just runs the test functions that are starting with the word `test` which means, in that test, our `pi` test is missing. To make it visible, add the keyword `test` at the beginning of the method name.

```shell
...
----------------------------------------------------------------------
Ran 3 tests in 0.010s

OK
```

Those dots at the beginning of the result shows the status of each test execution. It shows that it found three tests and all those tests are passed. There will be three `F`s other than three dots if all our tests fail. There is another situation where you might get `E`. It means that there is a problem with your test itself like there might be a syntax error or typo issue inside your test.

### 5. DAMP & DRY Principles in Your Tests
These two famous principles allow you to write clean and easy-to-understand tests. In this part, we'll talk about the beautiful names you can choose for your test cases and we'll be using the `setUp()` method to improve our tests.

#### 5.1. Descriptive and Meaningful Phrases (DAMP)
As we understood earlier, the `unittest` library will not run those tests starting with any word other than `test`. It's also a good reason to change the name of our function to a longer phrase like `test_if_multiplication_works` or `test_user_validation`. A name that represents what that test does. Also, make sure your test class is starting with the word `Test` because as your testing system grows, you may need some mocking classes which are not supposed to be tested independently and that's how you separate your testing functions.

#### 5.2. Don't Repeat Yourself (DRY)
Consider we need an object from a class called `Car` to test some of its methods and actions.

```python
class TestCar(unittest.TestCase):

    def test_if_car_can_move_forward(self):
        my_car = Car()
        self.assertEqual(my_car.move('forward'), 'car is moving forward')

    def test_if_car_can_move_backward(self):
        my_car = Car()
        self.assertEqual(my_car.move('backward'), 'car is moving backward')
    ...
```

Notice we are recreating an object from the Car class over and over. Use the `setUp()` method to define whatever you need per test. This method is called before each test you have.

```python
class TestCar(unittest.TestCase):

    def setUp(self):
      self.my_car= Car()

    def test_if_car_can_move_forward(self):
        self.assertEqual(self.my_car.move('forward'), 'car is moving forward')

    def test_if_car_can_move_backward(self):
        self.assertEqual(self.my_car.move('backward'), 'car is moving backward')
    ...
```

That's how you observe the DRY principle with `setUp()` method in your tests. For more information about these methods, check out [setUp() & tearDown() in Python Unit Testing](https://imsadra.me/setup-and-teardown-in-python-unit-testing).

### 6. Mocks
Mocking is not a test solution. It's actually part of some testing systems. Some projects may have mocks, some may not. With mocks, you can virtualize some necessities that your test may need in order to test a feature of the project.

As an example, imagine you have a function in your project that makes an HTTP request to an API and serializes the returned data. Now, you want to test the serialization phase by writing unit tests. What if that server crashes at the time you run your test? Your test will fail for sure but there is no room for blaming your project's feature right? It was not its fault. It was the server's crash that made your test fail.

![Artboard 1@4x.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1654197885475/tal8PxkE_.png align="center")

Mocking is the art of simulation. You can create a function that acts as the API server and you use it in the body of your test block. Then, your test failures will appear whenever there is something wrong with your project, not others'.

In the following example, we are mocking the `requests.get()` action. We have a module called `discovery.py` that contains the following function.

```python
from requests import get

def get_data(link, index):
    response = get(f'{link}/{index}')
    return get
```

In our `tests.py`, we need to test the `get_data()` function. Normally, my test will fail when the `link` is not reachable and the server might be the issue. This is how we mock that functionality.

```python
from unittest import TestCase, main, mock

from discovery import get_data
from requests import Response

succeed_response = Response()
succeed_response.status_code = 200

failed_response = Response()
failed_response.status_code = 404

class DiscoveryTest(TestCase):

    @mock.patch('discovery.get', return_value=succeed_response)
    def test_with_valid_index(self, mock_obj):
        response = get_data('https://google.com', 'search')
        self.assertEqual(response.status_code, 200)
    
    @mock.patch('discovery.get', return_value=failed_response)
    def test_with_invalid_index(self, moch_obj):
        response = get_data('https://google.com', 'somewhere')
        self.assertEqual(response.status_code, 404)

if __name__ == '__main__': main()
```

At first, this implementation might look a bit confusing. We are basically mocking the `get()` entity from the `dicovery` module as you can see in the patch decorators then, we specify the return value that we expect for the test.

In the `unittest` package, you can use mocks in different ways. You can implement them as decorators, context managers, or even purely in the `setUp` and `tearDown` methods. I prefer using decorators as it's more readable in my opinion.

### 7. Best Practices
We have pretty much talked about the major topics. In this section, we are going to take a look at the awesome practices that you can observe to upgrade your tests and give them a better look.

- __Make your tests so fast in executing__. Developers expect plug-and-play and fast tests. Imagine an open-source contributor who aims to improve a feature from your project. He does not care about your test development. All he wants is to make his changes and test them and fix any incoming bugs. If the testing process takes too long to execute, he might regret testing his changes in future collaborations.

- __Design your tests readable and simple__. Always think of someone who will read your test and make improvements based on what he has learned from your tests. Your tests might be much more valuable than your documentation for your developers because they are trained to learn technically.

- __Observe DRY and DAMP principles in your tests__. Having these methods in mind would help you to design better tests. A good test contains proper naming, simplicity, isolation, and maintainability.

- __Have a convention for storing your project's tests__. In Python, the best practice for storing your test files is to have a package called `tests` and keep your tests there. Make sure your test files' names start with `test_` which allows test runners to find your tests immediately. The `unittest` package has a discovery feature that always looks for the `test` keyword by default. A brilliant structure is as follows.

```shell
project
├── accounting
├── transaction
├── management
├── tests
│   ├── __init__.py
│   ├── test_accounting.py
│   ├── test_management.py
│   └── test_transaction.py
├── README.md
└── app.py
```

- __Make your tests cross-platform__. Having a cross-platform test comes in handy when it's about CI/CD development where the automated systems work with your tests. Having a stable structure for storing your tests is a crucial key. Simplifying, you have a nice structure when you can filter the test execution with a few options or commands.

### Conclusion
We reached the end but testing never ends. Having a good testing platform would definitely save a lot of your team's time. We saw a simple introduction to Python unit testing at first and then talked about some best practices and principles that would improve your testing skills for sure.