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
