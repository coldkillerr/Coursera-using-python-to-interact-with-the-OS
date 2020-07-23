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
