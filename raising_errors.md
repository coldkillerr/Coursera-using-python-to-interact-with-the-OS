<h1> Raising Errors In Python </h1>

We can raise a bunch of different
errors that come already
pre-built with Python or we can create our own,
if the standard ones aren't good enough. 


```python3
def validate_user(text,minlen):
	if minlen<1:
		raise ValueError('minimum length must be at least 1')
	if not text.isalnum():
		raise ValueError('Text is invalid')
	if len(text)<minlen:
		return False
	return True


if __name__ == '__main__':
	
	print(validate_user('Nishit78',7))
	print(validate_user('Ram878',10))
	print(validate_user('/.,',8))
```
```sh
$ python3 error_raising.py 
True
False
Traceback (most recent call last):
  File "error_raising.py", line 15, in <module>
    print(validate_user('/.,',8))
  File "error_raising.py", line 5, in validate_user
    raise ValueError('Text is invalid')
ValueError: Text is invalid
```

<h2> Assertion </h2>

The `assert` keyword tries to verify that
a conditional expression is true,
and if it's false it raises
an assertion error with the indicated message.

```python3
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

We've added an assertion that
verifies that the type of the username variable
is STR which we know is
a name that the interpreter uses for strings.
If the function is called with
a username parameter that's not a string,
an error will be raised with the message we provided. 

```python3
>>> from error_raising import validate_user
>>> validate_user([],1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/home/nishit/error_raising.py", line 2, in validate_user
    assert type(text) == str , 'username must be a string' 
AssertionError: username must be a string
>>> 
```
