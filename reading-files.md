<h1> Reading files in python </h1>

Open file and return a corresponding file object. If the file cannot be opened, an OSError is raised.


`file = open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)`


<h2> Different modes to open a file </h2>


| Character 	| Meaning 	|
|:-:	|:-:	|
| 'r' 	| open for reading (default) 	|
| 'w' 	| open for writing, truncating the file first 	|
| 'x' 	| open for exclusive creation, failing if the file already exists 	|
| 'a' 	| open for writing, appending to the end of the file if it exists 	|
| 'b' 	| binary mode 	|
| 't' 	| text mode (default) 	|
| '+' 	| open for updating (reading and writing) 	|

The default mode is 'r' (open for reading text, synonym of 'rt'). Modes 'w+' and 'w+b' open and truncate the file. Modes 'r+' and 'r+b' open the file with no truncation.
