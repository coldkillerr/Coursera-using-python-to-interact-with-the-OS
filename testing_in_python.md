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



