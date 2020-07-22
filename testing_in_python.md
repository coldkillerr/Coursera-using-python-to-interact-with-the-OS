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

