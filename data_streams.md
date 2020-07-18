<h1> Data Streams </h1>

<h2> Standard Streams </h2>

<h3> I/O streams </h3>

I/O streams are the basic mechanism for performing input and output operations in your programs

How does a Python program connect to both the screen and the keyboard?
Well, it uses I/O streams.
I/O streams are the basic mechanism for performing input and
output operations in your programs.

Most operating systems supply three different I/O streams by default each with
a different purpose. 

* `STDIN` 

The standard input stream commonly referred to as STDIN is a channel
between a program and a source of input.
Usually in the form of text data from the keyboard.
When we use the input function to accept user input in a Python script we're
using the STDIN stream.

* `STDOUT`

The standard output stream or STDOUT is a pathway between a program and
a target of output, like a display.
STDOUT generally takes the form of text displayed in a terminal.
As that play when we use the print function to write information to
the screen.

* `STDERR` 

Standard error displays output like standard out, but is used
specifically as a channel to show error messages and diagnostics from the program.
It's usually printed to the screen.
If you've ever run some Python code and receive an error,
then that error message was probably printed using standard error stream. 

I/O streams are ways for programs to get and receive information. 

<h2> Environment Variables </h2>

Python programs get executed
inside a shell command-line environment.
The variable set in
that environment which are called
environment variables are another source
of information that we can use in our scripts.

 <h3>The PATH Variable</h3>
 
```shell
$ echo $PATH
/home/nishit/.local/bin:/home/nishit/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
```
The shell uses this environment variable to
figure out where to look for executable files,
and we call them while specifying a directory.
All those directories listed there are
where the shell will look for programs.  

<h3> Environment Variables in Python </h3>
 
To access environment variables,
we use the `Environ` dictionary provided by the `OS` module. 

```python3
>>> import os
>>> print("HOME : {}".format(os.environ.get("HOME","")))
HOME : /home/nishit
>>> print("SHELL : {}".format(os.environ.get("SHELL","")))
SHELL : /bin/bash
>>> print("USER : {}".format(os.environ.get("USER","")))
USER : nishit
>>> 
```

To define a variable a way that
our script we'll be able to see it,
we need to run this in our command-line. 

```sh
$ export FRUIT=pineapple
```

```python3
>>> import os
>>> print("FRUIT : {}".format(os.environ.get("FRUIT","")))
FRUIT : pineapple
>>> 
```
<h3> Command-Line Arguments </h3>

These are parameters that are
passed to a program when it started. 
We can access them using `argv` list in the `sys` module.
