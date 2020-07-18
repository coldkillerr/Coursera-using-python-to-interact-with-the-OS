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



