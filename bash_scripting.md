<h1> Bash Scripting </h1>

<h2> Basic Linux Commands </h2>

* `echo` is a command used to print messages to the screen
* `cat` is command for showing contents of files
* `ls` is the command to list contents of a directory
   
  ```shell
  $ ls -l
  total 4
  -rw-r--r-- 1 nishit nishit    0 Jul 25 16:14 new_file.txt
  -rw------- 1 nishit nishit 1679 Jul 25 16:05 qwikUnitTesting.pem
  ```

  The first column indicates the permissions of the file.
  The second column is the number of
  i nodes that point to the file.
  The third and fourth columns indicate
  the owner and the group to which the file belongs.
  Then comes the size of the file that
  they've less modification and finally, the name.
  
  ```shell
  ls -la
  total 44
  drwxr-xr-x  2 nishit nishit  4096 Jul 25 16:14 .
  drwxr-xr-x 48 nishit nishit 36864 Jul 25 14:16 ..
  -rw-r--r--  1 nishit nishit     0 Jul 25 16:14 new_file.txt
  ```
  
  The `-la` shows
  hidden files which are the ones that start with a dot.
  In this case, the only ones
  are the shortcuts that we called out earlier.
  The `.` shortcut, for the current directory,
  and a `..` shortcut for the parent directory.
  The sizes of these directories are
  related to the amount of files in them. 

* `chmod` is a command to change permissions of a file.
* `mkdir` command is used to create a new directory. 
* `cd` command is used change into new directory.
* `pwd` is the command used  to print the current working directory. 
* `cp` command is used tocopy files from one directory to another.

  eg.
  ```shell
  $ cp ../qwikUnitTesting.pem .

  $ ls
  qwikUnitTesting.pem
  ```
  
  The dots `.` are shortcuts that we can
  use to refer to some special directories.
  The dot-dot `..` shortcut reverses a parent directory,
  the previous directory and the absolute path while
  the dot `.` shortcut reverses the current directory.
  So this command is copying the `qwikUnitTesting.pem`
  file located in the previous directory to this directory.
 
* `touch` command is used to create an empty file
* `mv` command is used to rename or move a file .
* `rm` command is used to remove files from directories.
   If we use `rm *` all files are deleted as the `*` acts as a placeholder for all files in the directory.
   if we want to delete a single file , the syntax for it is `rm filename`.
   
   <b> Note : This command works only on empty directories. </b>

<h2> Redirecting Streams </h2>
   
`Redirection` is a process of sending a stream to a different destination. his process is provided to us by the operating system and
can be really useful when you want to store the output of a command in a file,
instead of just looking at it on a screen.
To redirect the standard output of a program to a file
we use the greater than `>` symbol. 

Example:

```shell
$ cat text.py 
#!/usr/bin/env python3
print('text to be redirected to a file')

$ ./text.py 
text to be redirected to a file

$  ./text.py > new_text.txt

$ cat new_text.txt 
text to be redirected to a file
```
Each time we perform of redirection of STDOUT, the destination is overwritten. 
If we want to append the output we use `>>`.

```sh
$ ./text.py >> new_text.txt

$ cat new_text.txt 
text to be redirected to a file
text to be redirected to a file
```

In a similar way we can also redirect standard input.
Instead of using the keyboard to send data into a program,
we can use the less than `<` symbol to read the contents of a file. 

```sh
$ ./streams_err.py 
Enter data :
data to be written
Printing data to STDOUT : data to be written
Traceback (most recent call last):
  File "./streams_err.py", line 5, in <module>
    raise ValueError('Value Error Raised')
ValueError: Value Error Raised

$ ./streams_err.py < new_text.txt 
Enter data :
Printing data to STDOUT : text to be redirected to a file
Traceback (most recent call last):
  File "./streams_err.py", line 5, in <module>
    raise ValueError('Value Error Raised')
ValueError: Value Error Raised

$ cat new_text.txt 
text to be redirected to a file
text to be redirected to a file
```
We can also write the errors from a code to a file using `2f`

```sh
$ ./streams_err.py < new_text.txt 2> error_file.txt
Enter data :
Printing data to STDOUT : text to be redirected to a file

$ cat error_file.txt 
Traceback (most recent call last):
  File "./streams_err.py", line 5, in <module>
    raise ValueError('Value Error Raised')
ValueError: Value Error Raised
```
We didn't see the `ValueError` on screen because it was written to the file `error_file.txt`


The number `2` represents the file descriptor of the `STDERR` stream.
In this context you can think of a file descriptor
as a kind of variable pointing to an IO resource.
`0` and `1` are the file descriptors for `STDIN` and `STDOUT`.

<h2> Pipes and Pipelines </h2>

`Pipes` connect the output of
one program to the input of another.
This means we can pass data between programs,
taking the output of one and
making it the input of the next.
Pipes are represented by the pipe character `|`.

```sh
$ ls -l | less
```

```sh
total 26884
-rwxrwxrwx  1 nishit nishit       56 Jul 21 18:58 argov.py
drwxrwxr-x  2 nishit nishit     4096 May  9 15:16 assets
drwxrwxr-x  2 nishit nishit     4096 Jul 17 11:51 bin
-rw-rw-r--  1 nishit nishit    11636 Jul 27 11:58 Copy of Free Program Participation Certificate Template.doc
x
-rw-rw-r--  1 nishit nishit    41412 Jul 27 11:55 Copy of Free Program Participation Certificate Template.png
drwxr-xr-x  2 nishit nishit     4096 May 19 16:35 Desktop
drwxr-xr-x 14 nishit nishit     4096 Jul 27 13:06 Documents
drwxr-xr-x  3 nishit nishit     4096 Jul 25 13:17 Downloads
-rw-r--r--  1 nishit nishit      156 Jul 27 17:43 error_file.txt
-rw-r--r--  1 nishit nishit       61 Jul 18 15:35 exitc.py
-rw-r--r--  1 nishit nishit       23 Jul  1 19:47 hello.py
-rw-r--r--  1 nishit nishit       21 Jul  9 18:49 hosts.csv
drwxrwxr-x  2 nishit nishit     4096 Jul 13 17:38 include
drwxrwxrwx  3 nishit nishit     4096 Jan 11  2020 local
drwxr-xr-x  3 nishit nishit    61440 Jul 11 22:22 Music
-rw-rw-r--  1 nishit nishit    17638 Jul 24 12:15 newlogodmce.jpg
-rw-r--r--  1 nishit nishit       64 Jul 27 13:51 new_text.txt
drwxr-xr-x  6 nishit nishit     4096 Jul 21 18:12 Pictures
drwxrwxr-x  3 nishit nishit     4096 Jul 25 16:37 ProjectSHITBOT
drwxr-xr-x  2 nishit nishit     4096 Jul 24 13:15 __pycache__
drwxr-xr-x 18 nishit nishit     4096 Jul 19 14:43 Python-3.8.4
:
```

Here, the output of
the `ls-l` command is
connected to the input of the `less` command,
which is a terminal paging program.
This example can be pretty
useful when you want to look at
the contents of a directory containing lots of files.
The list of files generated by `ls` is piped to less,
which displays them one page at a time.
We can scroll up or down using the page up,
page down, or arrow keys.
Once we're done looking at the files,
we can quit with `Q` . 

Example 2 :


We're first using `cat` to get
the contents of our spider.txt file.

```sh
$  cat spider.txt

Incy wincy spider
Climbed up the waterspout
Down came the rain
And washed the spider out
Out came the sunshine
And dried up all the rain
And incy wincy spider
Climbed up the spout again.
Incy wincy spider
Climbed up a tree
Down came the snow
And made poor incy freeze
Out came the sunshine
And melted all the snow
So incy wincy spider
Had another go.
```

Those contents are then sent to a command called `tr`,
which gets its name from the word translate.
It takes the characters in
the first parameter, in this case,
it's a space and then transform
them into a character in the second parameter.
In this case, it's a newline character `\n`.
So basically, what we're doing is
putting each word in its own separate line.


Next, we pass results to the sort command through a pipe.
This command sorts results alphabetically.

```sh
$  cat spider.txt | tr ' ' '\n' | sort

a
again.
all
all
And
And
And
And
And
another
came
came
came
came
Climbed
Climbed
Climbed
Down
Down
dried
freeze
go.
Had
incy
incy
incy
Incy
Incy
made
melted
out
Out
Out
poor
rain
rain
snow
snow
So
spider
spider
spider
spider
spider
spout
sunshine
sunshine
the
the
the
the
the
the
the
the
the
tree
up
up
up
up
washed
waterspout
wincy
wincy
wincy
wincy
```

The sorted results are then passed to the `uniq` command,
which displays each match once,
and by using a `-c` flag,
it prefixes each unique line
with a number of times it occurred.

```sh
$  cat spider.txt | tr ' ' '\n' | sort | uniq 
a
again.
all
And
another
came
Climbed
Down
dried
freeze
go.
Had
incy
Incy
made
melted
out
Out
poor
rain
snow
So
spider
spout
sunshine
the
tree
up
washed
waterspout
wincy
```

This output is passed via pipe to
the `sort` command once more, this time,
with the `-nr` flag,
which sorts results numerically and in reverse order,
from most to least hits.

```
cat spider.txt | tr ' ' '\n' | sort | uniq -c | sort -nr
      9 the
      5 spider
      5 And
      4 wincy
      4 up
      4 came
      3 incy
      3 Climbed
      2 sunshine
      2 snow
      2 rain
      2 Out
      2 Incy
      2 Down
      2 all
      1 waterspout
      1 washed
      1 tree
      1 spout
      1 So
      1 poor
      1 out
      1 melted
      1 made
      1 Had
      1 go.
      1 freeze
      1 dried
      1 another
      1 again.
      1 a
```

The output is finally passed to the `head` command,
which prints the first 10 lines to stdl.

```sh
cat spider.txt | tr ' ' '\n' | sort | uniq -c | sort -nr| head
      9 the
      5 spider
      5 And
      4 wincy
      4 up
      4 came
      3 incy
      3 Climbed
      2 sunshine
      2 snow
```
<h3> Piping in Python </h3>

You can use your Python scripts and pipelines too.
Python can read from standard input using
the stdin file object provided by the sys module. 

```sh
$  cat capitalize.py 
#!/usr/bin/env python3
import sys
for line in sys.stdin:
	print(line.capitalize())
```

```sh
$  cat spider.txt | ./capitalize.py 
Incy wincy spider

Climbed up the waterspout

Down came the rain

And washed the spider out

Out came the sunshine

And dried up all the rain

And incy wincy spider

Climbed up the spout again.

Incy wincy spider

Climbed up a tree

Down came the snow

And made poor incy freeze

Out came the sunshine

And melted all the snow

So incy wincy spider

Had another go.
```
<h2> Signalling Processes </h2>

`Signals` are tokens delivered to running processes to indicate a desired action. Using signals, we can tell a program that we want it to pause or terminate.
We can also cause it to reload its configuration, or to close all open files.
Knowing how to send these signals lets us interact with processes and
have more control over how they behave. 

Example :

```sh
ping www.example.com
PING www.example.com (93.184.216.34) 56(84) bytes of data.
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=1 ttl=57 time=270 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=2 ttl=57 time=223 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=3 ttl=57 time=229 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=4 ttl=57 time=218 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=5 ttl=57 time=349 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=6 ttl=57 time=209 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=7 ttl=57 time=219 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=8 ttl=57 time=212 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=9 ttl=57 time=217 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=10 ttl=57 time=214 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=11 ttl=57 time=220 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=12 ttl=57 time=209 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=13 ttl=57 time=209 ms
^C
--- www.example.com ping statistics ---
14 packets transmitted, 13 received, 7% packet loss, time 13017ms
rtt min/avg/max/mdev = 209.062/231.006/349.040/37.375 ms
```

The `ping` command is now running,
sending `ICMP` packets to machine over the network once per second.
And it will keep running forever unless we interrupt it.
To do that, we use the `Ctrl-C` combination. 
When we interrupt it, the program doesn't just end abruptly.
First it prints a summary of what it did and what the results were.
It's very polite under these circumstances.
What's happening behind the scenes is the process received a signal indicating that
we wanted it to stop.
When that signal's received, the process does whatever it needs to finish cleanly.
The signal that control see sense is called `SIGINT`.
It's just one of many signals that we can send.


Another keyboard combination that we can use to send a signal is `Ctrl-Z`. 

```sh
$  ping www.example.com
PING www.example.com (93.184.216.34) 56(84) bytes of data.
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=1 ttl=57 time=209 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=2 ttl=57 time=211 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=3 ttl=57 time=208 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=4 ttl=57 time=208 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=5 ttl=57 time=210 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=6 ttl=57 time=221 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=7 ttl=57 time=211 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=8 ttl=57 time=210 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=9 ttl=57 time=230 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=10 ttl=57 time=209 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=11 ttl=57 time=209 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=12 ttl=57 time=208 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=13 ttl=57 time=216 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=14 ttl=57 time=208 ms
^Z
[1]+  Stopped                 ping www.example.com
```
The signal that we sent is called `SIGSTOP`.
This signal causes the program to stop running without actually terminating.
But don't worry, we can make it run again by executing `fg` 

```sh
$ fg
ping www.example.com
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=15 ttl=57 time=208 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=16 ttl=57 time=210 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=17 ttl=57 time=216 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=18 ttl=57 time=208 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=19 ttl=57 time=209 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=20 ttl=57 time=210 ms
^C
--- www.example.com ping statistics ---
20 packets transmitted, 20 received, 0% packet loss, time 203578ms
rtt min/avg/max/mdev = 208.388/211.985/230.643/5.374 ms
```
To send other signals, we can use the command called `Kill` .
By default, Kill will send a signal called `SIGTERM` that tells the program to terminate.


Since Kill is a separate program, we need to run it on a separate terminal.
And we also need to know the process identifier or
`PID` of the process that we want to send the signal to.


To find out the PID that we want to send the signal to,
we'll use the `ps` command which list the currently running processes.
Depending on what options that we pass,
it'll show different subsets of processes with different amounts of detail.


For this example, we'll call `ps ax`,
which lists all the running processes in the current computer.
And then we'll use the `grep` command to only keep lines that contain the name of
the process that we're looking for.


```sh
$  ping www.example.com
PING www.example.com (93.184.216.34) 56(84) bytes of data.
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=1 ttl=57 time=202 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=2 ttl=57 time=202 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=3 ttl=57 time=203 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=4 ttl=57 time=203 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=5 ttl=57 time=212 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=6 ttl=57 time=202 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=7 ttl=57 time=202 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=8 ttl=57 time=205 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=9 ttl=57 time=202 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=10 ttl=57 time=202 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=11 ttl=57 time=205 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=12 ttl=57 time=256 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=13 ttl=57 time=219 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=14 ttl=57 time=202 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=15 ttl=57 time=210 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=16 ttl=57 time=202 ms
64 bytes from 93.184.216.34 (93.184.216.34): icmp_seq=17 ttl=57 time=274 ms
Terminated
```

```sh
 $  ps ax | grep ping 
\ 1545 ?        Sl     0:00 /usr/lib/x86_64-linux-gnu/cinnamon-settings-daemon/csd-housekeeping
28321 pts/0    S+     0:00 ping www.example.com
28405 pts/1    S+     0:00 grep --color=auto ping
$ kill 28321
```

We've now sent the `SIGTERM` signal and the process was terminated.

<h2> Bash scripting </h2>

We can use `Bash` to write simple scripts when we need to use a lot of commands.

Example :

```sh
#!/bin/bash

echo "Starting at : $(date)"
echo

echo "UPTIME"
uptime 
echo

echo "FREE"
free 
echo

echo "WHO"
who 
echo

echo "Finishing at $(date)"
```

```sh
$  ./bash_1.sh 
Starting at : Thu Jul 30 11:02:25 IST 2020

UPTIME
 11:02:25 up 12:52,  1 user,  load average: 2.81, 3.01, 3.10

FREE
              total        used        free      shared  buff/cache   available
Mem:        3931304     2292156      227824      418704     1411324      972480
Swap:       2097148       96500     2000648

WHO
nishit   tty7         2020-07-29 22:09 (:0)

Finishing at Thu Jul 30 11:02:25 IST 2020
```
<h2> Variables </h2>

Bash lets us use
variables to store and retrieve values.

`Environment variables` are variables that are set in
the environment in which the command is executing.
We mentioned that we set
these variables using the equals `=` sign.
When we want to access the value of a variable in bash,
we need to prefix the name of
the variable with the dollar `$` sign.


On top of the predefined environment variables,
we can also define our own variables for our scripts.
To do that we just assign a value
to the name of the variable that we want to define. 

eg.

```sh
$ example=hello

$ echo $example
hello
```
There can be `no spaces` between the name
of the variable and the equal sign,
or between the equal sign and the value. 

<h2> Globs </h2>

`Globs` are characters that allow
us to create `list of files`.
The star `*` and question mark `?` are the most common globs.
Using these globs lets us create sequences of
filenames that we can use as
parameters to the commands we call in our scripts.

```sh
$  echo *sh
bash_1.sh encrypt.sh install.sh passwordGen.sh
```

```sh
echo p*
passwordGen.sh password.txt password.txt.save
```

```sh
$ echo ??????.sh
bash_1.sh
```
The `*` is used to replace a series of characters whereas `?` replaces a single character.
We can use this functionality in python using the `glob` module.

<h2> Conditional Execution in Bash </h2>

<h3> If statement </h3>

In bash scripting, the condition used is based on the exit status of commands.
We check the exit status for
command using the dollar sign question mark.
This logic is used by the if operator in bash.
To create a conditional expression, we're going to call a command and if the exit
status of that command is zero, then the condition will be considered true. 

Eg.

```sh

#!/bin/bash

if  grep "127.0.0.1" /etc/hosts ; then
	echo "all good"
else
	echo "ERROR ! 127.0.0.1 is not in hosts"
fi
```

```sh
$ ./check_localhost.sh 
127.0.0.1	localhost
all good
```


We start with the `if` keyword followed by the `grep` command that we'll use to
check for success.
At the end of the command, we have a semicolon `:` followed by the word `then`.
After that comes the body of the `conditional`.
We're using `indentation` like in Python.
We also have an `else` block for when the command doesn't finish successfully.
And finally, our conditional block finishes using the `fi` keyword. 

<h3> Test Statement </h3>

Test is a command that evaluates the conditions received and
exits with zero when they are true and with one when they're false. 

