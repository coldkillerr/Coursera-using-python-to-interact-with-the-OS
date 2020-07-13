<h1> Regular Expressions </h1>

<h2> Definition </h2>

A regular expression, also known as regex or regexp,
is essentially a search query for text that's expressed by string pattern.
When you run a search against a particular piece of text,
anything that matches a regular expression pattern you specified,
is returned as a result of the search. 

Regular expressions allow us to search for strings matching specific pattern in a text block .

Module used :  `re`

<h2> Using grep </h2>



`grep` works by printing
out any line that matches the query that we pass it.
So for a simplest query of passing a plain old string,
grep will print any lines
containing that string in the file that we give it.

```shell

nishit  SHITBOT  ~  grep thon /usr/share/dict/words

Anthony
Anthony's
Johnathon
Johnathon's
Jonathon
Jonathon's
Marathon
Marathon's
Phaethon
Phaethon's
Python
Python's
diphthong
diphthong's
diphthongs
marathon
marathon's
marathoner
marathoner's
marathoners
marathons
python
python's
pythons
telethon
telethon's
telethons
thong
thong's
thongs
```

`grep` is case sensitive . If we want to match with all cases (upper , lower , mixed ) , you should use `-i`

```shell
nishit  SHITBOT  ~  grep python /usr/share/dict/words -i

Python
Python's
python
python's
pythons
```
<h3> Reserved Characters </h3>

It's these characters that allow us to do more
advanced matching than just
checking for a literal string. 

For example, a dot(`.`) matches any character.

```shell
nishit  SHITBOT  ~  grep p.th.n /usr/share/dict/words -i
Python
Python's
diphthong
diphthong's
diphthongs
python
python's
pythons
```

Other easy examples of
special characters that we can use in
a irregular expressions are the caret,
or circumflex and the dollar sign anchor characters.
These tell us where in the line
the regex should match from.
The circumflex (`^`) indicates the beginning (finding patterns that starts-with)
and the dollar sign (`$`) indicates the end of the line (finding patterns that ends-with). 

```shell
nishit  SHITBOT  ~  grep ^fruit /usr/share/dict/words -i
fruit
fruit's
fruitcake
fruitcake's
fruitcakes
fruited
fruitful
fruitfully
fruitfulness
fruitfulness's
fruitier
fruitiest
fruiting
fruition
fruition's
fruitless
fruitlessly
fruitlessness
fruitlessness's
fruits
fruity
```
```shell
nishit  SHITBOT  ~  grep fruit$ /usr/share/dict/words -i
breadfruit
fruit
grapefruit
```
<h2> Using search() </h2>

```python3
>>> result=re.search(r'aza','plaza')
>>> print(result)
<re.Match object; span=(2, 5), match='aza'>
>>> 
```

The `re.search()` function returns the span and match if the match is found in the target text.
The span can be found using `result.span()` method.

```python3
>>> print(result.span())
(2, 5)
>>> 
```
The result is `None` if match is not found
```python3
>>> result=re.search(r'aze','plaza')
>>> print(result)
None
>>> 
```
<h3> Matching using special characters </h3>

```python3
>>> print(re.search(r'^a' , 'apple'))
<re.Match object; span=(0, 1), match='a'>
>>> print(re.search(r'a$' , 'ba'))
<re.Match object; span=(1, 2), match='a'>
>>> print(re.search(r'a.' , 'apple'))
<re.Match object; span=(0, 2), match='ap'>
>>> print(re.search(r'a..' , 'apple'))
<re.Match object; span=(0, 3), match='app'>
>>> 
```

If we want the match to be insensitive use `re.IGNORECASE` in the `re.search()` function.

```python3
>>> print(re.search(r'a..l' , 'Apple',re.IGNORECASE))
<re.Match object; span=(0, 4), match='Appl'>
>>> 
```
