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
