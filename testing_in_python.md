<h1> Testing In Python </h1>

<b>Software testing</b> is a process of evaluating
computer code to determine
whether or not it does what you expect it to do.
Tests can help make good code great.

<h2> Manual And Automated Testing </h2>

The most basic way of testing a script is to run it with
different parameters and see if it
returns the expected values.

Executing a script with
different command-line arguments to see
how its behavior changed is an example of `manual testing.`
Using the interpreter to try our code before
putting it in a script is another form of manual testing.

`Formal software testing` takes us process a step further,
codifying tests into
its own software and code that can be
run to verify that
our programs do what we expect them to do.
This is called `automatic testing`.

The goal of automatic testing
is to automate the process of
checking if the returned value matches the expectations.
Instead of us humans running
a function over and over with
different parameters and checking
the results are what we expected them to be,
we let the computer do this for us.
Automatic testing means we'll write code to do the test. 

<h2> Unit Tests </h2>

Unit tests are used to verify that
`small isolated parts` of a program are correct.
Unit tests are generally written
alongside the code to test the behavior
of individual pieces or units like functions or methods. 

An important characteristic of a unit test is `isolation`.
Unit test should only test the unit of code they target,
the function or method that's being tested.
This ensures that any success or
failure of the test is caused by the behavior of the unit
in question and doesn't result from some external factor
like the network being down
or a database server being unresponsive.

<h2> Writing Automatic Tests in Python </h2>

For this we create a test code in the same directory as the `code_to_be_tested.py` as `code_to_be_tested_test.py`.
Python provides us with a module called `unittest` for testing purposes.
The unittest module provides a `TestCase` class with a bunch of testing methods
ready to use. 

<h4>Code : </h4>

```python3

#!/usr/bin/env python3
import re
def check_web_address(text):
  pattern = r"[a-zA-Z]*\.[a-zA-Z]*$"
  result = re.search(pattern, text)
  return result != None

if __name__ == '__main__':

	print(check_web_address("gmail.com")) # True
	print(check_web_address("www@google")) # False
	print(check_web_address("www.Coursera.org")) # True
	print(check_web_address("web-address.com/homepage")) # False
	print(check_web_address("My_Favorite-Blog.US")) # True

```

<h4> Test Code : </h4>

```python3
#!/usr/bin/env python3
from reg import check_web_address
import unittest

class TestReg(unittest.TestCase):
	def test_basic(self):
		testcase='www.coursera.org'
		expected= True
		self.assertEqual(check_web_address(testcase),expected)


unittest.main()

```

<h3> Edge Cases </h3>

Edge cases are inputs to our code that produce unexpected results, and
are found at the extreme ends of the ranges of input we imagine our
programs will typically work with.
Edge cases usually need special handling in scripts in order for
the code to continue to behave correctly.

```python3
def test_empty(self):
	testcase = ''
	expected = False
	self.assertEqual(check_web_address(testcase),expected)

```


<h3> Basic assertions </h3>

|           Method          |      Checks that     | New in |
|:-------------------------:|:--------------------:|:------:|
| `assertEqual(a, b)`         | a == b               |        |
| `assertNotEqual(a, b)`      | a != b               |        |
| `assertTrue(x)`             | bool(x) is True      |        |
| `assertFalse(x)`            | bool(x) is False     |        |
| `assertIs(a, b)`            | a is b               | 3.1    |
| `assertIsNot(a, b)`         | a is not b           | 3.1    |
| `assertIsNone(x)`           | x is None            | 3.1    |
| `assertIsNotNone(x)`        | x is not None        | 3.1    |
| `assertIn(a, b)`            | a in b               | 3.1    |
| `assertNotIn(a, b)`         | a not in b           | 3.1    |
| `assertIsInstance(a, b)`    | isinstance(a, b)     | 3.2    |
| `assertNotIsInstance(a, b)` | not isinstance(a, b) | 3.2    |


<h2> Black Box VS White Box </h2>

`White-box testing` also sometimes
called `clear-box` or `transparent
testing` relies on the test creators knowledge of
the software being tested to construct the test cases.
With a white-box test,
the test creator knows how the code
works and can write test cases that
use the understanding to make sure
that everything is performing the way it's expected to. 

`Black-box tests` are written with
an awareness of what the program is supposed to do,
its requirements or specifications,
but not how it does it. 
In black-box testing,
the software being tested is treated like an opaque box.
In other words, the tester doesn't know
the internals of how the software works.


If the unit tests are `created before any code` is
written based on specifications
of what the code is supposed to do,
they can be considered `black-box` unit test.

If unit tests are `run alongside`
or after the code has been developed,
the test cases are made with
a knowledge of how software works.
They are `white-box` tests.

<h2> Other Test Types </h2>

`Integration tests` take the individual modules of code that unit test
verify then combine them into a group to test.
Depending on what our program does, and
how it interacts with the rest of the systems involved,
we might need to create a separate test environment for our test. 


While unit tests shouldn't cross boundaries to do things like
make a network request or integrate with an API or database,
the goal of an integration test is to verify these kinds of interactions and
make sure the whole system works how you expect it to.

A variant of unit tests are `regression tests`.
They're usually written as part of a debugging and troubleshooting process
to verify that an issue or error has been fixed once it's been identified.
Say our script has a bug and we're trying to fix it.
A good approach to doing this would be the first right to test fails by triggering
the buggy behavior, then fix the bug so that a test passes.
Regression tests are useful part of a test suite because they ensure
that the same mistake doesn't happen twice.

`Smoke test` sometimes called build verification test,
get their name from a concept that comes from testing hardware equipment.
When writing software smoke test serve as
a kind of sanity check to find major bugs in a program.
These tests are usually run before more refined testing takes place.
Since if the software fails the smoke test you can be pretty
sure none of the other tests will pass either.


`Load tests` verify that the system behaves well when it's under significant load.
To actually perform these tests will need to generate traffic to our application
simulating typical usage of the service.
These tests can be super-helpful when deploying new versions of our applications
to verify that performance does not degrade. 


Taking together a group of tests of one or
many kinds is commonly referred to as a `test suite`. 

<h2> Testing for Expected Errors </h2>

With some `edge cases` the expectation is that the function will raise an error and
we want to be able to test that too.
Well, we use the `assertRaises` method provided by the `unittest` module. 

```python3
# code to be tested

def validate_user(text,minlen):
	assert type(text) == str , 'username must be a string' 
	if minlen<1:
		raise ValueError('minimum length must be at least 1')
	if not text.isalnum():
		raise ValueError('Text is invalid')
	if len(text)<minlen:
		return False
	return True
```

```python3
# test code
import unittest
from validations import *

class TestReg(unittest.TestCase):
	def test_basic(self):
		testcase_text='Nishit78'
		testcase_len=7
		expected= True
		self.assertEqual(validate_user(testcase_text,testcase_len),expected)

	def test_too_short(self):
		self.assertEqual(validate_user('Ram878',10),False)

	def test_invalid_minlen(self):
		self.assertRaises(ValueError,validate_user,'user',-1)




unittest.main()
```

```shell
$ python3 validations_test.py 
...
----------------------------------------------------------------------
Ran 3 tests in 0.000s

OK
```

We can see that the `assertRaises` method works a little bit differently than
the `assertEqual` method that we used before.
In this case,
we need to first pass the error that we expect the function to raise.
Then the function name,
followed by any parameters that need to be passed to that function.
Behind the scenes, this method is calling the function that we want to test
using the try except block and
checking that it does raise the error that we said it would raise. 










<h2> Test Driven Development </h2>

A process called test-driven development or
TDD calls for creating the test before writing the code.
This might seem a bit counter-intuitive,
but it can make for
more thoughtful well-written programs. 


