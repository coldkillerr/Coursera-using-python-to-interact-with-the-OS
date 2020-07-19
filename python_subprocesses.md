<h1> Python Subprocesses </h1>

Sometimes it's easier or faster to use a system command as part of our
Python script to accomplish a task, or use some functionality that doesn't exist
in the Python modules, neither built in or external.
For these cases, Python provides a way to execute system commands in our scripts,
using functions provided by the `subprocess` module.

```python3
>>> import subprocess
>>> subprocess.run(["date"])
Sat Jul 18 16:33:34 IST 2020
CompletedProcess(args=['date'], returncode=0)
```
The `run` function returns an object of the `CompletedProcess` type.
This object includes information related to the execution of the command.
From the information that got printed we can see that the `returncode` of
the command was `0`.

To run the external command a secondary environment is created for
the child process or subprocess where the command is executed.
While the parent process, which is our script,
is waiting on the subprocess to finish, it's blocked,
which means that the parent can't do any work until the child finishes.
And I bet a lot of parents out there saying, I know that's right.
After the external command completes its work, the child process exits and
the flow of control returns to the parent.
Then the script can continue with normal execution.

```python3
>>> subprocess.run(["sleep","10"])
CompletedProcess(args=['sleep', '10'], returncode=0)
>>> 
```

The run function receives a list that starts with the name of the command that
we want to call, followed by any other parameters that we want to pass to that command.
So any elements following the program name are the command-line arguments for it. 

```python3
>>> result=subprocess.run(['ls','no_such_file'])
ls: cannot access 'no_such_file': No such file or directory
>>> print(result.returncode)
2
>>> 
```
We can catch the output of the run command using the `capture_output` function.
(This is available in python3.7 and ahead.)

```python3
>>> result=subprocess.run(["host","8.8.8.8"],capture_output=True)
>>> print(result)
CompletedProcess(args=['host', '8.8.8.8'], returncode=0, stdout=b'8.8.8.8.in-addr.arpa domain name pointer dns.google.\n', stderr=b'')
>>> print(result.stdout)
b'8.8.8.8.in-addr.arpa domain name pointer dns.google.\n'
>>> 
```
The output stored as standard output can be obtained using `stdout`.
The `b` at the start specifies that its not a string , its actually an array of bytes.
To convert it to string use decode .

```python3
>>> print(result.stdout.decode())
8.8.8.8.in-addr.arpa domain name pointer dns.google.

>>> print(result.stdout.decode().split())
['8.8.8.8.in-addr.arpa', 'domain', 'name', 'pointer', 'dns.google.']
>>> 
```
We used `split()` so that we can use whatever part of the string we want to use.

If the command fails the error is stored in `stderr` attribute.

```python3
>>> result=subprocess.run(["rm","does_not_exist"],capture_output=True)
>>> print(result.returncode)
1
>>> print(result.stdout)
b''
>>> print(result.stderr)
b"rm: cannot remove 'does_not_exist': No such file or directory\n"
>>> 
```
As `does_not_exist` does not exist , the returncode of the statement is `1` and hence no output is shown on `stdout` and the error is saved in `stderr`.


