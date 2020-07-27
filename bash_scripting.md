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
we use the greater than symbol. 

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




